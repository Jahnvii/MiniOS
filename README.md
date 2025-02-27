# MiniOS

## Overview
MiniOS Scheduler is a lightweight OS kernel that simulates **process scheduling algorithms** to manage task execution efficiently. It supports three key scheduling algorithms:

1. **First Come, First Serve (FCFS)** – Executes processes in the order they arrive.
2. **Round Robin (RR)** – Allocates a fixed time slice (quantum) to each process.
3. **Priority Scheduling** – Executes processes based on priority (higher priority first).

This project utilizes **POSIX Threads (Pthreads)** for concurrency management and **mutex locks** for thread synchronization to ensure correct execution.

## Features
- Simulates real-world **process scheduling algorithms**.
- Implements **thread-based process execution** using **Pthreads**.
- Ensures thread synchronization with **mutex locks**.
- Supports **interactive selection** of scheduling algorithms.

