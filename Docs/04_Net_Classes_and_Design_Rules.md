# PCB Net Classes and Design Rules

## 1. Purpose

This document records the electrical, routing and manufacturing constraints applied to the LAN7800 USB 3.1 Gen 1 to Gigabit Ethernet Adapter PCB.

The rules are intended to:

- Control trace widths and clearances
- Apply controlled-impedance routing
- Separate high-speed, power and general-purpose nets
- Control differential-pair geometry
- Define via and board-manufacturing constraints
- Provide traceable engineering evidence for design review

## 2. Rule-Definition Strategy

The PCB will use a hierarchical rule structure.

General rules will apply to the complete PCB, while more-specific rules will override them for:

- USB 2.0
- USB 3.x SuperSpeed
- Gigabit Ethernet MDI
- Power rails
- Crystal circuitry
- General low-speed signals

The most-specific applicable rule will be given the highest priority.

## 3. Planned Net Classes

| Net class | Function |
|---|---|
| `USB2_HS` | USB 2.0 D+ and D− |
| `USB3_SS` | USB 3.x TX and RX differential pairs |
| `ETH_MDI` | Four Gigabit Ethernet MDI pairs |
| `CLOCK_25MHZ` | LAN7800 crystal nets |
| `POWER_VBUS` | USB VBUS and filtered VBUS |
| `POWER_3V3` | 3.3 V digital and analogue rails |
| `POWER_2V5` | LAN7800 internal 2.5 V rail |
| `POWER_1V2` | LAN7800 internal 1.2 V rails |
| `GENERAL` | Remaining low-speed signals |

## 4. Differential-Pair Classes

| Differential-pair class | Members |
|---|---|
| `USB2_DIFF` | USB 2.0 differential pair |
| `USB3_DIFF` | USB 3 TX and RX pairs |
| `ETH_DIFF` | MDI TR0, TR1, TR2 and TR3 pairs |

## 5. Controlled-Impedance Profiles

| Interface | Altium profile | Target |
|---|---|---:|
| USB 2.0 | `D90` | 90 Ω differential |
| USB 3.x | `D90` | 90 Ω differential |
| Gigabit Ethernet | `D100` | 100 Ω differential |

The profiles were calculated using the implemented four-layer stack in Altium Layer Stack Manager.

## 6. Planned Design Rules

The following PCB rules will be created:

1. Global electrical clearance
2. General signal width
3. USB VBUS width
4. 3.3 V power width
5. 2.5 V power width
6. 1.2 V power width
7. USB 2.0 differential-pair routing
8. USB 3.x differential-pair routing
9. Gigabit Ethernet differential-pair routing
10. Differential-pair skew limits
11. Crystal routing constraints
12. Via size constraints
13. Solder-mask constraints
14. Silkscreen clearance
15. Board-edge clearance

## 7. Initial Manufacturing Baseline

| Constraint | Initial value |
|---|---:|
| General minimum clearance | 0.15 mm |
| General signal width | 0.15 mm |
| Minimum finished drill | 0.30 mm |
| Minimum via diameter | 0.60 mm |
| Minimum annular ring | 0.15 mm |
| Solder-mask expansion | 0.05 mm |

These values are initial engineering constraints and will be reviewed before manufacturing release.

## 8. Rule Priority

The intended priority order is:

```text
USB3 differential rules
USB2 differential rules
Ethernet differential rules
Crystal rules
Power rules
General routing rules
Global manufacturing rules

## 9. Verification

The rule-definition stage will be complete when:

- All required net classes exist.
- All differential pairs are recognised.
- Controlled-impedance profiles are assigned.
- Rule priorities are reviewed.
- Online DRC is enabled.
- Batch DRC reports no unresolved rule-definition errors.
- Screenshots are stored in the repository.

## 10. Repository Evidence

The following screenshots will be stored in the repository:

- `Images/PCB/02_Impedance_Profiles.png`
- `Images/PCB/03_Net_Classes.png`
- `Images/PCB/04_Differential_Pair_Classes.png`
- `Images/PCB/05_Routing_Rules.png`
- `Images/PCB/06_Rule_Priorities.png`
