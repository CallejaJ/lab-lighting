         

←→ Navegar

Módulo 05 · Lightning Network

Sesión 3 / Teoría

Segunda capa

# Lightning Network

Pagos instantáneos, privados, escalables y de bajo coste sobre la Bitcoin Network.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Lightning Network

01 · Escalabilidad

01 · El reto

## Bitcoin es seguro, pero lento.

Confirmar cada café en la cadena principal es caro, lento y poco privado. La descentralización y la seguridad se pagan en throughput.

~10Tx / segundo

~10minPor bloque

1–4MBPeso bloque

6×conf.≈ 1 hora

*   **Cuello de botella on-chain**: cada tx consume espacio de bloque y fee. Con congestión, pagos de unos euros dejan de tener sentido.
*   **Latencia de confirmación**: una tx sin confirmar puede ser reorganizada. Esperar 10 minutos a que se confirme el bloque no hace que la transacción sea segura.
*   **Privacidad limitada**: cada transacción queda pública en la cadena para siempre.
*   **No válido para micropagos**: pagar 50 sats en on-chain cuesta más fees que el propio pago.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Lightning Network

02 · Segunda capa

02 · Panorama de soluciones L2

## Construir sobre Bitcoin sin tocarlo.

01 · ACTIVOS RGB

Emite y transfiere **activos** (stablecoins, tokens, NFTs) con _client-side validation_. Los datos viven _off-chain_; la L1 sólo graba un hash-commitment incrustado en una UTXO (técnica _Pay-to-Contract_).

**Ventaja:** máxima privacidad — la cadena no ve nada del activo. **Reto:** emisor y receptor deben conservar la historia completa.

02 · ACTIVOS Taproot Assets

Propuesta de Lightning Labs. Emite **activos** anclados en outputs Taproot mediante _Merkle trees_. Pueden enrutarse por Lightning → stablecoins a velocidad LN.

**Ventaja:** interoperable con Lightning vía LND. **Caso típico:** Tether (USDT) pagable como sats.

03 · PAGOS Lightning Network

Red de **canales de pago** enrutados con HTLCs que permite enviar bitcoin entre cualquier par de nodos de forma **instantánea y barata**.

**Ventaja:** miles de tx/s efectivas, fees de sats, finalidad en < 1 segundo. **Madurez:** la L2 más adoptada.

¿Qué comparten?

No cambian el protocolo base. Firman operaciones _off-chain_ y, si hay conflicto, recurren a la L1 como tribunal. Herencia de **seguridad** gracias a Bitcoin.

¿En qué se diferencian?

Lightning resuelve **pagos**. RGB y Taproot Assets resuelven **emisión y transferencia de activos**. Se complementan, no compiten.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Lightning Network

03 · Canales de pago

03 · Canales de pago · La idea clave

## Un canal de pago es un 2-of-2 multisig con saldo móvil.

Un **canal de pago** es un acuerdo financiero bilateral entre dos nodos: bloquean fondos en la cadena y después intercambian _off-chain_ actualizaciones firmadas del saldo, liquidables en cualquier momento. Es el ladrillo sobre el que se construye toda Lightning Network.

Ciclo de vida del canal

*   **Apertura on-chain**: Alice y Bob publican una _funding transaction_ que envía N BTC a un output 2-de-2 (multifirma). Esa UTXO es el canal.
*   **Intercambio off-chain**: firman una _commitment transaction_ cada vez que el saldo cambia. Nunca se difunden en la red — sólo existen entre ambos.
*   **Cierre on-chain**: cualquiera puede publicar el último estado firmado. La UTXO se gasta y los saldos finales van a cada dueño.

Seguridad

Si alguien intenta hacer trampa publicando un estado antiguo, el otro puede reclamar **todo el dinero del canal** (_fairness protocol_).

ON-CHAIN

2 transacciones: abrir + cerrar

OFF-CHAIN

Miles de pagos entre medias

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Lightning Network

04 · Anatomía de un canal

04 · Ciclo de vida

## Apertura · Actualización · Cierre.

**Ejemplo simple ·** Alice pasa cada mañana por la cafetería de Bob a por un café. En lugar de pagar on-chain cada vez, abren un canal Lightning y liquidan todos los cafés con una única transacción al final.

### 01 · APERTURA
**funding tx (on-chain) → 2-of-2 multisig ALICE BOB 🔑 🔑**
- **UTXO capacidad:** 5 000 000 sats.
- Alice deposita 5M sats; el output queda bajo el control conjunto de ambas claves.
- **Coste:** 1 transacción on-chain.

### 02 · ACTUALIZACIÓN
**N × commit_tx (off-chain) ALICE BOB ☕**
- **commit_tx_n:** Alice 4.5M · Bob 500k.
- **Flujo:** 1. Firma Alice → 2. Bob entrega ☕ → 3. Firma Bob.
- Cada `commit_tx` redistribuye los saldos del canal. Con la tx firmada por Alice, Bob se asegura de poder cobrar al cierre del canal.
- **Coste:** 0 transacciones on-chain.

### 03 · CIERRE
**settlement tx (on-chain) · ambos firman ALICE BOB**
- **Resultado:** Alice 4 500 000 sats | Bob 500 000 sats.
- **Settlement:** Tras muchos cafés, ambos acuerdan cerrar. La settlement tx liquida los saldos on-chain.
- **Coste:** 1 transacción on-chain.

En todo el ciclo sólo **2 transacciones tocan la blockchain**: funding tx y settlement tx.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Lightning Network

05 · Commitment & revocación

05 · Fairness protocol

## ¿Por qué no se puede hacer trampa?

Si Alice publica un _commitment_ viejo que le favorece, Bob puede castigarla y llevarse **todo** el saldo del canal.

*   **Commitment transaction**: cada vez que el saldo cambia, se firma una nueva que refleja los saldos actuales. Si Alice la publica, su output queda _time-locked_ durante un periodo; ese retraso es la ventana en la que Bob puede detectar una commitment antigua y reaccionar antes de que Alice cobre.
*   **Revocation key**: al firmar la siguiente commitment, cada parte _revela_ una clave que revoca la anterior. Ambos guardan pruebas para castigar.
*   **Justicia criptográfica**: si Alice publica una commitment antigua, esa tx reparte el canal en dos outputs. Bob gasta el suyo al instante (ya estaba firmado a su favor) y, con la revocation key que Alice le reveló al sustituir ese estado, barre también el output de Alice antes de que venza su time-lock. Bob se queda con **los dos outputs**, es decir, con el 100% del canal.
*   **Watchtowers**: servicios que observan la cadena por ti; si estás offline, ellos publican la tx de castigo cuando detectan una commitment vieja.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Lightning Network

06 · Límites de un canal aislado

06 · El canal aislado

## Dos partes, dos problemas.

Un canal bilateral resuelve el intercambio repetido entre dos personas… _siempre que_ ambas colaboren y estén atentas. Fuera de ese escenario ideal aparecen limitaciones que frenan su uso real.

01 · DISPONIBILIDAD Si la contraparte desaparece

Para cerrar cooperativamente hace falta la firma de los dos. Si Bob se desconecta, Alice sólo puede hacer un **cierre unilateral** publicando su última commitment.

Ese output queda _time-locked_: sus fondos permanecen bloqueados durante todo el _CSV delay_ antes de que pueda gastarlos.

02 · VIGILANCIA Hay que estar mirando

El fairness protocol sólo castiga si alguien **detecta** la commitment antigua dentro del time-lock. Si nadie observa la cadena, el tramposo cobra sin consecuencias.

En la práctica obliga a tener el nodo online 24/7 o a delegar la vigilancia en _watchtowers_ de terceros.

03 · CAPITAL Fondos inmovilizados

La capacidad del canal vive en un UTXO 2-of-2. Mientras el canal esté abierto, ese capital no puede usarse para nada más.

Cuanto mayor sea el importe que quiera mover Alice, más dinero tiene que dejar encerrado por adelantado.

04 · RELACIÓN 1-A-1 Sólo sirve con esa persona

El canal entre Alice y Bob sólo permite pagarle **a Bob**. Para pagar a Carol hace falta abrir otro canal, con sus fees on-chain y su propio capital bloqueado.

Esta limitación es la que empujará hacia el **enrutado** a través de terceros, la idea clave de Lightning.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Lightning Network

07 · Los canales directos no bastan

07 · El límite de los canales bilaterales

## Un canal por pareja: inviable.

N = 6 15 canales

Grafo completo con N = 6 nodos

*   **Coste on-chain prohibitivo**: abrir un canal entre cada par requiere _N·(N−1)/2_ transacciones on-chain. Con 1M usuarios: **500 000 M** canales.
*   **Capital bloqueado**: cada canal inmoviliza fondos. Un usuario no puede fondear un canal con todo el mundo.
*   **Mantenimiento**: cada canal requiere vigilancia, firmas, storage de commits y posibles cierres.
*   **La solución**: enrutar pagos a través de canales ya existentes, como los paquetes en Internet.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Lightning Network

08 · HTLCs

08 · Hash Time-Locked Contracts

## El pegamento del enrutado.

Un **HTLC** (_Hash Time-Locked Contract_) es un contrato que paga al receptor _si_ revela un secreto antes de un plazo; en caso contrario, devuelve los fondos al remitente.

*   **Atomicidad**: o todos los saltos del enrutado cobran, o ninguno. **R** es el secreto que tiene que atravesar el camino completo; hasta que aparece, ningún nodo puede cobrar.
*   **Time-lock decreciente**: cada salto tiene un plazo un poco menor que el anterior, de modo que si el pago falla, cada nodo recupera sus fondos a tiempo.
*   **Onion routing**: el remitente cifra la ruta en capas, como una cebolla. Cada nodo intermedio descifra sólo _su_ capa, descubre a qué peer reenviar el pago y pasa el resto todavía cifrado. Ningún nodo conoce el camino completo: sólo ve a su predecesor y a su sucesor, nunca al remitente ni al destinatario final.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Lightning Network

09 · ¿Qué es Lightning Network?

09 · Lightning Network

## Una red de canales enrutados.

Lightning Network es un protocolo P2P que transmite pagos en bitcoins a través de una red de canales de pago, usando enrutado en cebolla, HTLCs y técnicas de _fair exchange_ criptográficas.

2016Paper Poon-Dryja

2018Mainnet live

~5kBTCCapacidad pública

~17kNodos activos

*   **Capas complementarias**: LN no sustituye a Bitcoin. Depende de él como ancla de seguridad y liquidación.
*   **BOLTs**: especificación abierta y mantenida en GitHub (_Basis Of Lightning Technology_). Implementaciones: LND, Core Lightning, Eclair, LDK.
*   **Propiedad clave**: _trust-minimized_. El enrutado no requiere confiar en los nodos intermedios para la custodia.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Lightning Network

10 · Beneficios de Lightning

10 · Qué se gana

## Instantáneo, barato y privado.

VELOCIDAD Sub-segundo

Los pagos se liquidan en milisegundos, no en minutos. Perfecto para TPV, POS y experiencias interactivas.

COSTE Fracción de sat

Las fees de enrutado son proporcionales al importe. Micropagos viables por primera vez.

PRIVACIDAD Onion routing

Los pagos viajan usando onion routing. Ningún intermediario conoce la ruta completa, ni quién paga a quién.

CAPACIDAD Millones de tx/s

No hay bloques: mientras haya liquidez en los canales, la red escala linealmente con nodos y capital.

NUEVO MODELO Micropagos viables

Pagar por KB de streaming, por segundo de audio, por palabra de una API. Modelos de negocio imposibles en L1.

INTERNACIONAL Remesas en minutos

Transferencias globales sin bancos, sin KYC intermedio, sin días de espera. Útil en entornos con banca frágil.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Lightning Network

11 · Capacidad y liquidez

11 · Inbound & outbound

## Dos depósitos en un canal.

«La capacidad de un canal es la suma de los saldos de ambos lados. Lo que puedes _enviar_ es tu saldo local (outbound); lo que puedes _recibir_ es el saldo remoto (inbound).»

Canal recién abierto · 5 000 000 sats

Tras pagar 2M sats

Canal equilibrado

*   **Outbound**: sats tuyos en tu lado del canal. Se gastan al enviar.
*   **Inbound**: sats del otro lado. Determina cuánto puedes recibir.
*   **Desbalance**: canales sin inbound no pueden recibir pagos. Hay que rebalancear (circular payments, submarine swaps, LSP).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Lightning Network

12 · Ejemplo completo

12 · Ejemplo completo

## Alice paga 1 BTC a Eric a través de 3 intermediarios.

Invoice: H = hash (R) HTLC 1.003 · 10 bloques HTLC 1.002 · 9 bloques HTLC 1.001 · 8 bloques HTLC 1.000 · 7 bloques Revelar R · cobra 1 R · cobra 1.001 R · cobra 1.002 R · cobra 1.003 A Alice B Bob C Carol D Diana E Eric

Canal Alice ↔ Bob

Alice · 2 BTCBob · 2 BTC

Canal Bob ↔ Carol

Bob · 2 BTCCarol · 2 BTC

Canal Carol ↔ Diana

Carol · 2 BTCDiana · 2 BTC

Canal Diana ↔ Eric

Diana · 2 BTCEric · 2 BTC

01 Configuración inicial

Cada par de nodos vecinos ya ha abierto previamente un canal Lightning entre ellos. Cada nodo ha bloqueado **2 BTC** en su lado del canal, así que **cada canal arranca con 4 BTC de capacidad total** repartidos a partes iguales.

←

1 2 3 4 5 6 7 8 9 10

→

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Lightning Network

13 · Arquitectura técnica

13 · Arquitectura técnica

## Una red P2P sobre Bitcoin.

Cada nodo Lightning mantiene conexiones cifradas con sus _peers_, vigila su subconjunto de la cadena y participa en un _gossip_ distribuido para descubrir rutas. La implementación de referencia cumple las **BOLTs**.

*   **Noise\_XK** (BOLT 08): canal cifrado y autenticado entre peers. Sin metadatos en claro.
*   **Gossip protocol** (BOLT 07): los nodos difunden _channel\_announcement_, _channel\_update_ y _node\_announcement_ para construir el grafo.
*   **Implementaciones**: LND (Go), Core Lightning (C), Eclair (Scala), LDK (Rust).
*   **Nodo Bitcoin asociado**: Lightning requiere bitcoind para publicar y observar transacciones on-chain.

Wallet del usuario móvil · web · desktop · CLI gRPC / REST Nodo Lightning lnd · CLN · eclair · LDK TCP + Noise peers Lightning otros nodos de la red RPC / ZMQ bitcoind backend Bitcoin · capa 1

El nodo Lightning habla con **tres mundos**: la wallet del usuario, sus peers Lightning y bitcoind.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Lightning Network

14 · Wallets y custodia

14 · Wallets Lightning

## Wallets Lightning: ¿quién tiene las keys?

Toda interacción del usuario con Lightning pasa por una **wallet**. La gran división entre wallets está en **quién custodia los fondos**: el proveedor de la wallet, o el propio usuario.

Característica

Wallet custodial

Wallet self-custodial

Custodia de fondos

La tiene el proveedor (Wallet of Satoshi, exchange).

La tiene el usuario: sus claves, sus canales.

UX

Inmediata: solo descargar e iniciar sesión.

Requiere gestionar liquidez, backups, conectividad.

Privacidad

Baja: el proveedor ve todo el historial del usuario.

Alta: el usuario mantiene la información localmente.

Riesgo

Contraparte: si el proveedor falla, los fondos se pierden.

Usuario: si no gestiona backup / watchtower, puede perder saldo.

Ejemplos

Wallet of Satoshi, Strike, Cash App

Phoenix, Breez, Zeus, Mutiny

LSP Lightning Service Providers

Actores que ofrecen **liquidez entrante** bajo demanda, canales _just-in-time_ y rutas estables. Los wallets mobile dependen en gran medida de LSPs.

HÍBRIDOS Modelos intermedios

Algunos wallets delegan la conectividad y el enrutado sin tomar custodia: el usuario conserva las claves pero no opera un nodo 24/7.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Lightning Network

15 · BOLT 11

15 · BOLT 11

## Anatomía de una invoice.

**BOLT 11** (_Basis Of Lightning Technology #11_) es la especificación abierta que define cómo se codifica una _payment request_. Empaqueta en un único string **bech32** todo lo que el remitente necesita para pagar: destino, _payment hash_, importe, expiración y pistas de ruta.

*   **HRP** (prefijo legible): `lnbc` mainnet · `lntb` testnet · `lnbcrt` regtest.
*   **Importe compacto**: base + multiplicador `m`/`u`/`n`/`p`. `2500u` = 2 500 μBTC = 250 000 sats.
*   **Single-use**: una invoice = un pago. Reutilizarla puede provocar pérdida de fondos.
*   **Distribución**: viaja fuera de Lightning — QR, NFC, email, deep-link `lightning:`.

lnbc2500u1pvjluezpp5qqqsyqcyq5rqwzqfqqqsyqcyq5rqwzqfqqqsyqcyq5rqwzqfqypqdq5xysxxatsyp3k7enxv4jsxqzpuaztrnwngzn3kdzw5hydlzf03qdgm2hdq27cqv3agm2awhz5se903vruatfhq77w3ls4evs3ch9zw97j25emudupq63nyw24cg27h2rspfj9srp

HRP Amount Timestamp Tagged fields Signature

Ejemplo real de la spec BOLT 11 · 2 500 μBTC (≈ 250 000 sats) en mainnet · _"1 cup coffee"_.

Chainbitcoin (mainnet)

Amount250 000 sats · 250 000 000 msat · 2 500 μBTC

Description"1 cup coffee"

Payee pubkey03e7156ae33b0a208d0744199163177e909e80176e55d97a2f221ede0f934dd9ad

Payment hash0001020304050607080900010203040506070809000102030405060708090102

Timestamp1 496 314 658 · 2017-06-01 10:57:38 UTC

Expiry60 s · caduca 10:58:38 UTC

Signaturee89639ba…bd750e · recovery flag 1

UTILIDAD [lightningdecoder.com](https://lightningdecoder.com/) — pega una invoice y la descompone en tiempo real.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Lightning Network

16 · UX moderna

16 · Más allá de BOLT 11

## Experiencias reutilizables y estáticas.

Una invoice BOLT 11 sirve para **un único cobro**: quien recibe tiene que generar una nueva cada vez. Esto no encaja del todo con suscripciones, donaciones abiertas o propinas en streaming. Actualizaciones modernas añaden **tres mecanismos por encima** que cubren esos huecos sin tocar el protocolo base.

LNURL Capa HTTPS sobre Lightning

El wallet recibe una URL en bech32 o una _lightning address_ tipo `alice@dominio.com`, la resuelve contra el servidor del receptor por HTTPS y recibe una **invoice BOLT 11 fresca** para cada pago. El endpoint actúa de puente: estático por fuera, dinámico por dentro.

*   `lnurl-pay` — pagar a una dirección estática
*   `lnurl-withdraw` — tirar sats de un servicio
*   `lnurl-auth` — login sin contraseña
*   `lnurl-channel` — apertura asistida de canal

Pragmático, pero requiere HTTPS y servidor online. No está en las BOLTs.

KEYSEND Pago espontáneo sin invoice

El remitente genera él mismo un secreto `R`, deriva `H = hash(R)` como payment hash y envía el HTLC con `R` incluido en un **campo TLV** dentro del onion. El destinatario descifra `R`, comprueba el hash y cobra.

Sin acuerdo previo ni metadatos compartidos — basta conocer el _node\_id_.

*   Propinas y donaciones al vuelo
*   _Value-4-value_ en podcasts (streaming de sats)
*   Micropagos entre bots/servicios

Sin _proof of payment_ (R lo creó el remitente) y el receptor debe tener keysend activado.

BOLT 12 Offers y pagos reutilizables

Introduce las **offers**: códigos estáticos y reutilizables, como un QR de negocio. El wallet pide una invoice al destinatario vía **onion messages** — mensajería cifrada y enrutada como los pagos, pero sin bloquear fondos con HTLCs.

offer → invoice\_request → invoice → pago

*   _Blinded paths_: destino anónimo
*   Firmas Schnorr, más compactas
*   Recurrencia y refunds nativos
*   Sin HTTPS: todo por Lightning

Candidato a suceder a BOLT 11.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17