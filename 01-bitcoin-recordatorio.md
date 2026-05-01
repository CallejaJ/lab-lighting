         

←→ Navegar

Módulo 05 · Bitcoin

Sesión 1 / Teoría

Recordatorioe

# ¿Qué es Bitcoin?

Un breve repaso a los fundamentos de la primera blockchain descentralizada

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

01 · Origen

01 · Origen y esencia

## Dinero electrónico entre pares.

Lo que hace aceptable a una criptomoneda

1.  ¿Puedo confiar en que este dinero es auténtico y no está falsificado?
2.  ¿Puedo confiar en que solo puede gastarse una vez? _(el problema del «doble gasto»)_
3.  ¿Puedo estar seguro de que nadie más podrá reclamarlo como suyo en lugar de mío?

— A. Antonopoulos, _Mastering Bitcoin_ · cap. 1

2008 Whitepaper

2009 Red Bitcoin

21MBTC Suministro finito

~10min Ritmo de bloques

*   **Satoshi Nakamoto (2008)** publica un whitepaper de 9 páginas sobre dinero electrónico P2P.
*   **Red descentralizada** sin autoridad central, sin intermediarios y sin permisos para participar.
*   **Resuelve el doble gasto** en entornos sin confianza mediante consenso por PoW.
*   **Unidad mínima**: 1 BTC = 100 000 000 satoshis; emisión programada hasta alcanzar 21 millones (en teoría).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Bitcoin

02 · Criptografía

02 · Cimientos criptográficos

## Propiedad basada en claves

«Poseer bitcoins equivale a poseer la clave privada asociada a la dirección» Esa clave autoriza a gastar las **UTXOs** (_Unspent Transaction Outputs_) vinculadas a la dirección — lo que llamamos «saldo» es simplemente la suma de esas UTXOs.

*   **Criptografía asimétrica** sobre la curva elíptica secp256k1.
*   **Derivación unidireccional**: clave privada → clave pública. Lo contrario es computacionalmente inviable.
*   **SHA-256** como función hash: compromete datos, construye hashes de bloques y direcciones.
*   **Firma digital ECDSA**: demuestra autoría sin revelar la clave privada; cualquiera puede verificarla con la clave pública.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

03 · Direcciones

03 · Direcciones y transacciones

## Tres formatos, un mismo propósito.

Legacy P2PKH · 1… `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` Pay-to-PubKey-Hash — el formato clásico basado en el hash de la clave pública.

Script P2SH · 3… `3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy` Pay-to-Script-Hash — habilita multi-firma, time-locks y otras condiciones.

SegWit Bech32 · bc1… `bc1qar0srrr7xfkvy5l643lydnw9re59gtzzwf5mdq` Nativo SegWit — tarifas más bajas, mejor detección de errores, estándar actual.

*   **Dirección** = derivada de la clave pública mediante SHA-256 + RIPEMD-160 y codificada (Base58 o Bech32).
*   **Transacción** = conjunto de inputs firmados con la clave privada + outputs que definen los nuevos propietarios.
*   **Fee** = inputs − outputs; incentivo económico que los mineros cobran por incluir la transacción en un bloque.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Bitcoin

04 · Blockchain

04 · Cadena de bloques

## Bloques enlazados por hash.

BlockN−1

prev\_hash**…0x7a2c**

merkle**…0x9f3e**

nonce**412 877**

hash →

BlockN

prev\_hash**…0xc41e**

merkle**…0x1d88**

nonce**2 901 133**

hash →

BlockN+1

prev\_hash**…0xe502**

merkle**pending**

nonce**?**

*   **Encadenamiento por hash**: cada bloque referencia al anterior, haciendo cualquier modificación pasada visiblemente incoherente.
*   **Merkle root**: compromete todas las transacciones del bloque en un único hash; verificación eficiente en O(log N).
*   **Nonce + PoW**: los mineros prueban valores hasta que el hash cumpla la dificultad objetivo.
*   **Ritmo**: un bloque cada ~10 minutos; reajuste automático de dificultad cada 2 016 bloques.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Bitcoin

05 · Transacciones

05 · Transacciones y UTXO

## Bitcoin es un registro, no un objeto.

Analogía · Registro de la Propiedad

Los bitcoins **no existen físicamente ni como datos digitales**. Transferir bitcoin se parece a transferir una vivienda: cuando le pasas tu casa a otra persona, _no coges la casa y la mueves a otro sitio_ — eso no tiene sentido.

En su lugar, un **registro público** (la blockchain) anota que la propiedad ahora pertenece a otra persona. «Tener bitcoins» significa, en realidad, **controlar las UTXOs que el registro te atribuye**.

Ejemplo · Transacción con fees

Inputs · UTXOs gastadas

bc1q…a3x0.60 BTC

bc1q…7fe0.42 BTC

Σ in = **1.02 BTC**

tx

Outputs · UTXOs nuevas

bc1q…b2c · pago0.80 BTC

bc1q…9cd · cambio0.21 BTC

Σ out = **1.01 BTC**

Fee Σ in − Σ out = **0.01 BTC** → la diferencia no se declara; emerge como propina implícita que cobra el minero que incluya la transacción en su bloque.

*   **UTXO** (_Unspent Transaction Output_) = cantidad de bitcoin con una condición de gasto; sólo se puede consumir **entera**.
*   **Inputs** = referencias a UTXOs anteriores que se gastan, autorizadas con la firma de la clave privada correspondiente.
*   **Outputs** = nuevas UTXOs que se crean (pago + cambio); todo sobrante vuelve al emisor como una UTXO de «cambio».
*   **Fee implícita**: Σ inputs − Σ outputs. Incentiva al minero a priorizar la transacción (ver _Mastering Bitcoin_, cap. 6).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Bitcoin

06 · La red Bitcoin

06 · La red Bitcoin

## Una red P2P plana y abierta.

La red · a vista de pájaro

La «red Bitcoin» es el **conjunto de nodos** que ejecutan el protocolo P2P Bitcoin e intercambian bloques y transacciones mediante _gossip_. **No existen servidores centrales, jerarquías ni intermediarios**.

*   **~10 000 nodos públicos** escuchando en la red principal.
*   **Descubrimiento**: DNS seeds + caché local + petición a pares conocidos.
*   **Handshake**, **inventario**, **getdata**, **block**, **tx**, **headers**… + _heartbeat_.
*   **BIP 324**: comunicación cifrada (no autenticada) entre pares.

Anatomía · 4 módulos funcionales

W Wallet Gestiona claves, firma transacciones.

M Miner Compite en la PoW para crear bloques.

B Blockchain Copia completa e índices locales.

N Network Routing Habla el protocolo P2P y propaga.

El **tipo** de nodo se define por **qué módulos tiene activos**: cada combinación da un perfil distinto.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Bitcoin

07 · Tipos de nodos

07 · Tipos de nodos

## Cuatro perfiles, cuatro compromisos.

Full Node Bitcoin Core · «Satoshi Client» Módulos: **W · M\* · B · N** (\*minero desactivado por defecto) **Valida cada bloque y transacción** aplicando todas las reglas de consenso. Implementación de referencia (C++, desde 2009). Independencia y privacidad máximas; >95 % de los nodos públicos lo ejecutan.

Archive Node Full node que guarda todo el histórico Módulos: **B · N** (sin wallet, sin minado) Mantiene la **blockchain completa** sin podarla (>700 GB). Sirve datos a clientes SPV, exploradores de bloques, exchanges y procesadores de pago. Actúa como **edge router** del ecosistema.

Lightweight (SPV) Cliente ligero · móviles, wallets Módulos: **W · N** (sin blockchain) Solo descarga **cabeceras de bloques** (~80 B cada una) y usa _Simplified Payment Verification_. Verifica PoW y pruebas Merkle; **confía en nodos completos** para los datos. Menos recursos, menos seguridad.

Third-Party API Wallet delegada · REST / WebSocket Módulos: **W** (sin N, sin B) No habla el protocolo P2P: consulta un servicio externo (Electrum, Esplora, APIs de exchanges…). Saldos, historial y _broadcast_ se **delegan por completo**. Máxima comodidad, máxima dependencia.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Bitcoin

08 · Nodos ligeros y SPV

08 · Nodos ligeros y SPV

## SPV: verificación simplificada.

Cómo funciona SPV

Un nodo ligero verifica **por profundidad**: si una transacción aparece en un bloque «enterrado» bajo suficiente PoW, se asume válida _sin reconstruir UTXOs_.

*   Descarga **solo cabeceras** (~80 B / bloque) vía mensaje `getheaders`.
*   Verifica la inclusión de una tx con una **prueba Merkle** desde el nodo al root.
*   **Limitación**: puede probar que una tx _existe_, pero no que _no existe_ — vulnerable a doble gasto.

**Filtros** para descubrir tus txs sin revelar direcciones al peer: _Bloom Filters_ (BIP 37, server-side) y _Compact Block Filters_ (BIP 157/158, client-side).

⚠ Riesgo Sybil attack **Un Sybil attack** consiste en crear **muchas identidades falsas** (nodos controlados por el mismo atacante) para _rodear_ a la víctima en la red. Si todos sus pares son hostiles, ve una realidad fabricada. Los SPV son **especialmente sensibles**: sin cadena local no pueden verificar por sí mismos, así que **dependen de sus pares**. También son vulnerables a _network partitioning_, DoS y, en última instancia, a doble gasto. **Defensa**: conectar a muchos pares aleatorios y, si es posible, apuntar al **propio nodo completo**.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Bitcoin

09 · Relay networks

09 · Propagación y relay networks

## Minimizar la latencia entre mineros.

El problema · block-finding race

Cuando un minero encuentra un bloque, los demás siguen trabajando sobre el anterior hasta que lo reciben. **Esos segundos de retraso favorecen a los grandes mineros** y empujan hacia la centralización. La red pública ya optimiza con _Compact Block Relay_ (BIP 152), pero **algunos actores van más allá con redes privadas**.

2015 Bitcoin Relay Network Matt Corallo · VPSes globales Red privada de servidores virtuales estratégicamente distribuidos para conectar **la mayoría de mineros y pools** con muy baja latencia.

2016 FIBRE Fast Internet Bitcoin Relay Engine Sucesor del BRN. **UDP + Forward Error Correction** + _compact block_: reduce drásticamente la latencia y tolera pérdidas sin re-peticiones.

La latencia es **crítica** en minería competitiva → en las siguientes transparencias nos centraremos en **minado** y proof-of-work.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

10 · Minado & consenso

10 · Minado = seguridad + consenso

## Consenso emergente, sin autoridad central.

La función real del minado

El propósito del minado **no es crear bitcoins**. Eso es el _incentivo_. El fin último es **asegurar el sistema**: validar transacciones y lograr que **miles de nodos independientes** converjan en la misma verdad sobre _quién posee qué_, sin ningún banco central ni cámara de compensación.

01 / Verificar Cada tx, cada nodo Todos los full nodes validan **independientemente** cada transacción según una lista exhaustiva de reglas.

02 / Agregar PoW + bloques Los mineros empaquetan txs en un bloque candidato y **demuestran cómputo** resolviendo el _proof of work_.

03 / Validar El bloque, por todos Cada nodo verifica el nuevo bloque independientemente y lo encadena al anterior si cumple las reglas.

04 / Elegir Más PoW acumulado Cada nodo selecciona la cadena con **mayor trabajo acumulado**. Esa es, por definición, la verdad.

**Consenso** no se vota: **emerge** de la interacción asíncrona de nodos independientes que siguen reglas simples.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Bitcoin

11 · La mempool

11 · La mempool

## El limbo de las tx sin confirmar.

Memory pool · mempool

Casi todos los nodos mantienen una **lista temporal en memoria** con las transacciones que han sido _validadas_ y _propagadas_ por la red pero que **todavía no están en ningún bloque**. A esa lista se la llama **mempool**.

Cuando una tx llega nueva, el nodo la **valida**, la guarda en su mempool y la **retransmite** (_relay_) a sus pares. Los mineros eligen **desde la mempool** qué incluyen en su próximo bloque candidato.

~300MB Tamaño por defecto

Local A cada nodo

RAM Donde vive

*   **Mercado de fees**: si la mempool se llena, el nodo expulsa las tx con **feerate más bajo**. Así emerge el precio por byte en vivo.
*   **Perspectiva local**: cada nodo tiene su propia mempool; pueden diferir entre sí según _policy_, uptime y red.
*   **Orphan pool**: tx cuyo «padre» aún no ha llegado se guardan aparte hasta que aparezca, momento en que se promueven a la mempool.
*   **Ciclo**: validar → mempool → relay → minada en bloque → expulsada. También se expulsan por _expiración_ (~2 semanas).

La mempool es la **sala de espera** de Bitcoin — y el termómetro más honesto del estado de la red. Sin ella no habría mercado de fees ni propagación eficiente.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Bitcoin

12 · Confirmaciones & doble gasto

12 · ¿Cuándo está "confirmada" una tx?

## Cada bloque es otra capa de seguridad.

Confirmación

Una transacción se considera **confirmada** cuando entra en un bloque minado y pasa a formar parte de la blockchain. A partir de ahí, cada bloque posterior añade una _confirmación adicional_ — y cuanta más PoW se apile encima, **más inmutable** se vuelve.

0 En mempool No confirmada · reemplazable

1 Primer bloque Café, propinas

3 Baja exposición Intercambios casuales

6 Regla estándar ~1 hora · defecto

100 Coinbase maturity Recompensa gastable

144 Alto valor ~24 h · bienes caros

Cómo se evita el double spending

Dentro de una misma cadena, las transacciones tienen un **orden topológico**: solo son válidas si gastan salidas de txs _anteriores_ y si **ninguna otra** ha gastado ya esas mismas salidas. Imposible gastar dos veces el mismo UTXO.

Si un atacante intenta reescribir la historia necesita **rehacer el PoW** de todos los bloques desde la tx objetivo — inviable a partir de ~6 confirmaciones salvo con un ataque del **51%**.

⚠ Doble gasto Ataque del 51% Un minero (o coalición) con **mayoría del hash rate** puede forkear la cadena y _reemplazar_ una tx ya confirmada por otra que devuelve el UTXO al atacante. Solo es rentable sobre txs propias y requiere un coste energético enorme. **Defensa**: esperar suficientes confirmaciones antes de entregar bienes de alto valor.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Bitcoin

13 · Recompensa & Proof of Work

13 · Incentivos + Proof of Work

## Coinbase = subsidy + fees.

Bloque nuevo Subsidy 3,125 BTC (2024+) Bitcoins **acuñados de la nada** en cada bloque. Empezó en **50 BTC** y se _halvea_ cada 210 000 bloques (~4 años). En 2140 será cero.

+

De cada tx Transaction fees Σ(inputs) − Σ(outputs) El minero se queda la _diferencia_ entre inputs y outputs de cada transacción incluida. Con el tiempo **serán la única fuente** de recompensa.

\=

Primera tx del bloque Coinbase transaction Sin inputs reales Tx especial que **no gasta UTXOs**: tiene un _coinbase input_ implícito. Paga al minero y debe esperar **100 confirmaciones** antes de poder gastarse.

Proof of Work · SHA-256 doble

H(merkle\_root, prev\_hash, X) ≤ target

El minero varía **X** (nonce de 32 bits + extra-nonce en el coinbase + timestamp) hasta que el hash del header **cae bajo el target**. Es una lotería: billones de intentos por segundo, ganador ≈ cada 10 min.

Verificar una solución es **instantáneo**; encontrarla cuesta _energía real_. Ése es el coste que asegura la cadena.

Cada cuántos bloques 2 016 Cada ~2 semanas todos los nodos **reajustan** el target de forma independiente, con la misma fórmula.

Fórmula de retarget new\_target = old\_target × (tiempo real 2016 bloques / 20 160 min) Si se minaron **más rápido** de 10 min/bloque → el target baja (más difícil). Si más lento → sube (más fácil). Ajuste máximo ×4 por período.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Bitcoin

14 · Mining pools & Stratum

14 · Mining pools

## Minar en solitario es una lotería.

Cómo funciona un pool Cooperar para cobrar a menudo Muchos mineros conectan su hardware a un **servidor pool**. El pool arma bloques candidato, distribuye trabajo, y cuando _alguien_ del pool encuentra la solución, el premio se reparte **proporcionalmente al trabajo aportado**.

*   **Primera pool**: Slushpool, diciembre 2010.
*   El pool cobra una comisión típica **< 2%**.
*   Un minero pequeño pasa de "un bloque cada 20 años" a **ingresos diarios** pequeños pero continuos.

Shares · cómo medir el trabajo Un share = hash bajo un target fácil El pool fija un **target más permisivo** (≥ 1 000× más fácil que el de la red). Cada vez que un minero encuentra un hash bajo ese target gana un _share_, que **prueba** que ha hecho trabajo real.

target red   0x000000000000003A30C0…0

target share 0x00000000003A30C0…0

**Reparto**: _PPS_ (pago fijo por share), _PPLNS_ (últimos N shares), _FPPS_ (PPS + incluye fees). Cada estrategia traslada distinto riesgo entre pool y minero.

Protocolo Stratum TCP + JSON-RPC · creado por Slush **No es un BIP**. El minero _no_ necesita un nodo completo: se conecta al pool, recibe **templates de bloque** y devuelve shares. **Stratum v2** añade cifrado y permite que cada minero escoja sus propias txs.

Mineroregistro (user/pass)Pool MinerosubscribePool Mineronotify · block templatePool Mineroset\_difficultyPool Minerosubmit · "share"Pool

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Bitcoin

15 · Cambiando las reglas · Hard Forks

15 · Hard Forks

## Cuando las reglas de consenso se rompen.

Hard fork Cambio **incompatible hacia atrás**. Alguien introduce una regla nueva que hace **válidos** bloques o txs que antes eran inválidos (o al revés). Los nodos que **no actualicen** rechazarán los nuevos bloques: la red se _parte en dos cadenas_ que evolucionan por separado.

*   Requiere **coordinación casi unánime**: mineros, wallets, exchanges y nodos.
*   Una vez separadas, **no convergen**: aparecen _dos criptomonedas_.
*   Causa habitual: bug en las reglas, o cambio deliberado (tamaño de bloque, formato de firma, etc.).

Caso más famoso · Ago 2017 Bitcoin Cash (BCH) Disputa por el tamaño de bloque (1 MB). Un grupo sube el límite a 8 MB y fuerza un fork en el bloque **478 558**. Nace BCH. Después **BCH se vuelve a forkear** en Bitcoin SV (2018).

Otros casos Bitcoin Gold (2017), Bitcoin XT, Bitcoin Classic Propuestas que, o no lograron adopción (XT, Classic), o derivaron en su propia cadena minoritaria. Ilustran lo **difícil** que es mover Bitcoin por hard fork.

Incidente accidental · Mar 2013 Bug Core 0.7 → 0.8 Un cambio no intencionado en BerkeleyDB provocó un fork involuntario durante 6 bloques. Se resolvió volviendo a la versión antigua.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Bitcoin

16 · Cambiando las reglas · Soft Forks

16 · Soft Forks

## Reglas que se estrechan, compatibles hacia atrás.

Soft fork Cambio **forward-compatible**. Se introducen reglas **más restrictivas**: todo lo válido bajo la nueva regla sigue siendo válido bajo la antigua. Los nodos sin actualizar **no notan nada** y siguen en consenso con el resto. _Técnicamente no es un fork_.

*   Solo pueden **restringir** lo válido, nunca ampliarlo (o sería un hard fork).
*   Activación por **señalización de mineros**: BIP34, BIP9, BIP8, speedy trial.
*   Críticas: deuda técnica, validación "ciega" en nodos viejos, casi **irreversibles**.

BIP 16 · Abr 2012 P2SH · Pay-to-Script-Hash Permite pagar a un **hash de script** (multifirma, contratos) en vez de a una clave pública. Origen de las direcciones que empiezan por **3…**.

BIP 141/143/147 · Ago 2017 SegWit · Segregated Witness Separa las firmas ("witness") del resto de la tx: arregla la maleabilidad, aumenta la capacidad efectiva del bloque y habilita **Lightning**. Direcciones **bc1q…**.

BIP 340/341/342 · Nov 2021 Taproot Firmas **Schnorr** + MAST: mejora privacidad y coste de contratos complejos. Direcciones **bc1p…**. Activado con _speedy trial_.

En Bitcoin, las reglas cambian **lentamente y con consenso**: los hard forks dividen la red, los soft forks la hacen evolucionar.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17