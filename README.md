# Lightning Polar Lab

<div align="left">
    <img src="https://img.shields.io/badge/LND-Lightning-F5A623?style=for-the-badge" alt="LND" />
    <img src="https://img.shields.io/badge/Bitcoin_Core-Regtest-F7931A?style=for-the-badge&logo=bitcoin" alt="Bitcoin Core" />
    <img src="https://img.shields.io/badge/Docker-Containers-2496ED?style=for-the-badge&logo=docker" alt="Docker" />
    <img src="https://img.shields.io/badge/Polar-Simulation-blue?style=for-the-badge" alt="Polar" />
</div>

<p align="left">
    <i>Laboratorio práctico de regtest para simular canales, enrutamiento y cierres en la red Lightning usando Polar y LND.</i>
</p>

## 📚 Índice del Laboratorio

1. [Recordatorio de Bitcoin](#1-recordatorio-de-bitcoin)
2. [Infraestructura de Bitcoin](#2-infraestructura-de-bitcoin)
3. [Introducción a Lightning Network](#3-introducción-a-lightning-network)
4. [Laboratorio Lightning con Polar](#4-laboratorio-lightning-con-polar)

## Conceptos Core de Lightning

Introducción a los conceptos clave que sustentan la red de canales de pago.

| Concepto              | Descripción                                                                                                                   |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Canal Bilateral**   | Enlace de liquidez entre dos nodos que requiere una transacción on-chain (funding tx) y permite pagos off-chain instantáneos. |
| **HTLC**              | Contrato (Hash Time-Locked Contract) que permite enrutar pagos por nodos intermedios de forma segura.                         |
| **Liquidez**          | Dividida en Inbound y Outbound, determina la capacidad de un nodo para recibir o enviar pagos en una ruta.                    |
| **Invoice (BOLT 11)** | Solicitud de pago codificada que contiene hash, importe, fecha de expiración y clave pública del destinatario.                |
| **Keysend**           | Pago espontáneo directo a una clave pública sin necesidad de generar una invoice previa.                                      |

## Operaciones de Red

Mecanismos de ciclo de vida de los canales y la liquidación de saldos off-chain a la cadena principal de Bitcoin.

| Operación              | Descripción                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Apertura de Canal**  | Transacción `on-chain` que bloquea fondos en una dirección 2-of-2 multifirma (UTXO).                                |
| **Cierre Cooperativo** | Cierre de mutuo acuerdo donde ambos nodos firman la `closing tx`, liberando los saldos rápidamente.                 |
| **Force-Close**        | Cierre unilateral publicando la última `commitment tx`. El saldo del iniciador retiene un `timelock` por seguridad. |

## System Architecture

| Componente         | Rol                                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------ |
| **Polar**          | Interfaz gráfica y orquestador que facilita la topología de la red local.                        |
| **Docker Desktop** | Motor de contenedores que ejecuta los nodos aislados y la base de datos en la máquina host.      |
| **Bitcoin Core**   | Nodo base backend en modo `regtest` que mina bloques, vigila txs on-chain y retransmite cierres. |
| **Nodos LND**      | Implementación Lightning Daemon que firma pagos, maneja canales y enruta tráfico.                |

## Technology Stack

- **Red Base**: Bitcoin Core vX
- **Implementación Lightning**: LND
- **Orquestación**: Polar v3.x, Docker Desktop

## Key Features

1. **Apertura y Cierre de Canales** — experimentación directa con transacciones on-chain que anclan y liquidan liquidez Lightning.
2. **Enrutamiento Multi-Hop** — propagación de pagos intermedios sin confianza usando contratos HTLC.
3. **Gestión de Liquidez Asimétrica** — exposición de problemas de liquidez _inbound_ y límites de saldo direccional.
4. **Análisis BOLT 11** — decodificación nativa de identificadores de pago estándar con y sin importes prestablecidos.
5. **Simulación de Force-Close** — ejecución forzada de cierres para comprobar la mecánica de `CheckSequenceVerify` y timelocks.

## Testing Strategy

Las validaciones del proyecto se ejecutan de manera exploratoria sobre un entorno de tipo `regtest` local mediante la interfaz visual de Polar y la CLI de LND (`lncli`). Se verifican visualmente las confirmaciones on-chain y los balances en cada salto off-chain.

## Project Setup

1. Instalar dependencias globales:
   - Polar 3.x
   - Docker Desktop

2. Configurar el entorno de red `lab-lightning`:
   - En Polar: `File → New Network`
   - Nodos LND: 4 (nombres: Alice, Bob, Carol, Dave)
   - Nodos Bitcoin: 1

3. Iniciar entorno local:
   Dale al botón `Start` en la interfaz de Polar y espera a que los contenedores arranquen.

4. Provisionar balances de prueba:
   ```bash
   # O a través de la pestaña Actions en UI:
   lncli walletbalance # Asegurar depósito de 100,000,000 sats
   ```

---

Built for Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026.


---

# 1. Recordatorio de Bitcoin

         

←→ Navegar

Módulo 05 · Bitcoin

Sesión 1 / Teoría

Recordatorioe

# ¿Qué es Bitcoin?

Un breve repaso a los fundamentos de la primera blockchain descentralizada

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

### 01 · Origen

### 01 · Origen y esencia

## Dinero electrónico entre pares.

Lo que hace aceptable a una criptomoneda

1.  ¿Puedo confiar en que este dinero es auténtico y no está falsificado?
2.  ¿Puedo confiar en que solo puede gastarse una vez? _(el problema del «doble gasto»)_
3.  ¿Puedo estar seguro de que nadie más podrá reclamarlo como suyo en lugar de mío?

— A. Antonopoulos, _Mastering Bitcoin_ · cap. 1

- **2008** Whitepaper

- **2009** Red Bitcoin

- **21MBTC** Suministro finito

- **~10min** Ritmo de bloques

*   **Satoshi Nakamoto (2008)** publica un whitepaper de 9 páginas sobre dinero electrónico P2P.
*   **Red descentralizada** sin autoridad central, sin intermediarios y sin permisos para participar.
*   **Resuelve el doble gasto** en entornos sin confianza mediante consenso por PoW.
*   **Unidad mínima**: 1 BTC = 100 000 000 satoshis; emisión programada hasta alcanzar 21 millones (en teoría).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Bitcoin

### 02 · Criptografía

### 02 · Cimientos criptográficos

## Propiedad basada en claves

«Poseer bitcoins equivale a poseer la clave privada asociada a la dirección» Esa clave autoriza a gastar las **UTXOs** (_Unspent Transaction Outputs_) vinculadas a la dirección — lo que llamamos «saldo» es simplemente la suma de esas UTXOs.

*   **Criptografía asimétrica** sobre la curva elíptica secp256k1.
*   **Derivación unidireccional**: clave privada → clave pública. Lo contrario es computacionalmente inviable.
*   **SHA-256** como función hash: compromete datos, construye hashes de bloques y direcciones.
*   **Firma digital ECDSA**: demuestra autoría sin revelar la clave privada; cualquiera puede verificarla con la clave pública.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

### 03 · Direcciones

### 03 · Direcciones y transacciones

## Tres formatos, un mismo propósito.

Legacy P2PKH · 1… `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` Pay-to-PubKey-Hash — el formato clásico basado en el hash de la clave pública.

Script P2SH · 3… `3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy` Pay-to-Script-Hash — habilita multi-firma, time-locks y otras condiciones.

SegWit Bech32 · bc1… `bc1qar0srrr7xfkvy5l643lydnw9re59gtzzwf5mdq` Nativo SegWit — tarifas más bajas, mejor detección de errores, estándar actual.

*   **Dirección** = derivada de la clave pública mediante SHA-256 + RIPEMD-160 y codificada (Base58 o Bech32).
*   **Transacción** = conjunto de inputs firmados con la clave privada + outputs que definen los nuevos propietarios.
*   **Fee** = inputs − outputs; incentivo económico que los mineros cobran por incluir la transacción en un bloque.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Bitcoin

### 04 · Blockchain

### 04 · Cadena de bloques

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

### 05 · Transacciones

### 05 · Transacciones y UTXO

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

### 06 · La red Bitcoin

### 06 · La red Bitcoin

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

### 07 · Tipos de nodos

### 07 · Tipos de nodos

## Cuatro perfiles, cuatro compromisos.

Full Node Bitcoin Core · «Satoshi Client» Módulos: **W · M\* · B · N** (\*minero desactivado por defecto) **Valida cada bloque y transacción** aplicando todas las reglas de consenso. Implementación de referencia (C++, desde 2009). Independencia y privacidad máximas; >95 % de los nodos públicos lo ejecutan.

Archive Node Full node que guarda todo el histórico Módulos: **B · N** (sin wallet, sin minado) Mantiene la **blockchain completa** sin podarla (>700 GB). Sirve datos a clientes SPV, exploradores de bloques, exchanges y procesadores de pago. Actúa como **edge router** del ecosistema.

Lightweight (SPV) Cliente ligero · móviles, wallets Módulos: **W · N** (sin blockchain) Solo descarga **cabeceras de bloques** (~80 B cada una) y usa _Simplified Payment Verification_. Verifica PoW y pruebas Merkle; **confía en nodos completos** para los datos. Menos recursos, menos seguridad.

Third-Party API Wallet delegada · REST / WebSocket Módulos: **W** (sin N, sin B) No habla el protocolo P2P: consulta un servicio externo (Electrum, Esplora, APIs de exchanges…). Saldos, historial y _broadcast_ se **delegan por completo**. Máxima comodidad, máxima dependencia.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Bitcoin

### 08 · Nodos ligeros y SPV

### 08 · Nodos ligeros y SPV

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

### 09 · Relay networks

### 09 · Propagación y relay networks

## Minimizar la latencia entre mineros.

El problema · block-finding race

Cuando un minero encuentra un bloque, los demás siguen trabajando sobre el anterior hasta que lo reciben. **Esos segundos de retraso favorecen a los grandes mineros** y empujan hacia la centralización. La red pública ya optimiza con _Compact Block Relay_ (BIP 152), pero **algunos actores van más allá con redes privadas**.

- **2015** Bitcoin Relay Network Matt Corallo · VPSes globales Red privada de servidores virtuales estratégicamente distribuidos para conectar **la mayoría de mineros y pools** con muy baja latencia.

- **2016** FIBRE Fast Internet Bitcoin Relay Engine Sucesor del BRN. **UDP + Forward Error Correction** + _compact block_: reduce drásticamente la latencia y tolera pérdidas sin re-peticiones.

La latencia es **crítica** en minería competitiva → en las siguientes transparencias nos centraremos en **minado** y proof-of-work.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

### 10 · Minado & consenso

### 10 · Minado = seguridad + consenso

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

### 11 · La mempool

### 11 · La mempool

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

### 12 · Confirmaciones & doble gasto

### 12 · ¿Cuándo está "confirmada" una tx?

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

### 13 · Recompensa & Proof of Work

### 13 · Incentivos + Proof of Work

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

### 14 · Mining pools & Stratum

### 14 · Mining pools

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

### 15 · Cambiando las reglas · Hard Forks

### 15 · Hard Forks

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

### 16 · Cambiando las reglas · Soft Forks

### 16 · Soft Forks

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

---

# 2. Infraestructura de Bitcoin

         

←→ Navegar

Módulo 05 · Bitcoin

Sesión 2 / Infraestructura

Bloque 2

# Infraestructura Bitcoin

De la instalación al bloque minado: cómo funciona un nodo Bitcoin por dentro.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

### 01 · Clientes de nodo

### 01 · Implementaciones del protocolo

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

### 02 · Anatomía del nodo

### 02 · Qué se instala con Bitcoin Core

## Cuatro binarios y un datadir.

bitcoind Daemon en _background_. El nodo propiamente dicho.

bitcoin-qt Mismo binario con GUI en Qt.

bitcoin-cli Cliente CLI que habla **JSON-RPC** con el daemon.

bitcoin-tx Crea y firma tx **offline**, sin nodo.

~/.bitcoin/ \# datadir por defecto ├── blocks/ \# bloques crudos: blk00000.dat, blk00001.dat… ├── chainstate/ \# UTXO set actual (LevelDB) ├── indexes/ \# opcional: txindex, coinstatsindex… ├── wallets/ \# descriptor wallets (SQLite) desde v0.21 ├── mempool.dat \# mempool persistido entre reinicios ├── debug.log \# log principal ├── bitcoin.conf \# configuración ├── testnet4/ \# cada red vive en su subdir ├── signet/ └── regtest/

Cada red (**main · testnet4 · signet · regtest**) aterriza en su propio subdirectorio, aislada del resto.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

### 03 · bitcoin.conf

### 03 · Configuración del nodo

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

### 04 · Hardware

### 04 · Archive vs. pruned

## Dos perfiles de disco, mismo consenso.

Archive · prune=0 Nodo **completo** ~700 GB (abril 2026) · SSD Guarda **toda la historia** de bloques. Útil para: _txindex_, explorers, block-cutters, queries del pasado. **IBD** (_Initial Block Download_ — la sincronización inicial desde el génesis hasta la punta actual): **días a semanas**. **Sirve bloques históricos** a otros peers cuando se sincronizan. _Community service_ de la red.

Pruned · prune≥550 Nodo **completo con poda** 5 – 20 GB · SSD o HDD Verifica **toda la cadena desde el génesis**, pero luego **tira los bloques viejos**. Mantiene solo UTXO set + últimos N MiB. No puede hacer _txindex_ ni servir bloques antiguos. **Misma seguridad** para ti, pero no contribuyes al IBD de otros.

~700GBCadena completa

- **4GBRAM** mínimo

8332Puerto RPC · mainnet

8333Puerto P2P

**Full node** — verifica todo el consenso (archive _o_ pruned).  
**Archive node** — variante de full node que _además_ conserva todos los bloques.  
**SPV / light client** — no verifica: confía en los peers y trabaja solo con cabeceras.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Bitcoin

### 05 · Interfaces

### 05 · Cómo se habla con bitcoind

## Cuatro canales, cuatro propósitos.

Control · pull JSON-RPC :8332 · HTTP + JSON El 95 % del trabajo. Control total del nodo y la wallet desde apps y CLI. **Autenticado**.

Read-only · pull REST :8332 · HTTP GET Solo lectura. Activar con `rest=1`. Útil para explorers que no necesitan escribir.

Notificación · push ZMQ :28332+ · TCP pub/sub El nodo _empuja_ eventos: **bloque nuevo**, **tx nueva**, **hashes**. Sin _polling_, reacción instantánea.

Consenso · pares P2P :8333 · binario propio Protocolo entre nodos para propagar bloques y tx. **BIP 324** añade cifrado entre pares.

Una stack típica: la **app** lanza comandos vía **RPC**, se suscribe a **ZMQ** para notificaciones, y expone datos al navegador por **REST**.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Bitcoin

### 06 · bitcoin-cli · cadena

### 06 · Cheatsheet · estado · bloques · tx

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

### 07 · bitcoin-cli · wallet

### 07 · Cheatsheet · wallet · PSBT · regtest

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

### 08 · Redes

### 08 · Redes de Bitcoin

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

### 09 · Signet

### 09 · Signet · la red pública estable

## Misma semántica, otra cadencia.

**Signet** es una red pública de pruebas en la que _no hay competición por minar_: en lugar de _proof-of-work_ abierto, los bloques los produce un conjunto cerrado de firmantes autorizados. Esto elimina los problemas de testnet3 (ataques de timewarp, _stalls_ de días, reorgs enormes) y hace que la red sea **predecible**, **estable** y **compartida** entre desarrolladores de todo el mundo.

Un bloque signet **solo es válido** si su coinbase incluye una firma de las claves autorizadas (_block challenge_). Elimina la volatilidad de testnet3 a cambio de un único punto de control explícito. BIP 325 · propuesto por Karl-Johan Alm en 2020.

Pública · oficial Signet global ~10 min/bloque La instancia por defecto (_Global Signet_). Activas con `-signet`. Faucets, explorers y peers públicos disponibles.

Pública · alternativa MutinyNet bloques cada 30 s Signet custom del equipo **Mutiny Wallet**. Tuvieron que forkear Core para hacer configurable el target. Faucet, esplora API, LSPs.

Privada Custom signet tú defines todo Arrancas con `-signet -signetchallenge=<script>`. **Tu propia red** para laboratorio, CI, talleres.

Signet encaja cuando necesitas **una red pública con otros actores** pero _predecible_. Para trabajo 100 % solo, regtest es mejor.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

### 10 · Regtest

### 10 · Regtest · nuestro laboratorio

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

### 11 · Simulación

### 11 · Herramientas de simulación regtest

## Regtest con todo incluido.

GUI · Electron + Docker Polar Interfaz gráfica para levantar **redes Bitcoin + Lightning en regtest** con un clic. Faucet integrado, logs en vivo, visualización de canales. Ideal para: **principiantes**, demos visuales, primeros experimentos. Recomendado · aprendizaje y testing sencillo

CLI · docker-compose Nigiri Un comando: `nigiri start` y tienes **bitcoind regtest + Electrs + Chopsticks** (proxy HTTP con faucet y `/mine`). Ideal para: **CI**, tests automatizados, scripts. Para scripting y tests

Kubernetes · Bitcoin Dev Project Warnet Despliega **redes Bitcoin P2P en un clúster Kubernetes** (o Minikube local). Monitoriza latencia, partición, comportamiento emergente. Usado en _Battle of Galen Erso_ — competición multi-equipo para **atacar nodos**. Avanzado · investigación

Filosofías distintas: **Polar** visualiza, **Nigiri** automatiza, **Warnet** estresa. Para prácticas guiadas en clase, lo más cómodo suele ser empezar con Polar y migrar a Nigiri cuando el ejercicio se automatiza.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Bitcoin

### 12 · Infra periférica

### 12 · Alrededor de bitcoind

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

### 13 · Node-in-a-box

### 13 · Soberanía sin compilar

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

### 14 · Minado

### 14 · Stack de minado · infraestructura

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

### 15 · Policy vs. consensus

### 15 · La polémica OP\_RETURN / Knots

## Policy no es consensus.

Core v30 (**oct. 2025**) eliminó el límite de 80 bytes en OP\_RETURN. Miles de operadores migraron a **Bitcoin Knots** en protesta. Knots pasó del ~5 % al **~22-25 %** de la red. Es el mejor ejemplo pedagógico actual de que la política de relay _no es lo mismo_ que el consenso. El debate más caliente del ciclo 2024-2026.

Policy · local Lo que decide **cada nodo** **Reglas blandas**, configurables, no rompen la red: qué tx relayas, cuáles aceptas en tu mempool, cuáles minas. Filtros de spam, `datacarriersize`, RBF. Dos nodos honestos pueden **discrepar** en policy sin bifurcar la red. Si una tx "prohibida" llega en un bloque, la **aceptan igual**.

Consensus · red Lo que decide **el protocolo** **Reglas duras**: PoW válida, scripts correctos, firmas ECDSA/Schnorr, cap de 21 M, límites de tamaño de bloque. **Violarlas bifurca la cadena**. Un _soft fork_ endurece consenso; un _hard fork_ lo afloja. El límite de OP\_RETURN **nunca fue consenso** — era policy.

Moraleja para operadores: **eliges tu política** al elegir cliente y configurar flags. Eliges **quién mina por ti** al elegir pool. Consenso lo decide la red entera, no tú.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Bitcoin

### 16 · Recursos y próximos pasos

### 16 · Cierre · puente a la práctica

## Ahora toca tocarlo.

Libro de referencia Mastering Bitcoin — Antonopoulos & Harding github.com/bitcoinbook/bitcoinbook

Tutoriales Learning Bitcoin from the Command Line github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line

Configuración Bitcoin Core Config Generator · Jameson Lopp jlopp.github.io/bitcoin-core-config-generator/

Docs oficiales bitcoincore.org · RPC API reference bitcoincore.org/en/doc/

Simulación Polar · Nigiri · Warnet lightningpolar.com · nigiri.vulpem.com · warnet.dev

Signet público MutinyNet · faucet · explorer mutinynet.com

Aprendizaje visual Learn Me A Bitcoin — Greg Walker learnmeabitcoin.com

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17

---

# 3. Introducción a Lightning Network

         

←→ Navegar

Módulo 05 · Lightning Network

Sesión 3 / Teoría

Segunda capa

# Lightning Network

Pagos instantáneos, privados, escalables y de bajo coste sobre la Bitcoin Network.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Lightning Network

### 01 · Escalabilidad

### 01 · El reto

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

### 02 · Segunda capa

### 02 · Panorama de soluciones L2

## Construir sobre Bitcoin sin tocarlo.

### 01 · ACTIVOS RGB

Emite y transfiere **activos** (stablecoins, tokens, NFTs) con _client-side validation_. Los datos viven _off-chain_; la L1 sólo graba un hash-commitment incrustado en una UTXO (técnica _Pay-to-Contract_).

**Ventaja:** máxima privacidad — la cadena no ve nada del activo. **Reto:** emisor y receptor deben conservar la historia completa.

### 02 · ACTIVOS Taproot Assets

Propuesta de Lightning Labs. Emite **activos** anclados en outputs Taproot mediante _Merkle trees_. Pueden enrutarse por Lightning → stablecoins a velocidad LN.

**Ventaja:** interoperable con Lightning vía LND. **Caso típico:** Tether (USDT) pagable como sats.

### 03 · PAGOS Lightning Network

Red de **canales de pago** enrutados con HTLCs que permite enviar bitcoin entre cualquier par de nodos de forma **instantánea y barata**.

**Ventaja:** miles de tx/s efectivas, fees de sats, finalidad en < 1 segundo. **Madurez:** la L2 más adoptada.

¿Qué comparten?

No cambian el protocolo base. Firman operaciones _off-chain_ y, si hay conflicto, recurren a la L1 como tribunal. Herencia de **seguridad** gracias a Bitcoin.

¿En qué se diferencian?

Lightning resuelve **pagos**. RGB y Taproot Assets resuelven **emisión y transferencia de activos**. Se complementan, no compiten.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Lightning Network

### 03 · Canales de pago

### 03 · Canales de pago · La idea clave

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

### 04 · Anatomía de un canal

### 04 · Ciclo de vida

## Apertura · Actualización · Cierre.

**Ejemplo simple ·** Alice pasa cada mañana por la cafetería de Bob a por un café. En lugar de pagar on-chain cada vez, abren un canal Lightning y liquidan todos los cafés con una única transacción al final.

### 01 · APERTURA funding tx (onchain) → 2-of-2 multisig ALICE BOB 🔑 🔑 2-of-2 MULTISIG · UTXO capacidad · 5 000 000 sats Alice deposita 5M sats; el output queda bajo el control conjunto de ambas claves. 1 tx on-chain 02 · ACTUALIZACIÓN N × commit\_tx (off-chain) ALICE BOB ☕ commit\_tx\_n alice 4.5M · bob 500k 1\. firma Alice → 2. Bob entrega ☕ → 3. firma Bob Cada commit\_tx redistribuye los saldos del canal. Con la tx firmada por Alice, Bob se asegura de poder cobrar al cierre del canal. 0 tx on-chain 03 · CIERRE settlement tx (onchain) · ambos firman ALICE BOB 4 500 000 sats 500 000 sats SETTLEMENT TX on-chain · minada Tras muchos cafés, ambos acuerdan cerrar. La settlement tx liquida los saldos on-chain. 1 tx on-chain

En todo el ciclo sólo **2 transacciones tocan la blockchain**: funding tx y settlement tx.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Lightning Network

### 05 · Commitment & revocación

### 05 · Fairness protocol

## ¿Por qué no se puede hacer trampa?

Si Alice publica un _commitment_ viejo que le favorece, Bob puede castigarla y llevarse **todo** el saldo del canal.

*   **Commitment transaction**: cada vez que el saldo cambia, se firma una nueva que refleja los saldos actuales. Si Alice la publica, su output queda _time-locked_ durante un periodo; ese retraso es la ventana en la que Bob puede detectar una commitment antigua y reaccionar antes de que Alice cobre.
*   **Revocation key**: al firmar la siguiente commitment, cada parte _revela_ una clave que revoca la anterior. Ambos guardan pruebas para castigar.
*   **Justicia criptográfica**: si Alice publica una commitment antigua, esa tx reparte el canal en dos outputs. Bob gasta el suyo al instante (ya estaba firmado a su favor) y, con la revocation key que Alice le reveló al sustituir ese estado, barre también el output de Alice antes de que venza su time-lock. Bob se queda con **los dos outputs**, es decir, con el 100% del canal.
*   **Watchtowers**: servicios que observan la cadena por ti; si estás offline, ellos publican la tx de castigo cuando detectan una commitment vieja.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Lightning Network

### 06 · Límites de un canal aislado

### 06 · El canal aislado

## Dos partes, dos problemas.

Un canal bilateral resuelve el intercambio repetido entre dos personas… _siempre que_ ambas colaboren y estén atentas. Fuera de ese escenario ideal aparecen limitaciones que frenan su uso real.

### 01 · DISPONIBILIDAD Si la contraparte desaparece

Para cerrar cooperativamente hace falta la firma de los dos. Si Bob se desconecta, Alice sólo puede hacer un **cierre unilateral** publicando su última commitment.

Ese output queda _time-locked_: sus fondos permanecen bloqueados durante todo el _CSV delay_ antes de que pueda gastarlos.

### 02 · VIGILANCIA Hay que estar mirando

El fairness protocol sólo castiga si alguien **detecta** la commitment antigua dentro del time-lock. Si nadie observa la cadena, el tramposo cobra sin consecuencias.

En la práctica obliga a tener el nodo online 24/7 o a delegar la vigilancia en _watchtowers_ de terceros.

### 03 · CAPITAL Fondos inmovilizados

La capacidad del canal vive en un UTXO 2-of-2. Mientras el canal esté abierto, ese capital no puede usarse para nada más.

Cuanto mayor sea el importe que quiera mover Alice, más dinero tiene que dejar encerrado por adelantado.

### 04 · RELACIÓN 1-A-1 Sólo sirve con esa persona

El canal entre Alice y Bob sólo permite pagarle **a Bob**. Para pagar a Carol hace falta abrir otro canal, con sus fees on-chain y su propio capital bloqueado.

Esta limitación es la que empujará hacia el **enrutado** a través de terceros, la idea clave de Lightning.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Lightning Network

### 07 · Los canales directos no bastan

### 07 · El límite de los canales bilaterales

## Un canal por pareja: inviable.

N = 6 15 canales

Grafo completo con N = 6 nodos

*   **Coste on-chain prohibitivo**: abrir un canal entre cada par requiere _N·(N−1)/2_ transacciones on-chain. Con 1M usuarios: **500 000 M** canales.
*   **Capital bloqueado**: cada canal inmoviliza fondos. Un usuario no puede fondear un canal con todo el mundo.
*   **Mantenimiento**: cada canal requiere vigilancia, firmas, storage de commits y posibles cierres.
*   **La solución**: enrutar pagos a través de canales ya existentes, como los paquetes en Internet.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Lightning Network

### 08 · HTLCs

### 08 · Hash Time-Locked Contracts

## El pegamento del enrutado.

Un **HTLC** (_Hash Time-Locked Contract_) es un contrato que paga al receptor _si_ revela un secreto antes de un plazo; en caso contrario, devuelve los fondos al remitente.

*   **Atomicidad**: o todos los saltos del enrutado cobran, o ninguno. **R** es el secreto que tiene que atravesar el camino completo; hasta que aparece, ningún nodo puede cobrar.
*   **Time-lock decreciente**: cada salto tiene un plazo un poco menor que el anterior, de modo que si el pago falla, cada nodo recupera sus fondos a tiempo.
*   **Onion routing**: el remitente cifra la ruta en capas, como una cebolla. Cada nodo intermedio descifra sólo _su_ capa, descubre a qué peer reenviar el pago y pasa el resto todavía cifrado. Ningún nodo conoce el camino completo: sólo ve a su predecesor y a su sucesor, nunca al remitente ni al destinatario final.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Lightning Network

### 09 · ¿Qué es Lightning Network?

### 09 · Lightning Network

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

### 10 · Beneficios de Lightning

### 10 · Qué se gana

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

### 11 · Capacidad y liquidez

### 11 · Inbound & outbound

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

### 12 · Ejemplo completo

### 12 · Ejemplo completo

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

### 13 · Arquitectura técnica

### 13 · Arquitectura técnica

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

### 14 · Wallets y custodia

### 14 · Wallets Lightning

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

### 15 · BOLT 11

### 15 · BOLT 11

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

### 16 · UX moderna

### 16 · Más allá de BOLT 11

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

---

# 4. Laboratorio Lightning con Polar

       

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