# PCB Architecture and Stack-Up

## 1. Purpose

This document records the PCB architecture and layer-stack decisions for the LAN7800 USB 3.1 Gen 1 to Gigabit Ethernet Adapter.

The PCB contains:

- USB 3.1 Gen 1 differential pairs
- USB 2.0 differential pair
- Four Gigabit Ethernet MDI differential pairs
- A 25 MHz crystal circuit
- Switching power regulators
- Analogue and digital power rails

The PCB must provide continuous signal-reference planes, controlled-impedance routing and low-impedance power distribution.

## 2. PCB Architecture Decision

**Decision:** Use a four-layer PCB based on Altium Designer's generic four-layer stack.

**Reasons:**

- USB 3 and Gigabit Ethernet require stable signal-return paths.
- Solid ground planes reduce return-path discontinuities and EMI.
- Four layers provide better routing and power distribution than a two-layer PCB.
- The structure supports controlled-impedance differential routing.
- It provides a practical balance between performance, complexity and cost.

The initial layout will use Altium's generic FR-4 material and stack parameters. The exact values can be adjusted later if the design is prepared for manufacture.

## 3. Layer Assignment

| Layer | Name | Primary function |
|---|---|---|
| L1 | TOP | Components, USB and Ethernet differential pairs, critical signals |
| L2 | GND | Continuous solid ground reference plane for L1 |
| L3 | GND | Continuous solid ground reference plane for L4 |
| L4 | BOTTOM | Power distribution, low-speed signals and secondary routing |

## 4. Layer-Use Rules

- Route USB and Ethernet differential pairs primarily on L1.
- Reference L1 high-speed signals directly to the L2 ground plane.
- Keep L2 continuous beneath USB, Ethernet and crystal-related signals.
- Keep L3 as a continuous ground plane.
- Use L4 for power rails and non-critical signals.
- Use short, wide tracks or copper regions for power distribution.
- Avoid routing high-speed signals across plane gaps or voids.
- Avoid layer changes on USB and Ethernet differential pairs.
- Connect L2 and L3 using ground stitching vias.
- Add ground copper on the outer layers where routing permits.

## 5. Controlled-Impedance Requirements

| Interface | Target differential impedance |
|---|---:|
| USB 2.0 D+ / D− | 90 Ω |
| USB 3 TX+ / TX− | 90 Ω |
| USB 3 RX+ / RX− | 90 Ω |
| Gigabit Ethernet MDI pairs | 100 Ω |

The final track width and pair separation will be calculated using Altium Layer Stack Manager.

The values will depend on:

- Copper thickness
- Dielectric thickness
- Dielectric constant
- Routing layer
- Distance to the reference plane

Track width and pair gap will not be selected by guesswork.

## 6. Altium Impedance Profiles

The following impedance profiles will be created in:

`Design → Layer Stack Manager → Impedance`

| Profile name | Type | Target |
|---|---|---:|
| `USB_90R_DIFF` | Differential | 90 Ω |
| `ETH_100R_DIFF` | Differential | 100 Ω |

Primary routing configuration:

```text
Routing layer: L1 Top
Reference layer: L2 GND

## 7. Grounding Architecture

The PCB will use one common digital ground plane on L2.

Separate schematic net names such as:

- `USB_SHIELD`
- `RJ45_SHIELD`
- `GND`

are used to document different EMC functions. The connector shields will connect to circuit ground only through their defined coupling networks.

The LAN7800 exposed pad and all local ground connections will connect to the solid L2 ground plane using short connections and multiple ground vias.

## 8. Power-Distribution Architecture

The principal PCB power rails are:

- `VBUS`
- `VBUSF`
- `+3V3`
- `+3V3_A`
- `+2V5`
- `+1V2`
- `+1V2_A`

Power distribution will primarily use copper regions or short, wide tracks on L3 and the outer layers.

The following areas require compact placement and routing:

- USB VBUS ferrite filter
- TLV62568 3.3 V regulator
- LAN7800 internal 1.2 V regulator loop
- LAN7800 analogue-rail ferrite filters
- Local decoupling capacitors

## 9. Mechanical Architecture

The intended signal flow is:

`USB Type-B → ESD protection → LAN7800 → RJ45 MagJack`

Initial placement principles:

- USB Type-B and RJ45 connectors at board edges.
- ESD protection immediately beside the USB connector.
- LAN7800 positioned between USB and Ethernet interfaces.
- Crystal and load capacitors beside the LAN7800 XI/XO pins.
- Switching regulators kept away from the crystal and high-speed differential pairs.
- Decoupling capacitors placed beside their associated supply pins.

The final board dimensions will be defined after initial component placement.

## 10. Verification

The stack-up will be considered complete when:

- The exact Eurocircuits buildup is selected.
- Copper and dielectric parameters are entered into Altium.
- The total thickness matches the manufacturer buildup.
- `USB_90R_DIFF` and `ETH_100R_DIFF` profiles are calculated.
- Calculated width and gap values are checked against Eurocircuits.
- The final stack-up screenshot is stored in the repository.
- PCB design rules reference the corresponding impedance profiles.

## 11. Evidence

Planned repository evidence:

- `Images/PCB/01_Layer_Stack.png`
- `Images/PCB/02_USB_90R_Impedance_Profile.png`
- `Images/PCB/03_ETH_100R_Impedance_Profile.png`
- `Images/PCB/04_Eurocircuits_Buildup.png`

## 12. Current Status

| Item | Status |
|---|---|
| Four-layer architecture selected | Complete |
| Manufacturer baseline selected | Complete |
| Nominal board thickness selected | Preliminary |
| Exact manufacturer buildup | Not selected |
| Altium layer stack entered | Not started |
| USB impedance profile | Not started |
| Ethernet impedance profile | Not started |
| Stack-up evidence captured | Not started |