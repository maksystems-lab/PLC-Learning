# Project 06: Basic Bottle Counter

- Language: Ladder Diagram (LD)
- Count Engine: IEC 61131-3 Up-Counter (CTU) for edge-triggered object tracking
- Digital Signal Processing: Input transition handling without external pulse blocks
- Interlocking Logic: Disabling conveyor movement via counter state bits
- Manual Reset Control: Operator-driven pushbutton clearing of runtime accumulation

## Hardware / I/O Mapping

### Inputs
* `I_Master_Start` (BOOL) - Normally Open Start Pushbutton
* `I_Master_Stop` (BOOL) - Normally Closed Stop Pushbutton
* `I_Bottle_Sensor` (BOOL) - Photoelectric Proximity Sensor
* `I_Counter_Reset` (BOOL) - Normally Open Manual Reset Pushbutton

### Outputs
* `Q_Conveyor_Motor` (BOOL) - Main Conveyor Belt Actuator
* `Q_Limit_Reached_Lamp` (BOOL) - Batch Limit Status Indicator

## Control Philosophy

* **System Enable Latch:** Uses standard 3-wire seal-in logic to establish the core operational run state (`M_System_Run`).
* **Edge-Triggered Counting:** Direct wiring of the proximity sensor to the up-counter (`CTU`) input pin to increment the count accumulator on every physical beam break.
* **Safety Interlock Execution:** When the live accumulation matches the preset value (`PV = 10`), the counter output bit breaks the conveyor motor rung instantly, stopping further product feed to prevent a pile-up.
* **Manual Loop Clearance:** System operation remains completely inhibited until an operator presses the hard reset button, clearing the counter memory back to zero and allowing the conveyor to restart safely.
