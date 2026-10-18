# ⭐ Furnace and Casting Line PLC Replacement

**Tools:** Delta PLC · Structured Text · Delta DIAView / DIAScreen

## Situation
A grid overvoltage event reached the plant and the panel protections could not react in time. The PLCs of the melting furnace and of the casting line (with robot) were damaged. The manufacturer answered only after a long delay and could not provide the original program files, so restoring the old programs was not possible.

## My role
Rebuilt the control programs for both machines from scratch: machine analysis, I/O mapping, PLC programming, HMI/SCADA screens, and commissioning.

## What I built
- Corrected several faults that existed in the original logic.
- Designed the program for local grid conditions: frequent power interruptions, with safe recovery after each one.
- Air-cleaning function that clears clogged burner nozzles with compressed air.
- Purge of cold fuel oil from the pipes.
- Trend charts for temperature and pressure.
- Event timeline for operators.
- Fault log that works like a small database of alarms and failures.
- New high-reliability protection devices in the panels against supply overvoltage.

## Technical challenge
The furnace hydraulic system is driven by a Veichi SD650 servo drive. Its manual had incomplete RS485 information and the manufacturer could not give a correct answer, so I controlled the drive speed with a 0–10 V analog output from the PLC instead. I also had to work out how the hydraulic system operates before I could automate it.

## Images
<!-- TODO: add files to images/ then uncomment
![Main furnace screen](images/main-screen.png)
![Trend chart](images/trends.png)
![Event timeline](images/event-timeline.png)
![Fault log](images/fault-log.png)
![Furnace and casting line](images/plant.jpg)
-->
*Screenshots to be added: main furnace screen, trend chart, event timeline, fault log, plant photo.*

## Result
| | Before | After |
|---|---|---|
| Furnace stops | 2–3 per day, up to 1 hour each (swap a clogged burner gun, then clean the dirty one) | No unplanned stops for this reason; burner guns opened once a week for preventive cleaning only |

- The furnace restarts safely after a power cut and return.
- Rebuild and commissioning took about 10 days.
- A plant-wide UPS is being installed to protect against unreliable grid power.

