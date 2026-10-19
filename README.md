# ⭐ Furnace and Casting Line PLC Replacement

**Tools:** Delta PLC · Delta DIADesigner (PLC programming, Structured Text) · Delta DIAScreen (HMI)

## Hardware

| Part | Model | Qty |
|------|-------|-----|
| PLC | Delta DVP28SV311T | 1 |
| Digital input modules | DVP-16SM | 2 |
| Digital output modules | DVP-16SN | 2 |
| Thermocouple input module | DVP-04TC | 1 |
| Analog I/O module | DVP-06XA | 1 |
| HMI | Delta DOP-110IS | 1 |

## Situation

A grid overvoltage event reached the plant and the panel protections could not react in time. The PLCs of the melting furnace and of the casting line (with robot) were damaged. The manufacturer answered only after a long delay and could not provide the original program files, so restoring the old programs was not possible.

## My role

Rebuilt the control programs for both machines from scratch: machine analysis, I/O mapping, PLC programming, HMI screens, and commissioning.

## What I built

- Corrected several faults that existed in the original logic.
- Designed the program for local grid conditions: frequent power interruptions, with safe recovery after each one.
- Air-cleaning function that clears clogged burner nozzles with compressed air.
- Purge of cold fuel oil from the pipes.
- Trend charts for temperature and pressure.
- Event timeline for operators.
- Fault log that works like a small database of alarms and failures.
- New high-reliability protection devices in the panels against supply overvoltage.
- Operator setpoints and HMI screens on a Delta DOP-110IS.
- **HMI text rewritten:** the original screen had been programmed abroad (China), and its Arabic and English translations were poor and hard for operators to understand. I rewrote all screen texts, alarms and labels in clear Arabic and English so operators can read them correctly.
- **Electrical drawings redone in EPLAN:** I redrew the control panel schematics from scratch in EPLAN following European standards, which makes the panel much easier to read, troubleshoot and maintain.

## Technical challenge

The furnace hydraulic system is driven by a Veichi SD650 servo drive. Its manual had incomplete RS485 information and the manufacturer could not give a correct answer, so I controlled the drive speed with a 0–10 V analog output from the PLC instead. I also had to work out how the hydraulic system operates before I could automate it.

## Electrical design

Full panel schematics (EPLAN, European standards): see [schematics/](schematics/).

## Images

![Arabic HMI home screen with the customer logo blurred](images/hmi-home-ar-blurred-logo.png)

![English HMI home screen with the customer logo blurred](images/hmi-home-en-blurred-logo.png)

![Arabic HMI trend chart](images/hmi-trend-screen-ar-blurred-logo.png)

*Trend chart interface; no live readings are shown because the furnace is currently stopped.*

![HMI event log](images/hmi-event-log-ar-blurred-logo.png)

![HMI I/O status screen](images/hmi-io-status-ar-blurred-logo.png)

![HMI manual controls screen](images/hmi-manual-controls-ar-blurred-logo.png)

### PLC code example: exhaust valve timer

The Structured Text example below starts a timer while the exhaust valve is moving and sets an error if it does not finish within the configured interval.

![PLC Structured Text exhaust valve timer and error logic](images/plc-exhaust-valve-timer-code.png)

### Startup logic and interlocks

This excerpt shows the automatic-mode condition, system on/off toggle, and startup checks that block operation when fan-fault signals are active.

![PLC automatic mode and startup interlocks](images/plc-startup-interlocks-code.png)

### Hydraulic system sequence

This example shows part of the hydraulic door-open sequence, including its start delay and related interlocks.

![PLC hydraulic door sequence](images/plc-hydraulic-door-sequence-code.png)

### Servo speed register mapping

The MOV blocks copy the speed value from D350 to the servo speed registers.

![PLC servo speed MOV blocks](images/plc-servo-speed-mov-blocks.png)

## PLC communications and hardware

The network overview shows the PLC and two HMI panels connected over Modbus serial and Ethernet. The PLC hardware layout shows the controller and installed I/O modules. The IP address has been blurred in the network screenshot.

![PLC and HMI network overview with IP address blurred](images/plc-hmi-network-redacted-ip.png)

![PLC hardware and I/O module layout](images/plc-hardware-module-layout.png)

## Result

| | Before | After |
|---|---|---|
| Furnace stops | 2–3 per day, up to 1 hour each (swap a clogged burner gun, then clean the dirty one) | No unplanned stops for this reason; burner guns opened once a week for preventive cleaning only |

- The furnace restarts safely after a power cut and return.
- Rebuild and commissioning took about 10 days.
- A plant-wide UPS is being installed to protect against unreliable grid power.
