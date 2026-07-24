# APB Slave Design and Verification using SystemVerilog

## Project Overview

This project implements an **AMBA APB (Advanced Peripheral Bus) Slave** in Verilog and verifies its functionality using a **transaction-based SystemVerilog verification environment**. The design supports both **read** and **write** transactions, incorporates **slave error detection**, and is verified using a custom testbench consisting of a **Generator, Driver, Monitor, Scoreboard, and Environment**.

The project was developed to strengthen my understanding of the APB protocol, finite state machine (FSM) design, transaction-based verification, mailbox communication, and functional checking using SystemVerilog without UVM.

---

## Features

- APB Slave RTL Design
- APB Read and Write Transactions
- Finite State Machine (FSM) Implementation
- Internal Memory-Based Data Storage
- PREADY Handshake Generation
- PSLVERR Generation
- Address Range Checking
- Invalid Address Detection
- Transaction-Based Verification Environment
- Mailbox Communication
- Functional Scoreboard
- Simulation Waveform Analysis

---

## APB Slave Interface

| Signal | Direction | Description |
|--------|-----------|-------------|
| **PCLK** | Input | APB Clock |
| **PRESETn** | Input | Active-Low Reset |
| **PSEL** | Input | Peripheral Select |
| **PENABLE** | Input | Access Phase Enable |
| **PWRITE** | Input | Read/Write Control |
| **PADDR** | Input | Address Bus |
| **PWDATA** | Input | Write Data Bus |
| **PRDATA** | Output | Read Data Bus |
| **PREADY** | Output | Transfer Completion Signal |
| **PSLVERR** | Output | Slave Error Indicator |

---

## Design Architecture

The APB Slave is implemented using a finite state machine consisting of the following states:

- **Idle**
- **Write**
- **Read**

The slave stores incoming write data into an internal memory array and returns the stored value during read transactions. Basic error detection logic has also been implemented for address and data validation.

---

## Verification Architecture

The verification environment follows a transaction-based architecture using SystemVerilog.

```text
          Generator
              │
              ▼
          Mailbox
              │
              ▼
           Driver
              │
              ▼
      APB Interface
              │
              ▼
        APB Slave DUT
              │
              ▼
          Monitor
              │
              ▼
          Mailbox
              │
              ▼
        Scoreboard
```

---

## Verification Components

### Transaction

Stores all APB transaction information including:

- Address
- Write Data
- Read Data
- Control Signals
- Slave Error Status

### Generator

- Randomly generates APB transactions.
- Sends transactions to the driver through a mailbox.

### Driver

- Drives APB interface signals according to the generated transactions.
- Implements APB read and write protocol.

### Monitor

- Observes DUT interface signals.
- Captures completed transactions.
- Sends captured transactions to the scoreboard.

### Scoreboard

- Maintains a reference memory model.
- Compares DUT read data with expected data.
- Reports data match/mismatch.

### Environment

- Connects all verification components.
- Performs reset.
- Controls simulation execution.
- Synchronizes Generator, Driver, Monitor, and Scoreboard.

---

## APB Transaction Flow

### Write Transaction

1. Assert **PSEL**
2. Drive **PADDR** and **PWDATA**
3. Assert **PENABLE**
4. Slave asserts **PREADY**
5. Data is written into internal memory

### Read Transaction

1. Assert **PSEL**
2. Drive **PADDR**
3. Assert **PENABLE**
4. Slave returns **PRDATA**
5. Transfer completes when **PREADY** becomes High

---

## Error Detection

The APB Slave includes basic error detection for:

- Invalid Address Range
- Invalid Address Value
- Invalid Data Value

Whenever an error condition is detected during a valid APB access, **PSLVERR** is asserted.

---

## Simulation Results

Simulation successfully demonstrates:

- ✅ APB Write Operations
- ✅ APB Read Operations
- ✅ Correct FSM State Transitions
- ✅ Proper PREADY Handshake
- ✅ Correct Memory Read/Write Operations
- ✅ Successful Scoreboard Verification
- ✅ Successful Transaction Completion

---

## Project Images

The repository includes the following simulation results:

- APB FSM Diagram
- Console Output (Write Transactions)
- Console Output (Read Transactions)
- Simulation Waveform

---

## Tools Used

- **Verilog HDL**
- **SystemVerilog**
- **EDA Playground**
- **Synopsys VCS Simulator**
- **EPWave**

---

## Learning Outcomes

Through this project, I gained hands-on experience with:

- AMBA APB Protocol
- RTL Design
- Finite State Machine (FSM) Design
- SystemVerilog Classes
- Transaction-Based Verification
- Mailbox Communication
- Virtual Interfaces
- Driver-Monitor Architecture
- Functional Scoreboard Development
- Functional Verification
- Waveform Debugging

---

## Repository Structure

```text
APB-Slave-SystemVerilog/
│
├── design.sv
├── testbench.sv
├── README.md
│
└── Images/
    ├── APB_FSM.png
    ├── Console_Output_1.png
    ├── Console_Output_2.png
    └── Simulation_Waveform.png
```

---

## Future Improvements

- Add Functional Coverage
- Add SystemVerilog Assertions (SVA)
- Verify Wait-State Transactions
- Extend to UVM-Based Verification Environment
- Improve Error Injection Testcases

---

## Author

**Shreyas M**

**Domain:** VLSI Design Verification | SystemVerilog | Digital Design
