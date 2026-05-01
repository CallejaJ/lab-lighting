         

←→ Navegar

Módulo 05 · Bitcoin

Sesión 2 / Infraestructura

Bloque 2

# Infraestructura Bitcoin

De la instalación al bloque minado: cómo funciona un nodo Bitcoin por dentro.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

01 · Clientes de nodo

01 · Implementaciones del protocolo

## Varios clientes, un mismo consenso.

C++ · MIT Bitcoin Core ~75% **Implementación de referencia**. v30 (oct. 2025). Descriptor-only wallets, sin BDB, sin límite OP\_RETURN.

C++ · MIT Bitcoin Knots ~22% Fork conservador de **Luke Dashjr**. Mantiene spam filters y el límite de OP\_RETURN.

Go · ISC btcd ~0.5% **Sin wallet** por diseño. Solo nodo + RPC. Muy usado en librerías del ecosistema Go.

C++ · AGPL libbitcoin ~1.3% Arquitectura **modular y limpia**. Poca tracción real en producción.

Node.js bcoin <0.5% Mantenido por Purse/Handshake. **Casi inactivo** hoy.

**¿Descentralización, también en el desarrollo?** Un bug sutil en una implementación minoritaria puede provocar un fork accidental.  
En **marzo de 2013**, la actualización de Bitcoin Core 0.7 a 0.8 cambió la base de datos interna (de BerkeleyDB a LevelDB): un bloque perfectamente válido para los nodos 0.8 fue rechazado por los nodos 0.7 por un límite silencioso de BDB, y la red se bifurcó durante **~6 horas** hasta que los mineros acordaron volver a la cadena compatible con 0.7.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Bitcoin

02 · Anatomía del nodo

02 · Qué se instala con Bitcoin Core

## Cuatro binarios y un datadir.

bitcoind Daemon en _background_. El nodo propiamente dicho.

bitcoin-qt Mismo binario con GUI en Qt.

bitcoin-cli Cliente CLI que habla **JSON-RPC** con el daemon.

bitcoin-tx Crea y firma tx **offline**, sin nodo.

~/.bitcoin/ \# datadir por defecto ├── blocks/ \# bloques crudos: blk00000.dat, blk00001.dat… ├── chainstate/ \# UTXO set actual (LevelDB) ├── indexes/ \# opcional: txindex, coinstatsindex… ├── wallets/ \# descriptor wallets (SQLite) desde v0.21 ├── mempool.dat \# mempool persistido entre reinicios ├── debug.log \# log principal ├── bitcoin.conf \# configuración ├── testnet4/ \# cada red vive en su subdir ├── signet/ └── regtest/

Cada red (**main · testnet4 · signet · regtest**) aterriza en su propio subdirectorio, aislada del resto.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

03 · bitcoin.conf

03 · Configuración del nodo

## El 90 % del despliegue vive en bitcoin.conf.

\# ── Red ───────────────────────────── testnet4\=1 \# signet=1 / regtest=1 \# ── Almacenamiento ───────────────── prune\=5000 \# MiB; 0 = archive dbcache\=4000 \# RAM para UTXO cache txindex\=1 \# incompatible con prune coinstatsindex\=1 blockfilterindex\=1 \# ── RPC ──────────────────────────── server\=1 rpcauth\=user:hash... rpcbind\=127.0.0.1 rpcallowip\=127.0.0.1 \# ── ZMQ · push a apps ────────────── zmqpubrawblock\=tcp://127.0.0.1:28332 zmqpubrawtx\=tcp://127.0.0.1:28333 \# ── Privacidad · Tor ─────────────── proxy\=127.0.0.1:9050 listenonion\=1

*   **Flags mutuamente excluyentes**: `testnet`, `testnet4`, `signet`, `regtest`. Sin ninguna = mainnet.
*   **Prune vs. txindex**: elige uno. Prune tira bloques viejos; txindex conserva todo e indexa.
*   **Índices opcionales**: `coinstatsindex` precomputa estadísticas agregadas del UTXO set (supply total, #UTXOs) para responder `gettxoutsetinfo` al instante. `blockfilterindex` construye filtros compactos BIP 157/158 que permiten a light wallets (p.ej. Neutrino) detectar _sus_ tx sin descargar bloques enteros.
*   **rpcauth** (hash salado) > `rpcuser/rpcpassword` en texto plano. _Nunca_ expongas el RPC a internet.
*   **ZMQ** permite que apps externas (explorers, bots) reaccionen al instante a nuevos bloques y tx.
*   **Configuración**: _Bitcoin Core Config Generator:_ [formulario web](https://jlopp.github.io/bitcoin-core-config-generator/) que te devuelve el fichero ya validado.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Bitcoin

04 · Hardware

04 · Archive vs. pruned

## Dos perfiles de disco, mismo consenso.

Archive · prune=0 Nodo **completo** ~700 GB (abril 2026) · SSD Guarda **toda la historia** de bloques. Útil para: _txindex_, explorers, block-cutters, queries del pasado. **IBD** (_Initial Block Download_ — la sincronización inicial desde el génesis hasta la punta actual): **días a semanas**. **Sirve bloques históricos** a otros peers cuando se sincronizan. _Community service_ de la red.

Pruned · prune≥550 Nodo **completo con poda** 5 – 20 GB · SSD o HDD Verifica **toda la cadena desde el génesis**, pero luego **tira los bloques viejos**. Mantiene solo UTXO set + últimos N MiB. No puede hacer _txindex_ ni servir bloques antiguos. **Misma seguridad** para ti, pero no contribuyes al IBD de otros.

~700GBCadena completa

4GBRAM mínimo

8332Puerto RPC · mainnet

8333Puerto P2P

**Full node** — verifica todo el consenso (archive _o_ pruned).  
**Archive node** — variante de full node que _además_ conserva todos los bloques.  
**SPV / light client** — no verifica: confía en los peers y trabaja solo con cabeceras.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Bitcoin

05 · Interfaces

05 · Cómo se habla con bitcoind

## Cuatro canales, cuatro propósitos.

Control · pull JSON-RPC :8332 · HTTP + JSON El 95 % del trabajo. Control total del nodo y la wallet desde apps y CLI. **Autenticado**.

Read-only · pull REST :8332 · HTTP GET Solo lectura. Activar con `rest=1`. Útil para explorers que no necesitan escribir.

Notificación · push ZMQ :28332+ · TCP pub/sub El nodo _empuja_ eventos: **bloque nuevo**, **tx nueva**, **hashes**. Sin _polling_, reacción instantánea.

Consenso · pares P2P :8333 · binario propio Protocolo entre nodos para propagar bloques y tx. **BIP 324** añade cifrado entre pares.

Una stack típica: la **app** lanza comandos vía **RPC**, se suscribe a **ZMQ** para notificaciones, y expone datos al navegador por **REST**.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Bitcoin

06 · bitcoin-cli · cadena

06 · Cheatsheet · estado · bloques · tx

## Los comandos de gestión del nodo.

Todos los comandos de esta lista se invocan como `bitcoin-cli [-regtest|-signet] <comando> [args…]`. El flag de red (por defecto, mainnet) se coloca _antes_ del comando.

Estado del nodo · cadena

*   getblockchaininfo \# altura, IBD, red, softforks
*   getnetworkinfo \# peers, versión, warnings
*   getmempoolinfo \# tx en mempool, minfee
*   getpeerinfo \# detalle de cada peer
*   getblockcount \# altura actual
*   getbestblockhash \# hash del tip
*   uptime \# segundos de vida del nodo

Consultar bloques

*   getblockhash <height>
*   getblock <hash> \[verbosity\]
*   getblockheader <hash>
*   getblockstats <hash|height>
*   getdifficulty \# dificultad actual (×genesis)
*   getchaintxstats \# estadísticas globales

Consultar transacciones

*   getrawtransaction <txid> \[verbose\]
*   decoderawtransaction <hex>
*   gettxout <txid> <vout> # UTXO set
*   sendrawtransaction <hex>
*   testmempoolaccept '\[<hex>\]'

Servicios auxiliares

*   help \[cmd\] # descripción del comando
*   stop \# apaga el nodo limpiamente
*   addnode <host> add|remove|onetry
*   setnetworkactive true|false
*   verifychain \[level\] \[nblocks\]

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Bitcoin

07 · bitcoin-cli · wallet

07 · Cheatsheet · wallet · PSBT · regtest

## Wallet, firma multi-parte y minería local.

Todos los comandos de esta lista se invocan como `bitcoin-cli [-regtest|-signet] <comando> [args…]`. El flag de red (por defecto, mainnet) se coloca _antes_ del comando.

Wallet · descriptor-only

*   createwallet "name"
*   loadwallet / unloadwallet
*   getnewaddress \["label"\] \[bech32|bech32m\]
*   listunspent \# tus UTXOs
*   getbalance / getbalances \# saldo total / desglose por estado
*   sendtoaddress <addr> <btc> # envía sats a una dirección

PSBT · firmas offline · multisig

*   walletcreatefundedpsbt \# crea PSBT con inputs y cambio
*   walletprocesspsbt \# firma con la wallet local
*   combinepsbt \# junta firmas
*   finalizepsbt \# produce hex broadcastable
*   analyzepsbt \# ¿qué le falta?
*   decodepsbt \# vista humana

Regtest · minería bajo demanda

*   generatetoaddress <n> <addr> # mina n bloques al vuelo
*   generateblock <addr> '\[txs\]' # mina un bloque con txs elegidas
*   invalidateblock <hash> # simula reorg
*   reconsiderblock <hash> # deshace un invalidateblock
*   getmininginfo \# dificultad, tamaño

Mempool · fees · descriptors

*   getrawmempool \[verbose\]
*   bumpfee <txid> # RBF
*   psbtbumpfee <txid>
*   prioritisetransaction \# sube/baja prioridad local
*   estimatesmartfee <confs>
*   getdescriptorinfo \# valida y añade checksum a un descriptor
*   deriveaddresses <desc> # expande un descriptor en direcciones

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Bitcoin

08 · Redes

08 · Redes de Bitcoin

## Una red para cada propósito.

Red

Consenso

Control

Uso típico

mainnet

PoW · ~10 min

Descentralizado

Producción.

testnet3

PoW, irregular (_timewarp_)

Descentralizado, inestable

Compatibilidad histórica. **En deprecación**.

testnet4

PoW + fix timewarp (**BIP 94**)

Descentralizado

Reemplazo oficial de testnet3 (Core v28+).

signet

Bloques **firmados** (BIP 325)

Clave del signet challenge

Testing predecible y estable.

regtest

Tú mineas con `generatetoaddress`

100 % local

Dev, CI, tests, **prácticas de clase**.

**Timewarp**: vulnerabilidad clásica de testnet3 donde los mineros pueden manipular los _timestamps_ de los bloques para forzar un ajuste de dificultad a la baja y minar cientos de bloques en segundos. BIP 94 (testnet4) lo corrige acotando el margen de los timestamps entre periodos de dificultad.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Bitcoin

09 · Signet

09 · Signet · la red pública estable

## Misma semántica, otra cadencia.

**Signet** es una red pública de pruebas en la que _no hay competición por minar_: en lugar de _proof-of-work_ abierto, los bloques los produce un conjunto cerrado de firmantes autorizados. Esto elimina los problemas de testnet3 (ataques de timewarp, _stalls_ de días, reorgs enormes) y hace que la red sea **predecible**, **estable** y **compartida** entre desarrolladores de todo el mundo.

Un bloque signet **solo es válido** si su coinbase incluye una firma de las claves autorizadas (_block challenge_). Elimina la volatilidad de testnet3 a cambio de un único punto de control explícito. BIP 325 · propuesto por Karl-Johan Alm en 2020.

Pública · oficial Signet global ~10 min/bloque La instancia por defecto (_Global Signet_). Activas con `-signet`. Faucets, explorers y peers públicos disponibles.

Pública · alternativa MutinyNet bloques cada 30 s Signet custom del equipo **Mutiny Wallet**. Tuvieron que forkear Core para hacer configurable el target. Faucet, esplora API, LSPs.

Privada Custom signet tú defines todo Arrancas con `-signet -signetchallenge=<script>`. **Tu propia red** para laboratorio, CI, talleres.

Signet encaja cuando necesitas **una red pública con otros actores** pero _predecible_. Para trabajo 100 % solo, regtest es mejor.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

10 · Regtest

10 · Regtest · nuestro laboratorio

## Tu red privada de Bitcoin, en segundos.

01 Arrancar $ bitcoind -regtest -daemon

→

02 Crear wallet + addr $ bitcoin-cli -regtest createwallet "lab" $ A=$(bitcoin-cli -regtest getnewaddress)

→

03 Minar 101 bloques $ bitcoin-cli -regtest \\ generatetoaddress 101 $A

*   **Dificultad mínima**: cada `generatetoaddress` produce un bloque _instantáneo_. Nadie más mina.
*   **Por qué 101** bloques: el coinbase de un bloque no es gastable hasta pasados **100 bloques** (regla COINBASE\_MATURITY).
*   **Red aislada**: puerto p2p `:18444`, RPC `:18443`. Cero riesgo de tocar mainnet.

\# Descargar Bitcoin Core → [bitcoincore.org/en/download](https://bitcoincore.org/en/download/) \# Binarios oficiales firmados por los # mantenedores del proyecto. Incluye # bitcoind, bitcoin-cli, bitcoin-qt y # bitcoin-tx. Disponible para Linux, # macOS y Windows.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Bitcoin

11 · Simulación

11 · Herramientas de simulación regtest

## Regtest con todo incluido.

GUI · Electron + Docker Polar Interfaz gráfica para levantar **redes Bitcoin + Lightning en regtest** con un clic. Faucet integrado, logs en vivo, visualización de canales. Ideal para: **principiantes**, demos visuales, primeros experimentos. Recomendado · aprendizaje y testing sencillo

CLI · docker-compose Nigiri Un comando: `nigiri start` y tienes **bitcoind regtest + Electrs + Chopsticks** (proxy HTTP con faucet y `/mine`). Ideal para: **CI**, tests automatizados, scripts. Para scripting y tests

Kubernetes · Bitcoin Dev Project Warnet Despliega **redes Bitcoin P2P en un clúster Kubernetes** (o Minikube local). Monitoriza latencia, partición, comportamiento emergente. Usado en _Battle of Galen Erso_ — competición multi-equipo para **atacar nodos**. Avanzado · investigación

Filosofías distintas: **Polar** visualiza, **Nigiri** automatiza, **Warnet** estresa. Para prácticas guiadas en clase, lo más cómodo suele ser empezar con Polar y migrar a Nigiri cuando el ejercicio se automatiza.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Bitcoin

12 · Infra periférica

12 · Alrededor de bitcoind

## El nodo no va solo.

`bitcoind` valida el consenso, pero por sí solo **no resuelve** preguntas como "¿qué saldo tiene esta dirección?" o "¿qué fees se están pagando ahora mismo?". Alrededor del nodo aparece un **ecosistema de servicios** que transforman esos datos en respuestas útiles para wallets, explorers y pasarelas de pago.

Núcleo bitcoind Valida consenso. Sirve RPC, REST, ZMQ. **No** hace búsqueda por dirección de forma eficiente.

Electrum server · Rust Electrs Indexa por **dirección**. Sync rápido (~1 día). Índice compacto. El más popular.

Electrum server · C++ Fulcrum **~8× más rápido** que ElectrumX para queries. Sync más lento (3-5 días). Recomendado por RaspiBolt.

Electrum server · Python ElectrumX El pionero. **El más lento** sincronizando (una semana). Uso histórico.

Explorer mempool.space El **estándar de facto**. Visualiza mempool, fees, bloques. Auto-hospedable.

Explorer btc-rpc-explorer · Esplora Alternativas más ligeras. Útiles en regtest y CI para inspeccionar.

Pasarela de pago BTCPay Server Auto-hospedado, multi-tienda. Integra bitcoind + Lightning + facturación.

Wallet desktop Sparrow · Specter Conectan a **tu** nodo (directo o vía Electrs). PSBT, multisig, hardware wallets.

**¿Qué es un Electrum server?** Un servicio que se conecta a tu `bitcoind`, lee la blockchain y construye un **índice por dirección y por script**. Expone el _protocolo Electrum_ (TCP/TLS, JSON) para que wallets ligeras (Sparrow, Electrum, Specter) pregunten "dame UTXOs e historial de esta xpub" sin descargar ni indexar toda la cadena. Sin un Electrum server propio, tu wallet acaba hablando con los servidores de terceros.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Bitcoin

13 · Node-in-a-box

13 · Soberanía sin compilar

## Distros llave en mano.

Distribución

Filosofía

Hardware típico

Umbrel

**Facilidad máxima**. UI tipo iOS, tienda de apps (BTCPay, mempool, electrs…).

Raspberry Pi 4/5 · Umbrel Home · VM Linux.

Start9 · StartOS

**Soberanía y seguridad** ante todo. Tor por defecto, servicios aislados.

Start9 Server (hardware propio) · x86/ARM.

RaspiBlitz

La más longeva. Foco en **Lightning**, pantalla LCD con stats en vivo.

Raspberry Pi + SSD externo.

myNode

Suite completa: BTCPay, JoinMarket, Whirlpool, Specter, Electrs…

**myNode Model Two** (2025): Intel N100, 16 GB, 2 TB.

nix-bitcoin

Config **declarativa y reproducible** en NixOS. Para sysadmins.

Cualquier máquina Linux con NixOS.

**Nota**: todas estas distros permiten ya **cambiar Core por Knots** con un switch en los ajustes — reflejo del cambio de cuota de mercado tras la polémica OP\_RETURN.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Bitcoin

14 · Minado

14 · Stack de minado · infraestructura

## Cliente, firmware, pool, protocolo.

Cliente · en el minero

*   **CGMiner** C — decano; sigue dominando en ASICs modernos.
*   **BFGMiner** C — fork de CGMiner, hardware específico.
*   **BOSminer** Rust — Braiins; reemplazo moderno, solo Stratum V2.
*   **cpuminer-opt** C — solo aprender o regtest.

Firmware alternativo · ASIC

*   **Braiins OS+** — open source, autotuning.
*   **LuxOS · Vnish · ePIC** — comerciales, optimizan consumo.

Protocolo minero ↔ pool

*   **Stratum V1** (2012, Slush) — TCP + JSON-RPC. _Pool decide_ el template.
*   **Stratum V2** — cifrado, binario, **Job Declaration Protocol**: el minero vuelve a decidir qué txs. Descentraliza la _policy_.
*   **getblocktemplate** BIP22/23 — clásico, para pools descentralizadas.

Software del pool · servidor

*   **CKPool · public-pool** — open source.
*   **SRI** — Stratum V2 reference implementation.
*   **Eloipool** — histórico, apenas mantenido.

Para regtest, `generatetoaddress` sustituye a todo este stack.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Bitcoin

15 · Policy vs. consensus

15 · La polémica OP\_RETURN / Knots

## Policy no es consensus.

Core v30 (**oct. 2025**) eliminó el límite de 80 bytes en OP\_RETURN. Miles de operadores migraron a **Bitcoin Knots** en protesta. Knots pasó del ~5 % al **~22-25 %** de la red. Es el mejor ejemplo pedagógico actual de que la política de relay _no es lo mismo_ que el consenso. El debate más caliente del ciclo 2024-2026.

Policy · local Lo que decide **cada nodo** **Reglas blandas**, configurables, no rompen la red: qué tx relayas, cuáles aceptas en tu mempool, cuáles minas. Filtros de spam, `datacarriersize`, RBF. Dos nodos honestos pueden **discrepar** en policy sin bifurcar la red. Si una tx "prohibida" llega en un bloque, la **aceptan igual**.

Consensus · red Lo que decide **el protocolo** **Reglas duras**: PoW válida, scripts correctos, firmas ECDSA/Schnorr, cap de 21 M, límites de tamaño de bloque. **Violarlas bifurca la cadena**. Un _soft fork_ endurece consenso; un _hard fork_ lo afloja. El límite de OP\_RETURN **nunca fue consenso** — era policy.

Moraleja para operadores: **eliges tu política** al elegir cliente y configurar flags. Eliges **quién mina por ti** al elegir pool. Consenso lo decide la red entera, no tú.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Bitcoin

16 · Recursos y próximos pasos

16 · Cierre · puente a la práctica

## Ahora toca tocarlo.

Libro de referencia Mastering Bitcoin — Antonopoulos & Harding github.com/bitcoinbook/bitcoinbook

Tutoriales Learning Bitcoin from the Command Line github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line

Configuración Bitcoin Core Config Generator · Jameson Lopp jlopp.github.io/bitcoin-core-config-generator/

Docs oficiales bitcoincore.org · RPC API reference bitcoincore.org/en/doc/

Simulación Polar · Nigiri · Warnet lightningpolar.com · nigiri.vulpem.com · warnet.dev

Signet público MutinyNet · faucet · explorer mutinynet.com

Aprendizaje visual Learn Me A Bitcoin — Greg Walker learnmeabitcoin.com

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17