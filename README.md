# Reliable Data Transfer Protocol (SR&GBN) Implementation

**IERG3310 Lab1** - Implementation of a SR&GBN Protocol in C

## Overview

This project implements a Selective Repeat (SR) protocol to simulate reliable data transfer between a sender and a receiver. The protocol is implemented in C and uses a provided simulator framework to handle packet transmission, acknowledgments, and error handling.

## Features

- **Selective Repeat Protocol**: Implements the SR protocol for reliable data transfer.
- **Window Management**: Supports configurable window sizes for the sender.
- **Checksum Calculation**: Computes and verifies checksums for error detection.
- **Packet Handling**: Manages packet transmission, retransmission, and buffering.
- **Event Logging**: Logs important events such as packet transmission, reception, timeouts, and buffer operations.
- **Performance Metrics**: Calculates and displays throughput and goodput statistics.

## Implementation Details

### Protocol Behavior
- **Sender (Node A)**:
  - Sends packets within the window size.
  - Handles ACKs, retransmits packets on timeout, and manages buffer for outgoing messages.
  - Computes checksums for data packets and verifies ACKs.
- **Receiver (Node B)**:
  - Processes incoming packets, checks for corruption, and sends ACKs.
  - Delivers correct packets to the application layer.

### Key Functions
- `ComputeChecksum()`: Computes the checksum for a packet.
- `CheckCorrupted()`: Verifies if a packet is corrupted using checksum.
- `A_output()`: Handles data transmission from the sender.
- `A_input()`: Processes incoming ACKs at the sender.
- `A_timerinterrupt()`: Handles timer interrupts for retransmission.
- `B_input()`: Processes incoming packets at the receiver.

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
gcc sr.c -o sr
