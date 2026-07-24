## Project Overview

This project implements an AMBA APB (Advanced Peripheral Bus) Slave in Verilog and verifies its functionality using a transaction-based SystemVerilog verification environment. The design supports both read and write transactions, incorporates slave error detection, and is verified using a custom testbench consisting of a Generator, Driver, Monitor, Scoreboard, and Environment.

The project was developed to strengthen understanding of APB protocol timing, finite state machine (FSM) design, transaction-based verification, mailbox communication, and functional checking without using UVM.

## Features
APB Slave RTL Design
Read and Write Transactions
APB FSM Implementation
Memory-based Data Storage
PREADY Handshake Generation
PSLVERR Generation
Address Range Checking
Invalid Address Detection
Transaction-based Verification Environment
Mailbox Communication
Functional Scoreboard
Waveform and Console Verification
APB Slave Interface
Signal	Direction	Description
PCLK	Input	APB Clock
PRESETn	Input	Active Low Reset
PSEL	Input	Peripheral Select
PENABLE	Input	Access Phase Enable
PWRITE	Input	Read/Write Control
PADDR	Input	Address Bus
PWDATA	Input	Write Data
PRDATA	Output	Read Data
PREADY	Output	Transfer Completion
PSLVERR	Output	Slave Error Indicator
Design Architecture

The APB Slave is implemented using a finite state machine consisting of three logical operations:

Idle
Write
Read

The slave stores incoming write data into an internal memory and returns the stored value during read transactions. Error detection logic is included for address and data validation.

## Verification Architecture

The verification environment follows a transaction-based architecture using SystemVerilog.

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

## Verification Components
Transaction

Stores APB transaction fields such as address, write data, read data, control signals, and slave error information.

Generator

Randomly generates APB read and write transactions and sends them to the driver using a mailbox.

Driver

Drives APB protocol signals to the DUT according to generated transactions.

Monitor

Samples DUT interface signals and reconstructs completed transactions.

Scoreboard

Maintains a reference memory model and compares DUT read data against expected values while reporting mismatches.

## Environment

Connects all verification components and controls reset, execution, synchronization, and simulation flow.

APB Transaction Flow
Write Operation
Assert PSEL
Drive Address and Write Data
Assert PENABLE
Slave asserts PREADY
Data is written into internal memory
Read Operation
Assert PSEL
Drive Address
Assert PENABLE
Slave returns PRDATA
Transfer completes when PREADY becomes High
Error Detection

The slave includes basic error detection for

Invalid Address Range
Invalid Address Value
Invalid Data Value

Whenever an error condition is detected during a valid APB access, PSLVERR is asserted.

## Simulation Results

Simulation confirms

Successful APB Read Operations
Successful APB Write Operations
Correct FSM State Transitions
Proper PREADY Handshake
Correct Memory Read/Write
Correct Scoreboard Comparison
Successful Transaction Completion
Waveforms

The repository contains

APB FSM Diagram
Console Output
Simulation Waveform

demonstrating successful protocol execution and verification.

## Tools Used
Verilog HDL
SystemVerilog
EDA Playground
Synopsys VCS Simulator
EPWave

## Learning Outcomes

This project helped me gain practical experience in

APB Protocol
RTL Design
Finite State Machine Design
SystemVerilog Classes
Transaction-Based Verification
Mailboxes
Virtual Interfaces
Driver-Monitor Communication
Scoreboard Development
Functional Verification
Debugging using Waveforms
