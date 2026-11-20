# RoboGPT — Industrial Robotic Pick-and-Place Automation Simulation

## 1. Project Title
**RoboGPT: Automated Warehouse Pick-and-Place Simulation (`.roboviewer`)**

## 2. Project Overview
**RoboGPT** is an industrial robotics simulation project designed to model an automated pick-and-place material handling cell within a warehouse environment. Configured inside a `.roboviewer` simulation workspace, the system coordinates a **Universal Robots UR10e** 6-axis collaborative robotic arm equipped with a **Vacuum Gripper** and a **Belt Conveyor** to transport a **Package Box** onto a **Pallet** using deterministic waypoint and I/O control logic.

> **Simulation Notice:** This repository documents a virtual simulation environment. Physical hardware deployment and physical safety validation have not been executed.

## 3. Main Objectives
- Automate repetitive material transfer from a belt conveyor pickup zone to a palletizing/placement zone.
- Synchronize conveyor motion control with 6-DOF robotic arm kinematics and pneumatic vacuum actuation.
- Establish repeatable, collision-free approach, grasp, home, and release trajectories using predefined pose coordinates.
- Validate end-to-end pick-and-place sequencing in a virtual warehouse environment prior to physical deployment.

## 4. Hardware / Simulation Components
| Component | Specification / Model | Role in Simulation |
| :--- | :--- | :--- |
| **Robotic Manipulator** | UR10e (6-Axis Arm) | Executes articulated pick, transfer, and place trajectories. |
| **End-of-Arm Tooling (EoAT)** | Vacuum Gripper | Mounted at the robot TCP to secure and release flat-surfaced packages. |
| **Transport System** | Belt Conveyor | Moves the package box from the infeed zone to the predefined pickup stop. |
| **Workpiece / Material** | Package Box | Target payload handled during the automated pick-and-place cycle. |
| **Target Destination** | Industrial Pallet | Stationary receiving platform for package placement. |
| **Workspace** | Warehouse Environment | Virtual industrial cell housing the manipulator, conveyor, and pallet. |

## 5. System Architecture
The simulation operates through centralized sequence execution within the `.roboviewer` project environment:
- **Actuation Layer:** The **UR10e** manipulator executes joint/Cartesian motion commands while the **TCP-mounted Vacuum Gripper** toggles suction states (`ON`/`OFF`).
- **Material Transport Layer:** The **Belt Conveyor** advances the **Package Box** along a linear path until reaching the programmed pickup stop position.
- **Control & Logic Layer:** Sequential program blocks govern conveyor start/stop triggers, waypoint transitions (`Prepick` $\rightarrow$ `Pick` $\rightarrow$ `Home` $\rightarrow$ `Place`), and gripper state changes.

## 6. Working Principle
The system relies on **deterministic sequence programming** and **predefined spatial poses**. Rather than external machine vision, the simulation coordinates timing and positional stops: the belt conveyor delivers the package box to a known pickup coordinate and halts, allowing the UR10e arm to execute a top-down vertical approach, engage vacuum suction at the Tool Centre Point (TCP), retract via a safe home pose, and deposit the workpiece onto the pallet.

## 7. Automation Workflow
1. **Conveyor Start:** The belt conveyor activates and transports the package box toward the robot cell.
2. **Pickup Stop:** The conveyor reaches the predefined pickup stop coordinate and halts.
3. **Prepick Positioning:** The UR10e moves to the elevated `Prepick` pose directly above the package box.
4. **Vertical Approach:** The robot descends linearly along the tool Z-axis to contact the top surface of the box.
5. **Vacuum Grasp:** The vacuum gripper activates (`ON`), securing the package box to the TCP.
6. **Home Retraction:** The robot lifts the payload and transitions to the intermediate `Home` position.
7. **Placement Motion:** The robot moves from `Home` to the predefined `Place` position over the pallet.
8. **Payload Release:** The vacuum gripper deactivates (`OFF`), releasing the package box onto the pallet.
9. **Cycle Completion:** The robot clears the placement zone, completing the automated sequence.

## 8. Technologies and Tools Used
- **RoboViewer Simulation Platform (`.roboviewer`):** Virtual 3D robotics environment, cell layout, kinematic solver, and visual node/block sequence controller.
- **JSON Configuration (`manifest.json`):** Structured project metadata and scene/program serialization inside the `.roboviewer` archive.
- **UR10e Kinematic Model:** 6-DOF industrial robot digital twin configuration.

## 9. Key Features
- **Synchronized Cell Control:** Coordinated state transitions between linear conveyor transport and 6-axis robotic manipulation.
- **Top-Down Approach Strategy:** Dedicated `Prepick` and `Home` waypoints minimize lateral collision risks with the conveyor frame and pallet.
- **Modular Program Blocks:** Distinct movement, conveyor control, and gripper actuation nodes for straightforward debugging and trajectory tuning.
- **Pre-Deployment Verification:** Risk-free validation of reachability, TCP orientation, and cycle sequencing.

## 10. Applications
- Automated end-of-line packaging and carton handling.
- Warehouse palletizing and order fulfillment cells.
- Conveyor-to-pallet material transfer in logistics centers.
- General industrial pick-and-place production lines.

## 11. Project Author
- **Author:** Baqir Ariyal
- **Institution:** Lovely Professional University
- **Registration Number:** 12602693
- **Project Category:** Robotics and Automation