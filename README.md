# Two-Axis Pick-and-Place Automation | Siemens LOGO! 8.4 + FACTORY I/O 25.8

A PLC control project for the **Assembler (two-axis pick-and-place)** scene in **FACTORY I/O 25.8**. The control program is written in **FBD (Function Block Diagram)** using **Siemens LOGO! 8.4** and **LOGO! Soft Comfort 8.4**.

You can find simulation videos or photos of machine function in (media\) folder.



## Project overview

The complete operating sequence is divided into four functional sections:

1. **Feeder** — feeds/presents the item for the pick-and-place operation.
2. **Pick** — performs the pick operation.
3. **Place** — performs the place operation.
4. **Delivery** — performs the delivery/output operation and completes the cycle.

Each section has two control flags: `Run` and `Done`. The `Run` flag identifies the section currently executing. The next section is enabled when the current section completes and its `Done` flag becomes active. The sequence is interlocked so that the other sections remain inactive while one section is running.

See [Control sequence and stop behavior](docs/Assembler_FBD_Diagram.pdf) for the sequence description and state-transition diagram.

## Main features

- **Four-part sequential control:** Feeder → Pick → Place → Delivery, coordinated through each section's `Run` and `Done` flags.
- **Cycle-complete stop:** Pressing the normal machine Stop button requests a controlled stop. The ongoing cycle is allowed to continue through Delivery. When `Delivery_Done` becomes active, the next Feeder cycle is inhibited and the machine remains stopped.
- **Critical alarm handling:** Critical alarms stop the machine according to the programmed alarm response. The currently active alarm message is shown on the LOGO! display.
- **Structured FBD program:** The control logic is separated into functional sections to make troubleshooting, maintenance, and modification easier.
- **PLC display diagnostics:** The LOGO! display shows the execution/status information for the process sections.
- **Overall machine status:** The display background color indicates the overall state, such as alarm, running, or stopped.

## Technology stack

| Component | Version / description |
|---|---|
| PLC | Siemens LOGO! 8.4 |
| Programming language | Function Block Diagram (FBD) |
| PLC programming software | LOGO! Soft Comfort 8.4 |
| 3D simulation software | FACTORY I/O 25.8 |
| Simulation scene | Assembler — two-axis pick-and-place |



## Getting started

1. Install **LOGO! Soft Comfort 8.4** and **FACTORY I/O 25.8**.
2. Put the original LOGO! Soft Comfort project file in `src/` and open it in LOGO! Soft Comfort 8.4.
3. Put the customized Assembler scene file in `factoryio/` and open it in FACTORY I/O 2.5.8
4. Configure the FACTORY I/O driver and the LOGO! communication settings to match the actual project configuration. Document the selected driver, connection settings, and tag mapping without publishing credentials.
5. Run the simulation and verify the four-stage sequence, cycle-complete stop, critical alarm reactions, PLC display messages, and overall status indication.


## Sequence and stop behavior

The normal sequence follows the four sections in order. While a section's `Run` flag is active, the other sections are held inactive. Completion of a section is indicated by its `Done` flag and enables the following section.

The machine Stop button is described as a **cycle-complete stop**, not an immediate interruption of the cycle. When Stop is requested during an active cycle, the current cycle continues through the remaining sections. At the end of Delivery, `Delivery_Done` does not restart Feeder; the machine then remains stopped. This is distinct from the critical-alarm response.


## Alarms and diagnostics

When a configured critical alarm becomes active, the programmed alarm response stops the machine sequence and the active alarm message is displayed on the LOGO! display.

The program is organized into separate process sections. The LOGO! display provides status/execution feedback for the relevant section and indicates the overall machine state through its background color.


## Author and project information

- Author: Hamed Zalipour
- Project type: PLC programming and industrial automation simulation
- Date: 2026
- Contact: zalipourhamed@gmail.com
