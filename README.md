# Static-Timing-Analysis-2
 In this directory, we are focusing on application of these concepts on real chip using opensource STA tool called 'Opentimer'.

**Section 1: Introduction to STA-02 and opentimer tool**

1.1 Introduction to sta-2

![Screenshot 2025-02-07 161437](https://github.com/user-attachments/assets/9f6c11a4-b940-46d1-a3d0-db5a5a94db35)

OpenTimer is an open-source tool written in C++.

Unlike standard tools, it requires specific command-line constraints.

However, it supports standard formats like Verilog, DEF, and LEF.

**1.2 Introduction to opentimer, netlist definition and my_run.tcl creation**

**Analysis of Small Circuits Using OpenTimer**

Now, let's continue analyzing small circuits. The circuit we are working with consists of:

1.A launch flip-flop

2.A capture flip-flop

3.Combinational logic

This is the same circuit you might have seen in a previous module. We will now extend that work and perform timing analysis on it.

**Step 1: Naming the Nets**

Before diving into Static Timing Analysis (STA), the first step is naming all the nets in the circuit. These names are crucial for accurate analysis and debugging.

Input nets → Named as in

Output nets → Named as out

Internal nets → Named as net2, net3, and net4

These names are required for defining constraints and setting up simulations.

**Step 2: Launching OpenTimer** 

Now, let's launch OpenTimer, which we installed earlier in a Linux virtual machine.

Opening OpenTimer

After installation, launch OpenTimer from the terminal.

The tool operates through command-line inputs.

Getting Help on Commands

Typing help in the terminal displays all available commands.

To get specific details, use help <command>.

Some important commands:

Design Commands → Set up the circuit description and constraints.

Constraint Commands → Define timing constraints such as clock periods and delays.

Analysis Commands → Run different types of timing checks.

Reporting Commands → Generate reports for setup time, hold time, and slack.

![Screenshot 2025-03-11 102128](https://github.com/user-attachments/assets/c017aaab-1c0a-4fa5-9488-2d49401dc926)


1. Classes of Commands in OpenTimer
   
OpenTimer organizes commands into different classes:

**design-initiate** Commands that initialize the design, such as loading libraries, netlists, and constraints.

**design-modifier** Commands that modify the design topology, such as changing constraints, nets, or cells.

**design-report** Commands that generate reports on timing, slack, and violations.

**design-exec** Commands that execute the design operation, running the actual timing analysis.

2. Commands under design-initiate
   
These commands are responsible for loading necessary files to set up a timing analysis environment.

set_early_celllib_fpath <file_path.lib> 

Loads the early timing library (Liberty .lib file).

This file contains cell delay, setup time, and hold time information for early mode analysis.

set_late_celllib_fpath <file_path.lib> 

Loads the late timing library (another Liberty .lib file).

Used for late mode analysis (e.g., worst-case timing scenarios).

set_verilog_fpath <file_path.v> Loads the Verilog netlist file (.v).

Defines the logical connectivity of the design.

set_spef_fpath <file_path.spef>

Loads the Standard Parasitic Exchange Format (SPEF) file.

Contains information about wire delays and parasitics.

set_timing_fpath <file_path.timing>

Loads the timing constraint file (.timing).

Defines clock definitions, input/output delays, and constraints.

3. Key Takeaways
   
The design-initiate commands set up the environment by loading required files.

The Liberty (.lib) files define cell timing characteristics.

The Verilog (.v) file defines the circuit structure.

The SPEF (.spef) file provides parasitic delay information.

The Timing (.timing) file applies timing constraints.

Once the setup is complete, we move to:

Running STA using design-exec commands.

Modifying constraints with design-modifier.

Generating timing reports using design-report. 

![Screenshot 2025-03-11 104121](https://github.com/user-attachments/assets/9afbab78-ff89-4a80-8402-01cc2e877ad6)

There is a tcl file to work for opentimer. 

**vim my_run.tcl**

This command is used to open or create a file named my_run.tcl in the Vim text editor.


In the follwoing section,  there will be a TCL script (my_run.tcl) used for OpenTimer, a tool for Static Timing Analysis (STA).

![Screenshot 2025-03-11 132502](https://github.com/user-attachments/assets/f3e95e41-4732-4667-a46f-3c2135a0f6a6)

In the next, we will open this timer file, 

cat my_netlist.timing


**Section 2: Constraints creation commands for opentimer**


**2.1 Clock creation and clock arrival time definitions**

![Screenshot 2025-03-11 145902](https://github.com/user-attachments/assets/79180659-392c-4363-8d29-9f23a3e28584)

1️⃣ Clock Definition & Duty Cycle

A clock constraint defines the clock signal, including:

Source: Where the clock originates.

Period: The duration of one complete cycle.

Duty Cycle: The percentage of time the clock signal stays high within one cycle.

Example Explanation:

The clock period is 1 nanosecond (1 ns).

A 50% duty cycle means the clock stays high for 50% of the period and low for the remaining 50%.

If the duty cycle were 30%, the clock would be high for 30% of the time and low for 70%.


![Screenshot 2025-03-11 150419](https://github.com/user-attachments/assets/1740bd7b-da7a-49f9-8959-2d70270c5df0)

2️⃣ Arrival Time Definition

Arrival time is when a signal reaches a point in the circuit.

Example Terms:

Early rise arrival time: The earliest time a signal transition (0→1) occurs.

Early fall arrival time: The earliest time a signal transition (1→0) occurs.

Late rise arrival time: The latest time a signal transition (0→1) occurs.

Late fall arrival time: The latest time a signal transition (1→0) occurs.

Example in STA:

The early rise arrival time is 0 ps (picoseconds), meaning the clock starts exactly at 0 ps.

The late fall arrival time could be 50 ps, meaning that at most, the fall transition can occur 50 ps later.


![Screenshot 2025-03-11 151133](https://github.com/user-attachments/assets/a861fd5a-fd3f-4d6c-927d-30c8a39d7a63)


![Screenshot 2025-03-11 151519](https://github.com/user-attachments/assets/b2499d91-2d7a-4a14-8e69-9dca48ec78c3)










