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

## Differential-Pair Routing Rules

| Rule | Differential-pair class | Impedance profile | Width | Gap |
|---|---|---|---:|---:|
| `DP_USB3_D90` | `USB3_DIFF` | `D90` | 0.246 mm | 0.127 mm |
| `DP_USB2_D90` | `USB2_DIFF` | `D90` | 0.246 mm | 0.127 mm |
| `DP_ETH_D100` | `ETH_DIFF` | `D100` | 0.184 mm | 0.127 mm |

The preferred width and pair gap are derived from the controlled-impedance profiles in Altium Layer Stack Manager.

## Differential-Pair Clearance Rule

A dedicated clearance rule permits the controlled-impedance gap within each differential pair while maintaining a larger clearance to unrelated copper.

| Rule | Application | Minimum clearance | Priority |
|---|---|---:|---:|
| `CLEARANCE_SAME_DIFF_PAIR` | Members of the same differential pair | 0.127 mm | 1 |
| `Clearance_1` | All other electrical objects | 0.254 mm | 2 |

The differential-pair rule has higher priority than the general board-clearance rule.

## Routing Width Rules

| Rule | Scope | Minimum | Preferred | Maximum |
|---|---|---:|---:|---:|
| `WIDTH_SWITCH_NODES` | `SWITCH_NODES` | 0.40 mm | 0.60 mm | 1.00 mm |
| `WIDTH_VBUS` | `POWER_VBUS` | 0.40 mm | 0.60 mm | 1.00 mm |
| `WIDTH_1V2` | `POWER_1V2` | 0.30 mm | 0.50 mm | 0.80 mm |
| `WIDTH_3V3` | `POWER_3V3` | 0.30 mm | 0.50 mm | 0.80 mm |
| `WIDTH_2V5` | `POWER_2V5` | 0.20 mm | 0.30 mm | 0.50 mm |
| `WIDTH_GENERAL` | All remaining nets | 0.15 mm | 0.20 mm | 0.30 mm |

The values are initial routing constraints. Short power connections may use copper regions where this provides a lower-impedance current path.

## Routing Layer Rules

High-speed and clock nets are constrained to the Top Layer so that they reference the adjacent continuous L2 ground plane and avoid unnecessary layer transitions.

| Rule | Net class | Top Layer | Bottom Layer |
|---|---|---|---|
| `ROUTE_LAYER_USB3` | `USB3_SS` | Allowed | Not allowed |
| `ROUTE_LAYER_USB2` | `USB2_HS` | Allowed | Not allowed |
| `ROUTE_LAYER_ETH` | `ETH_MDI` | Allowed | Not allowed |
| `ROUTE_LAYER_CLOCK` | `CLOCK_25MHZ` | Allowed | Not allowed |
| `ROUTE_LAYER_GENERAL` | All remaining nets | Allowed | Allowed |

The high-speed interfaces will be routed primarily on L1 and referenced to the continuous L2 `GND_1` plane.

## Routing Via Style Rules

| Rule | Scope | Preferred diameter | Preferred hole |
|---|---|---:|---:|
| `VIA_POWER` | Power net classes | 0.80 mm | 0.40 mm |
| `VIA_GENERAL` | All remaining nets | 0.60 mm | 0.30 mm |

The general via provides a 0.15 mm nominal annular ring. Larger power vias are preferred where supply rails change layers. USB, Ethernet and crystal nets are constrained to the Top Layer to avoid unnecessary via transitions.

## Matched-Length Rules

This checks the overall length difference between MDI_TR0, TR1, TR2 and TR3. Microchip allows a maximum delta of 600 mils or 15.24 mm between the four pairs.

Altium uses Within Differential Pair Length for matching the two members of each pair, and Group Matched Lengths for matching complete differential pairs against one another.

| Rule                      | Scope       | Mode                     | Tolerance |
| ------------------------- | ----------- | ------------------------ | --------: |
| `MATCH_USB3_WITHIN_PAIR`  | `USB3_DIFF` | Within differential pair |  0.127 mm |
| `MATCH_ETH_WITHIN_PAIR`   | `ETH_DIFF`  | Within differential pair |   1.27 mm |
| `MATCH_ETH_BETWEEN_PAIRS` | `ETH_DIFF`  | Between complete pairs   |  15.24 mm |

## Minimum Annular Ring Rule

The minimum annular ring is controlled to maintain sufficient copper around drilled pads and vias.

| Rule | Scope | Minimum annular ring |
|---|---|---:|
| `MIN_ANNULAR_RING` | All pads and vias | 0.15 mm |

The general routing via uses a 0.60 mm diameter and a 0.30 mm hole:

`(0.60 mm − 0.30 mm) / 2 = 0.15 mm`


## Drilled-Hole Size Rule

The drilled-hole rule prevents pads and vias from using hole sizes below the selected manufacturing baseline.

| Rule | Scope | Minimum hole | Maximum hole |
|---|---|---:|---:|
| `MIN_DRILLED_HOLE` | All pads and vias | 0.30 mm | 6.35 mm |

The 0.30 mm minimum matches the general routing-via hole size. The maximum value allows for connector and mechanical mounting holes and will be reviewed against the final footprint set.

## Solder-Mask Expansion Rule

A positive solder-mask expansion is applied around component pads to compensate for solder-mask registration tolerances.

| Rule | Scope | Top expansion | Bottom expansion |
|---|---|---:|---:|
| `SM_EXPANSION_PADS` | All component pads | 0.075 mm | 0.075 mm |

The expansion is measured from the copper-pad edge. Vias are excluded from this rule and will be handled separately through via-tenting settings.

Fine-pitch footprints may use local solder-mask overrides where necessary to maintain acceptable solder-mask slivers.

## Minimum Solder-Mask Sliver Rule

The solder-mask sliver rule controls the minimum remaining strip of solder mask between adjacent mask openings.

| Rule | Scope | Minimum sliver |
|---|---|---:|
| `MIN_SOLDER_MASK_SLIVER` | All solder-mask openings | 0.075 mm |

The value is based on an LDI solder-mask manufacturing process. Fine-pitch components will be reviewed individually during DRC to confirm that the resulting mask geometry is manufacturable.

## Silk-to-Solder-Mask Clearance Rule

The silkscreen clearance rule prevents component outlines, reference
designators and other overlay objects from overlapping exposed pads and
solder-mask openings.

| Rule | Scope | Check mode | Minimum clearance |
|---|---|---|---:|
| `SILK_TO_MASK_CLEARANCE` | All silkscreen objects | Clearance to solder-mask openings | 0.10 mm |

Silkscreen objects will be reviewed after component placement to ensure
that reference designators remain readable and do not extend over exposed
copper, holes or solderable pads.


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
