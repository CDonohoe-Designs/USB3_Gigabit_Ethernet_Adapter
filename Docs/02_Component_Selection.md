# Component Selection

## Purpose

Record the main component choices for the LAN7800 USB3 Gigabit Ethernet Adapter.

## Selection Criteria

Components will be selected based on:

- Electrical suitability
- Datasheet support
- Availability
- Practical footprint
- Low-volume assembly suitability
- 4-layer PCB compatibility

## Main Component Summary

| Function | Proposed Choice | Status |
|---|---|---|
| USB-to-Ethernet controller | Microchip LAN7800 | Selected |
| USB connector | USB-C receptacle | Planned |
| Ethernet connector | RJ45 with integrated magnetics | TBD |
| USB ESD protection | Low-capacitance USB3 ESD device | TBD |
| Ethernet ESD protection | Gigabit Ethernet ESD device | TBD |
| Power regulation | Buck / LDO regulators | TBD |
| Clock source | 25 MHz crystal or oscillator | TBD |
| LEDs | Link / activity / speed LEDs | TBD |
| Test points | SMT test pads | Planned |

## Key Design Notes

- LAN7800 is the main USB3.1 Gen 1 to Gigabit Ethernet controller.
- USB-C is preferred for a modern compact adapter design.
- RJ45 with integrated magnetics is preferred to simplify layout.
- USB3 and Ethernet interfaces require suitable low-capacitance ESD protection.
- Power rails and current budget must be confirmed from the LAN7800 datasheet.
- A 25 MHz clock source is required.
- Test points should be added for VBUS, power rails, reset, enables, and useful bring-up signals.

## Next Actions

1. Confirm LAN7800 package.
2. Select USB-C connector.
3. Select RJ45 MagJack.
4. Select USB and Ethernet ESD devices.
5. Define the power tree.
6. Select the 25 MHz clock source.
7. Add manufacturer part numbers.