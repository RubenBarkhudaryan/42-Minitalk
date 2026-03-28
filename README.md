# 42 Minitalk

## Overview
Minitalk is a small IPC project where a client sends text to a server using only Unix signals.

Each character is transmitted bit by bit with synchronization logic.

This project is a practical introduction to low-level inter-process communication (IPC) where reliability must be built manually on top of signal primitives.

## Features
- Signal-based communication:
  - SIGUSR1
  - SIGUSR2
- Server PID based client targeting
- Character reconstruction on server side
- Acknowledgment mechanism for reliability
- Bonus client/server with stronger delivery guarantees
- Unicode-oriented testing utilities included

## Core Concepts

### Signal-Based Protocol
Because only signals are allowed, the sender encodes each character as bits and transmits them one by one. The receiver reconstructs bytes in the correct order.

### Delivery Reliability
Without synchronization, fast signal bursts can be lost or misordered by implementation timing.

To mitigate this, the project uses acknowledgment logic so the client sends the next bit/char only when the server confirms reception.

### Server Identity
The client targets a specific process ID, which makes PID management part of normal usage and testing.

## Build
- make

## Run
Start server:
- ./server

Send message:
- ./client SERVER_PID "Hello from client"

Bonus:
- ./server_bonus
- ./client_bonus SERVER_PID "Hello bonus"

## Typical Flow
1. Start server and read printed PID.
2. Run client with PID and message.
3. Server decodes bitstream and prints reconstructed text.
4. Bonus mode improves synchronization robustness.

## Project Structure
- server.c / client.c: mandatory
- server_bonus.c / client_bonus.c: bonus
- minitalk_utils.c and libft_functions.c: helpers
- minitalk.h: shared declarations
- testers: additional test helpers

## Error Cases Considered
- invalid PID
- signal interruptions during transmission
- partial state recovery between characters
- graceful handling of malformed client calls

## Key Learnings
- Low-level IPC with signals
- Message framing and acknowledgment design
- Async-safe coding and robust edge-case handling

## Notes
Minitalk is a strong bridge from simple process signaling to protocol design fundamentals.
