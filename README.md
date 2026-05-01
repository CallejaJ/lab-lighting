# Lightning Polar Lab

<div align="center">
    <img src="https://img.shields.io/badge/LND-Lightning-F5A623?style=for-the-badge" alt="LND" />
    <img src="https://img.shields.io/badge/Bitcoin_Core-Regtest-F7931A?style=for-the-badge&logo=bitcoin" alt="Bitcoin Core" />
    <img src="https://img.shields.io/badge/Docker-Containers-2496ED?style=for-the-badge&logo=docker" alt="Docker" />
    <img src="https://img.shields.io/badge/Polar-Simulation-blue?style=for-the-badge" alt="Polar" />
</div>

<p align="center">
    <i>Laboratorio práctico de regtest para simular canales, enrutamiento y cierres en la red Lightning usando Polar y LND.</i>
</p>

## Conceptos Core de Lightning

Introducción a los conceptos clave que sustentan la red de canales de pago.

| Concepto | Descripción |
|---|---|
| **Canal Bilateral** | Enlace de liquidez entre dos nodos que requiere una transacción on-chain (funding tx) y permite pagos off-chain instantáneos. |
| **HTLC** | Contrato (Hash Time-Locked Contract) que permite enrutar pagos por nodos intermedios de forma segura. |
| **Liquidez** | Dividida en Inbound y Outbound, determina la capacidad de un nodo para recibir o enviar pagos en una ruta. |
| **Invoice (BOLT 11)** | Solicitud de pago codificada que contiene hash, importe, fecha de expiración y clave pública del destinatario. |
| **Keysend** | Pago espontáneo directo a una clave pública sin necesidad de generar una invoice previa. |

## Operaciones de Red

Mecanismos de ciclo de vida de los canales y la liquidación de saldos off-chain a la cadena principal de Bitcoin.

| Operación | Descripción |
|---|---|
| **Apertura de Canal** | Transacción `on-chain` que bloquea fondos en una dirección 2-of-2 multifirma (UTXO). |
| **Cierre Cooperativo** | Cierre de mutuo acuerdo donde ambos nodos firman la `closing tx`, liberando los saldos rápidamente. |
| **Force-Close** | Cierre unilateral publicando la última `commitment tx`. El saldo del iniciador retiene un `timelock` por seguridad. |

## System Architecture

| Componente | Rol |
|---|---|
| **Polar** | Interfaz gráfica y orquestador que facilita la topología de la red local. |
| **Docker Desktop** | Motor de contenedores que ejecuta los nodos aislados y la base de datos en la máquina host. |
| **Bitcoin Core** | Nodo base backend en modo `regtest` que mina bloques, vigila txs on-chain y retransmite cierres. |
| **Nodos LND** | Implementación Lightning Daemon que firma pagos, maneja canales y enruta tráfico. |

## Technology Stack

- **Red Base**: Bitcoin Core vX
- **Implementación Lightning**: LND
- **Orquestación**: Polar v3.x, Docker Desktop

## Key Features

1. **Apertura y Cierre de Canales** — experimentación directa con transacciones on-chain que anclan y liquidan liquidez Lightning.
2. **Enrutamiento Multi-Hop** — propagación de pagos intermedios sin confianza usando contratos HTLC.
3. **Gestión de Liquidez Asimétrica** — exposición de problemas de liquidez *inbound* y límites de saldo direccional.
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
