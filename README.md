# Reliable Data Transfer Protocol Implementation

**IERG3310 Lab1** - Implementation of Selective Repeat (SR) and Go-Back-N (GBN) Protocols in C

## Overview

This project implements two reliable data transfer protocols, **Selective Repeat (SR)** and **Go-Back-N (GBN)**, to simulate reliable data transfer between a sender and a receiver. Both protocols are implemented in C and use a provided simulator framework to handle packet transmission, acknowledgments, and error handling.

## Features

### Common Features
- **Reliable Data Transfer**: Ensures data is delivered correctly despite packet loss or corruption.
- **Window Management**: Supports configurable window sizes for the sender.
- **Checksum Calculation**: Computes and verifies checksums for error detection.
- **Packet Handling**: Manages packet transmission, retransmission, and buffering.
- **Event Logging**: Logs important events such as packet transmission, reception, timeouts, and buffer operations.
- **Performance Metrics**: Calculates and displays throughput and goodput statistics.

### Selective Repeat (SR) Specific Features
- **Selective Acknowledgment**: Only lost or corrupted packets are retransmitted.
- **Efficient Resource Usage**: Minimizes retransmissions by acknowledging only the missing packets.

### Go-Back-N (GBN) Specific Features
- **Cumulative Acknowledgment**: Retransmits all packets from the first lost or corrupted packet onward.
- **Simpler Implementation**: Easier to implement but may be less efficient in high-loss environments.

## Implementation Details

### Protocol Behavior
- **Sender (Node A)**:
  - Sends packets within the window size.
  - Handles ACKs, retransmits packets on timeout, and manages buffer for outgoing messages.
  - Computes checksums for data packets and verifies ACKs.
- **Receiver (Node B)**:
  - Processes incoming packets, checks for corruption, and sends ACKs.
  - Delivers correct packets to the application layer.

### Key Functions (Common to Both Protocols)
- `ComputeChecksum()`: Computes the checksum for a packet.
- `CheckCorrupted()`: Verifies if a packet is corrupted using checksum.
- `A_output()`: Handles data transmission from the sender.
- `A_input()`: Processes incoming ACKs at the sender.
- `A_timerinterrupt()`: Handles timer interrupts for retransmission.
- `B_input()`: Processes incoming packets at the receiver.

### Protocol-Specific Functions
- **SR**:
  - `A_input_sr()`: Processes ACKs and advances the window base selectively.
- **GBN**:
  - `A_input_gbn()`: Processes ACKs and resets the window base cumulatively.

### Output Format
- Logs events such as packet transmission, reception, corruption, and timeouts.
- Provides a summary of packet statistics, including sent, received, retransmitted, lost, and corrupted packets.
- Calculates goodput in bits per second (bps).

## How to Run

### Prerequisites
- C compiler (e.g., GCC, Clang)
- Basic understanding of C programming and networking concepts

### Compilation
```bash
# For SR protocol
gcc sr.c -o sr

# For GBN protocol
gcc gbn.c -o gbn
