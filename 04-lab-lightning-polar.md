       

Módulo 05 · Lightning Network · Sesión 4 · Laboratorio

# Laboratorio Lightning con Polar

Del canal bilateral al pago enrutado: abrimos canales, enviamos invoices, debuggeamos HTLCs y provocamos un force-close sobre una red Lightning _regtest_ levantada en nuestro propio equipo host.

**Manuel Montenegro** Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

## Objetivos de la sesión

Al acabar esta práctica deberíais ser capaces de:

*   Levantar una red Lightning local con varios nodos LND conectados entre sí.
*   Abrir y cerrar canales (cooperativamente y forzadamente) e inspeccionar las transacciones on-chain asociadas.
*   Enviar pagos enrutados multi-hop y observar cómo los HTLCs se propagan y se liquidan.
*   Distinguir _outbound_ e _inbound liquidity_ y diagnosticar por qué un pago falla.
*   Decodificar una invoice BOLT 11 identificando cada uno de sus segmentos.
*   Realizar un pago Keysend (espontáneo, sin invoice).

## Prerrequisitos

*   **Polar 3.x** instalado. Descarga: [lightningpolar.com](https://lightningpolar.com).
*   **Docker Desktop** arrancado (Polar orquesta contenedores por debajo). Descarga: [docker.com](https://www.docker.com/products/docker-desktop/). Comprobación rápida: `docker run hello-world`.
*   Haber revisado las slides de la **sesión 3 · Teoría Lightning Network**, especialmente los bloques de HTLCs, canales, liquidez y BOLT 11.
*   Navegador con acceso a [lightningdecoder.com](https://lightningdecoder.com).

Bloque 0

## Setup de Polar

1.  Arranca Polar. Menú _File → New Network_. Llama al network `lab-lightning`.
2.  Configura la topología inicial: **4 nodos LND** (los renombras Alice, Bob, Carol y Dave) y **1 nodo Bitcoin Core**. Polar añade todos los servicios por defecto al crear el network.
    
    Nota
    
    **¿Qué es un nodo LND?** LND (_Lightning Network Daemon_) es una de las implementaciones de referencia de un nodo Lightning. Es el software que habla BOLT con otros nodos, mantiene el estado de los canales, construye las commitment transactions, enruta HTLCs y firma los pagos. Junto a Core Lightning (CLN) y Eclair, es uno de los clientes Lightning más usados en producción.
    
    **¿Qué hace aquí el nodo Bitcoin Core?** Un nodo Lightning _no_ es autónomo: necesita un nodo Bitcoin por debajo para leer la blockchain, detectar confirmaciones de las funding transactions, vigilar que la contraparte no publique un estado antiguo (_justice transactions_) y retransmitir los cierres de canal. El nodo Bitcoin Core cumple aquí ese papel de backend on-chain para los 4 nodos LND, además de minar bloques bajo demanda en regtest para simular la confirmación.
    
    **Un solo Bitcoin Core para los 4 LND.** En esta práctica los 4 nodos LND se conectan al _mismo_ nodo Bitcoin Core para ahorrar recursos del equipo host. En un despliegue real, lo ideal por seguridad y privacidad es que cada nodo LND tenga su propio nodo Bitcoin Core: así evitas filtrar a un tercero qué transacciones te interesan y no dependes de un único punto de fallo.
    
3.  Pulsa _Start_ en la barra superior. Espera a que los 5 servicios aparezcan en verde ("Running"). La primera vez tarda ~30 s mientras Docker descarga imágenes.
4.  Explora la interfaz de Polar. Fíjate en las opciones de minado de la red. Pulsa en un nodo Bitcoin y mira su información, conexiones y acciones. Haz lo mismo con uno de los nodos LND.
5.  Añade fondos al nodo **Alice**. Pulsa en el nodo, ve a la pestaña _Actions_ y deposita **100 000 000 sats**.
    
    Observación
    
    Observa el _block height_ de nuestra blockchain. ¿Qué valor tiene ahora? ¿Por qué ese valor?
    
6.  Abre el terminal embebido de Alice: click sobre el nodo → panel lateral derecho → pestaña _Actions_ → botón _Launch_ (o abre una shell al contenedor con Docker). Comprueba:
    
    ```
    alice$ lncli getinfo
    alice$ lncli walletbalance
    ```
    
7.  Repite el proceso de añadir fondos para el resto de nodos: **Bob**, **Carol** y **Dave**. En cada uno, pestaña _Actions_ → depositar **100 000 000 sats**. Al terminar, los 4 nodos LND deben tener saldo on-chain disponible.

Checkpoint

Los 4 nodos LND y el nodo Bitcoin Core están "Running". Cada nodo Lightning tiene **100 000 000 sats** en su wallet on-chain. El explorer de Polar muestra la cadena regtest con más de 100 bloques minados.

Bloque 1

## Anatomía de un canal

Abrimos y cerramos un primer canal Alice ↔ Bob desde línea de comandos para observar paso a paso la _funding transaction_, el canal en _Pending Open_ y la transición a _Open_ según se van minando bloques. Después repetimos la operación desde la interfaz gráfica de Polar, donde todo el flujo se colapsa en un único clic.

### Fase A · Abrir y cerrar un canal desde línea de comandos

1.  **Obtén el pubkey de Bob.** Desde el terminal embebido de Bob (_Actions → Launch_):
    
    ```
    bob$ lncli getinfo | grep identity_pubkey
    ```
    
    Copia la cadena hex de 66 caracteres.
2.  **Abre el canal desde el terminal de Alice sin minar bloques.**
    
    ```
    alice$ lncli openchannel --node_key=<pubkey_bob> --local_amt=5000000
    ```
    
    LND construye, firma y broadcastea la funding tx a la mempool de bitcoind.
3.  **Observa el estado _Pending Open_.** En Polar, el canal aparece en color naranja y el contador `Channels` de Alice y Bob pasa a `0 / 1 / 0`. Confírmalo también por CLI:
    
    ```
    alice$ lncli pendingchannels
    alice$ lncli listchannels
    ```
    
    Observación
    
    ¿Por qué el canal está en estado _Pending_ y no directamente _Active_?
    
4.  **Mina 6 bloques** pulsando 6 veces en el botón de _Quick Mine_. Observa cómo, al llegar a la sexta confirmación, el canal pasa de _Pending_ a _Open_.
5.  **Alice inspecciona el canal ya abierto.**
    
    ```
    alice$ lncli pendingchannels
    alice$ lncli listchannels
    ```
    
    Fíjate en los campos `capacity`, `local_balance` y `remote_balance`.
    
    Observación
    
    ¿Cuánto tiene Alice en su lado del canal? ¿Y cuánto tiene Bob? ¿Por qué Alice tiene menos que Bob?
    
6.  Bob crea una invoice de 100 000 sats:
    
    ```
    bob$ lncli addinvoice --amt 100000 --memo "un cafe"
    ```
    
    Copia el campo `payment_request` (empieza por `lnbcrt...`).
    
    Recordatorio · Invoice
    
    En **Bitcoin on-chain**, para pagar a alguien basta con su dirección: el pagador construye y firma por su cuenta una transacción contra esa dirección y la broadcastea a la red. El flujo lo inicia el que paga.
    
    En **Lightning (off-chain)** el flujo se invierte: es el _receptor_ quien tiene que generar primero una _invoice_ (o _payment request_), que contiene el `payment_hash`, el importe, un expiry y otros metadatos. Esa invoice es el contrato que el pagador necesita para poder construir el HTLC (_Hash Time-Locked Contract_): sin ella no sabe qué _preimage_ tiene que desvelar el receptor para cobrar. Por eso aquí Bob crea la invoice antes de que Alice pueda pagarle.
    
    Observación
    
    Fíjate en el campo `r_hash` que devuelve `addinvoice`. ¿Qué es exactamente ese valor? ¿Quién lo ha generado y qué papel va a jugar cuando Alice pague la invoice?
    
7.  Alice paga la invoice:
    
    ```
    alice$ lncli payinvoice <payment_request>
    ```
    
    Confirma con `y` cuando te pregunte. Comprueba después con `lncli channelbalance` y `lncli listchannels`: Alice ha perdido 100 000 sats de su `local_balance` y Bob los ha ganado en el suyo.
    
    Observación
    
    ¿Es esta una transacción que va a parar a la mempool y por tanto minada? ¿Por qué?
    
8.  Alice cierra el canal cooperativamente desde la CLI usando el `funding_txid` y el `output_index` que devolvió `listchannels`:
    
    ```
    alice$ lncli closechannel --funding_txid <txid>
    ```
    
    Mina 1 bloque para confirmar el cierre. Observa cómo el `confirmed_balance` de Alice y de Bob ha cambiado.

### Fase B · Abrir, inspeccionar y cerrar desde la interfaz gráfica

1.  **Abre un canal desde la interfaz.** En el lienzo de Polar, **arrastra** desde Alice hasta Bob (o click derecho sobre Alice → _Create Channel_). Capacidad: **5 000 000 sats**. Iniciador: Alice. Pulsa _Open Channel_. Polar firma la funding tx y mina automáticamente 6 bloques: el canal pasa a _Open_ casi al instante.
2.  **Explora el canal desde la interfaz.** Pulsa sobre la línea que une Alice y Bob. El panel lateral abre el diálogo _Channel Details_ con:
    
    *   `Status` — estado del canal (_Open_).
    *   `Capacity` — 5 000 000 sats.
    *   `Source Balance` / `Destination Balance` — saldo en cada lado del canal.
    *   `Channel Point` — `<funding_txid>:<output_index>`, el UTXO 2-of-2 que ancla el canal en la blockchain.
    *   `Is Private` — si el canal es unannounced (_true_) o público (_false_).
    
    Debajo aparecen los bloques _Source Node_ y _Destination Node_ con el nombre, la implementación (LND), la versión y el estado de cada extremo. Observa además cómo el contador `Channels` de Alice y Bob en el panel de nodo muestra ahora `1 / 0 / 0`.
3.  **Bob crea una invoice desde la interfaz.** Pulsa sobre el nodo de Bob, abre la pestaña _Actions_ y en la tarjeta _Create Invoice_ introduce **3 000 000 sats**. Pulsa _Create Invoice_: Polar muestra el `payment_request` completo (`lnbcrt…`). Cópialo al portapapeles con el botón de copiar.
4.  **Alice paga la invoice desde la interfaz.** Pulsa sobre el nodo de Alice, abre la pestaña _Actions_ y en la tarjeta _Pay Invoice_ pega el `payment_request` que acabas de copiar. Pulsa _Pay Invoice_. Vuelve a pulsar sobre el canal y observa cómo `Source Balance` y `Destination Balance` se han actualizado: Alice tiene 3 000 000 sats menos y Bob 3 000 000 sats más.
5.  **Cierra el canal desde la interfaz.** Click derecho sobre el canal → _Close Channel_ y confirma. Polar emite la _cooperative close_, la mina automáticamente y el canal desaparece del lienzo. Los sats vuelven a la wallet on-chain de Alice y Bob.

¿Qué ocurre al cerrar un canal?

Cerrar un canal significa liquidar on-chain el saldo off-chain que los dos peers han ido acumulando. Para ello se construye y se publica en la red Bitcoin una transacción especial llamada **closing transaction**.

Esta transacción **gasta el UTXO 2-of-2** que abrió el canal (la _funding tx_) y crea dos nuevas salidas on-chain: una por el saldo final de Alice y otra por el saldo final de Bob. Cuando los dos peers están de acuerdo en el reparto —el caso normal— hablamos de _cooperative close_: ambos firman conjuntamente la closing tx, se paga una única fee on-chain, y los fondos vuelven a estar disponibles en cuanto la transacción se confirma en un bloque.

Si uno de los peers no coopera o está desconectado, el otro puede cerrar unilateralmente publicando su _commitment transaction_ más reciente (_force-close_). En ese caso los fondos tardan más en liberarse, porque la salida del que inició el cierre está sujeta a un _timelock_ `CheckSequenceVerify` que permite al otro peer contestar si detecta fraude.

Checkpoint

Has vivido el ciclo completo de un canal por los dos caminos: primero paso a paso desde línea de comandos, viendo la funding tx en la mempool, el canal en _Pending_ y su transición a _Open_ según se minan bloques; y después con un solo clic desde la interfaz gráfica, que colapsa todo el flujo en una acción instantánea.

Bloque 2

## Enrutado multi-hop con HTLCs

Reproducimos el ejemplo canónico de la sesión teórica: Alice paga a Dave pasando por Bob y Carol. Observamos cómo el balance se desplaza a lo largo de toda la cadena de canales.

1.  Monta la topología **Alice ↔ Bob ↔ Carol ↔ Dave**. Cada canal de 5 000 000 sats, iniciado por el nodo "izquierdo". Mina 6 bloques y espera a que los tres canales estén _Open_.
2.  **Antes del pago**, prueba que Dave intente enviar 100 000 sats a Alice. Alice crea una invoice primero y Dave intenta pagarla. ¿Qué ocurre? Lee con atención el mensaje de error.
3.  Diagnostica la causa inspeccionando desde la interfaz los canales de Dave y sus saldos `Source Balance` / `Destination Balance`. ¿Cuánto puede enviar Dave ahora mismo?
4.  Ahora en sentido correcto: Dave crea una invoice de 1 000 000 sats desde la interfaz.
5.  Alice paga la invoice desde la interfaz gráfica. Si quieres inspeccionar antes la ruta que LND elegirá, puedes consultarla desde la CLI:
    
    ```
    alice$ lncli queryroutes --dest <pubkey_dave> --amt 1000000
    ```
    
6.  Inspecciona las fees cobradas por los intermediarios:
    
    ```
    bob$ lncli feereport
    carol$ lncli feereport
    ```
    
    Observación
    
    ¿Cuántos sats ha ganado cada intermediario por reenviar el pago? Y dentro del array `channel_fees`, ¿qué significan los campos `base_fee_msat` y `fee_rate`?
    
7.  Comprueba los balances finales en los 4 nodos. Dibuja mentalmente cómo se ha desplazado la liquidez a través de toda la cadena.
8.  **Repite el paso 2**: Dave paga ahora 100 000 sats a Alice. ¿Funciona esta vez? ¿Por qué?

Observación clave

Un canal sin _outbound liquidity_ no puede enviar pagos, por mucha capacidad que tenga. El capital es direccional: 1 BTC de tu lado ≠ 1 BTC de capacidad del canal.

Bloque 3

## Liquidez inbound / outbound

Experimentamos en carne propia la asimetría del capital en Lightning. Un comercio que sólo recibe pagos se queda sin inbound rápidamente.

1.  Añade un nuevo nodo LND **Erin** al network y añádele fondos.
2.  Dave abre un canal hacia Erin de 10 000 000 sats. Polar se encargará de minar 6 bloques para confirmarlo.
3.  Examina el canal Dave → Erin desde la interfaz. Tiene 10M de _inbound_ pero ningún sat _outbound_.
4.  Simula el caso "comercio": Erin crea una invoice de 1 000 000 sats desde la interfaz y Alice la paga también desde la interfaz. La ruta será `Alice → Bob → Carol → Dave → Erin`. El pago funciona y, tras cobrar, Erin ahora tiene **1 000 000 sats outbound**.
5.  Erin recibe ventas, ventas, ventas. Repite 4 pagos más de 1M cada uno desde Alice hasta Erin. Al quinto ya verás que falla: los _canales intermedios_ se quedan sin liquidez en la dirección Alice → Erin, o el propio canal Dave↔Erin ya tiene todo el balance del lado de Erin.

Checkpoint

Entiendes por qué un comercio que sólo recibe pagos Lightning sufre un problema de inbound. En el mundo real, los **LSPs** (Lightning Service Providers) y los **submarine swaps** existen para resolver esto: el LSP te abre un canal con inbound ya "cargado" a cambio de una tarifa.

Un **submarine swap** es un intercambio atómico entre sats on-chain y sats off-chain: envías bitcoins on-chain a un proveedor y a cambio recibes liquidez Lightning (o al revés, conviertes saldo en un canal en un pago on-chain sin cerrar el canal). Los dos movimientos quedan atados por el mismo HTLC, así que o se completan los dos o no se completa ninguno — sin necesidad de confiar en el proveedor.

Bloque 4

## BOLT 11 y variantes

Diseccionamos una invoice real y probamos el pago espontáneo sin invoice (keysend).

1.  Alice genera una invoice "rica" con descripción, importe y expiración personalizada:
    
    ```
    alice$ lncli addinvoice \
      --amt 25000 \
      --memo "1 cup coffee" \
      --expiry 3600
    ```
    
    Copia el `payment_request`.
2.  Abre [lightningdecoder.com](https://lightningdecoder.com) y pega la invoice. Identifica:
    *   **Human Readable Part**: empieza por `lnbcrt` (prefijo de red _regtest_).
    *   **Amount**: 25 000 sats codificados.
    *   **Timestamp**: segundos desde Unix Epoch.
    *   **Payment hash** (tagged field `p`): 32 bytes.
    *   **Description** (tagged field `d`): "1 cup coffee".
    *   **Signature** del nodo destino (104 chars bech32).
3.  Decodifícala también desde CLI y compara:
    
    ```
    alice$ lncli decodepayreq <payment_request>
    ```
    
4.  Genera una invoice **sin importe** (amount-less):
    
    ```
    alice$ lncli addinvoice --memo "donacion libre"
    ```
    
    Decodifícala. ¿Qué campo clave no aparece? ¿Para qué casos de uso sirven estas invoices? Ahora págala desde Bob indicando explícitamente el importe con el flag `--amt`:
    
    ```
    bob$ lncli payinvoice --amt 2000 <payment_request>
    ```
    
    Confirma con `y`. Sin el flag `--amt`, `payinvoice` fallaría: la invoice no fija cantidad, así que es el pagador quien la decide en el momento del pago.
5.  **Keysend** — pago sin invoice. Dave publica su pubkey:
    
    ```
    dave$ lncli getinfo
    # copia el campo identity_pubkey
    ```
    
    Alice le envía 10 000 sats directamente:
    
    ```
    alice$ lncli sendpayment \
      --keysend \
      --dest <pubkey_de_dave> \
      --amt 10000
    ```
    

Cuándo usar cada una

**Invoice amount-less** — útil cuando el receptor sabe que va a cobrar pero no cuánto: donaciones, _tip jars_, crowdfunding con precio libre. Inconvenientes: sigue siendo de un solo uso, el receptor no firma ningún importe dentro de la invoice (no hay prueba criptográfica de qué cantidad "tocaba" pagar) y abre vector de ingeniería social (pueden confundirte sobre cuánto debes pagar).

**Keysend** — útil cuando el pagador quiere enviar sin coordinación previa: _podcasting 2.0_ (streaming de sats en tiempo real), tips espontáneos a una pubkey conocida, mensajería Lightning. Inconvenientes: no está en el BOLT oficial, el receptor no recibe factura firmada (contabilidad complicada) y abre vector de spam, por lo que muchos nodos lo desactivan.

Para casos que necesitan reutilización real y garantías más fuertes, **BOLT 12 offers** está reemplazando progresivamente a ambos.

Bloque 5

## Force-close y cierre de la sesión

Observamos qué ocurre cuando uno de los lados no puede (o no quiere) cerrar el canal cooperativamente y recurre al broadcast unilateral de su última commitment transaction.

1.  Añade dos nuevos nodos LND, **Frank** y **Grace**, al network. Añade fondos a Frank.
2.  Frank abre un canal hacia Grace de **5 000 000 sats**. Polar se encargará de minar 6 bloques para confirmarlo.
3.  Frank envía un pago de **2 000 000 sats** a Grace. Desde la interfaz: Grace crea una invoice por esa cantidad en su pestaña _Actions → Create Invoice_, copia el `payment_request` y Frank lo paga desde su pestaña _Actions → Pay Invoice_. Así, cuando se produzca el force-close, la commitment transaction tendrá valor real a ambos lados del canal.
4.  Obtén el `funding_txid` y el `output_index` del canal. Lanza en Frank:
    
    ```
    frank$ lncli listchannels
    ```
    
    Busca el campo `channel_point`. Tiene el formato `<funding_txid>:<output_index>` — la parte antes de los dos puntos es el `funding_txid` y el número después es el `output_index`.
5.  Con esos datos, Frank fuerza el cierre del canal con Grace:
    
    ```
    frank$ lncli closechannel \
      --force \
      --funding_txid <txid> \
      --output_index <idx>
    ```
    
    Este comando **no** genera una cooperative close: Frank broadcastea unilateralmente su última **commitment transaction** a la mempool de Bitcoin Core, sin minarla.
6.  Localiza el `txid` de la commitment transaction consultando el estado del cierre pendiente en Frank:
    
    ```
    frank$ lncli pendingchannels
    ```
    
    La commitment todavía no está minada, así que el canal aparece dentro de `waiting_close_channels`. Ahí tienes el campo `closing_txid`: ese es el hash de la commitment transaction que Frank acaba de publicar a la mempool. Observa también `limbo_balance`: son los sats de Frank "en el aire" mientras dure el cierre.
7.  Decodifica la commitment transaction desde el nodo Bitcoin Core. En Polar, pulsa sobre el nodo **bitcoind**, abre la pestaña _Actions_ y lanza un terminal de `bitcoin-cli`. Consulta la tx con verbosidad alta:
    
    ```
    bitcoind$ bitcoin-cli getrawtransaction <closing_txid> 2
    ```
    
    Observa el array `vout`: verás **cuatro outputs**, todos de tipo `witness_v0_scripthash` (P2WSH):
    
    *   **Dos outputs de 330 sats** — los _anchor outputs_, uno por peer, que permiten acelerar la confirmación si hiciera falta.
    *   **Un output de ~2 000 000 sats** — corresponde al saldo de Grace (`to_remote`). En el formato de canal moderno no tiene timelock significativo: Grace podrá gastarlo prácticamente de inmediato.
    *   **Un output de ~3 000 000 sats** (menos la commitment fee y los dos anchors, que los paga Frank por ser el iniciador) — corresponde al saldo de Frank (`to_local`). Está bloqueado por un script con `OP_CHECKSEQUENCEVERIFY` y un **timelock relativo**.
    
    A este nivel **no puedes ver las instrucciones del script**: P2WSH solo expone el hash del script. Por eso no distingues `to_local` de `to_remote` mirando el output en sí — lo deduces por el **valor** (quién recibió qué balance) y porque solo el output del iniciador lleva el `CheckSequenceVerify`. El script con el `OP_CHECKSEQUENCEVERIFY` únicamente se revelará cuando Frank intente gastar ese output, al final del timelock relativo.
    
    Fíjate también en los campos `locktime` y `sequence` de la transacción: verás valores aparentemente aleatorios como `542485917` o `2153782885`. No son errores — son el _obscured commitment number_ (BOLT 3): un número de revisión del canal ofuscado dentro de estos campos, que solo los dos peers pueden desenmascarar.
    
8.  Mina **1 bloque** con _Quick Mine_ para confirmar la commitment transaction. Vuelve a ejecutar:
    
    ```
    frank$ lncli pendingchannels
    ```
    
    El canal ya no está en `waiting_close_channels`, sino en **`pending_force_closing_channels`**. Ahora aparecen los campos que antes no salían: `blocks_til_maturity` (bloques que faltan para que venza el `CheckSequenceVerify`), `maturity_height` (altura a la que se desbloquean los fondos), `recovered_balance` y el detalle de los pending HTLCs si los hubiera. `limbo_balance` sigue marcando los sats de Frank retenidos por el timelock.
9.  Comprueba que Frank no puede mover todavía sus fondos — están bloqueados hasta que venza el `CheckSequenceVerify`. Ahora hay que minar los **N bloques** restantes (donde N = `blocks_til_maturity`). Como el valor suele ser alto (144, 600, etc.), ir pulsando _Quick Mine_ uno por uno es inviable. En su lugar, usa el terminal de **bitcoind** en Polar y lanza un solo comando para minar todos los bloques de golpe:
    
    ```
    bitcoind$ bitcoin-cli -generate <N>
    ```
    
    Sustituye `<N>` por el valor de `blocks_til_maturity`. El comando `-generate` es un atajo de `bitcoin-cli` que crea una nueva dirección del wallet y mina los N bloques pagándose las recompensas a sí mismo, todo en una sola llamada. Tarda apenas unos segundos incluso para 600 bloques.
    
    Después verifica que Frank ha recuperado sus sats on-chain:
    
    ```
    frank$ lncli walletbalance
    frank$ lncli pendingchannels
    ```
    
    El canal ya no debería aparecer en ninguna lista de canales pendientes y el `confirmed_balance` de Frank habrá aumentado.

Conexión teórica

El timelock en el output propio existe para dar una _ventana de contestación_ al otro nodo. Si Frank hubiera publicado un estado _antiguo_ (intentando trampa), Grace tendría tiempo de publicar la _revocation key_ durante esos N bloques y quedarse con los fondos de Frank. Es el núcleo del _Poon-Dryja fairness protocol_ visto en la slide 5.

Entregable

## Qué tenéis que entregar

Formato

Subid un único archivo `lightning-lab-<apellido>.zip`: la **network exportada desde Polar** al final del laboratorio.

Desde Polar: menú _File → Export Network_. Polar genera un `.zip` con el estado completo de la red (nodos, canales, balances, datos on-chain). Ese es el archivo que subís tal cual, renombrándolo con vuestro apellido.