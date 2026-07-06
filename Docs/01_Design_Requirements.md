# Design Requirements

## Project Title

USB3 Gigabit Ethernet Adapter

## Objective

Design a USB3.1 Gen 1 to Gigabit Ethernet adapter based on the Microchip LAN7800 USB-to-Ethernet controller.

The project is being developed in Altium Designer and documented as a complete hardware design exercise, including schematic capture, component selection, PCB layout planning, design-rule setup, manufacturing outputs, and board bring-up planning.

## Project Scope

This project covers the hardware design of a compact USB3-to-Gigabit-Ethernet adapter. The design will include the USB interface, LAN7800 controller circuitry, Ethernet interface, power regulation, ESD protection, clocking, status LEDs, test points, PCB layout, and manufacturing documentation.

Firmware and driver development are outside the current scope. The adapter is expected to use standard operating system support for the LAN7800 device where available.

## Main Functional Requirements

| Requirement | Description |
|---|---|
| USB interface | USB3.1 Gen 1 upstream interface operating up to 5 Gbps |
| Ethernet interface | Gigabit Ethernet downstream interface |
| Main controller | Microchip LAN7800 USB-to-Ethernet controller |
| Power source | Bus-powered from USB VBUS |
| Power regulation | On-board regulators for LAN7800 supply rails |
| Clock source | 25 MHz clock source for LAN7800 |
| Ethernet connector | RJ45 connector with integrated or external magnetics |
| ESD protection | ESD protection on USB and Ethernet external interfaces |
| Status indication | LEDs for link, activity, and speed indication where supported |
| Reset/configuration | Reset and configuration strap support |
| Test access | Test points for power rails, reset, clock, and bring-up signals |

## USB Interface Requirements

- Use a USB3.1 Gen 1 capable connector.
- Support USB SuperSpeed differential pairs.
- Include suitable ESD protection on USB data lines.
- Route USB3 differential pairs with controlled impedance.
- Keep USB3 pair routing short, direct, and length-conscious.
- Maintain solid ground reference under high-speed USB signals.
- Avoid stubs and unnecessary vias on high-speed USB routing where practical.

## Ethernet Interface Requirements

- Support 10/100/1000 Mbps Ethernet operation.
- Use an RJ45 connector with suitable magnetics.
- Route Ethernet MDI pairs as controlled, length-conscious differential pairs.
- Keep Ethernet pair routing symmetrical and away from noisy switching nodes.
- Include appropriate Bob Smith termination or magnetics-side termination if required by the selected connector/reference circuit.
- Provide Ethernet-side ESD protection where appropriate.

## Power Requirements

- The board shall be powered from USB VBUS.
- Generate all required LAN7800 supply rails on-board.
- Provide adequate bulk and local decoupling.
- Place decoupling capacitors close to the relevant LAN7800 power pins.
- Keep switching regulator loops compact.
- Keep noisy power switching areas away from USB3 and Ethernet differential pairs.
- Provide test points for key power rails.

## Clocking Requirements

- Provide a 25 MHz clock source suitable for the LAN7800.
- Place the crystal or oscillator close to the LAN7800.
- Keep crystal traces short and symmetrical.
- Avoid routing high-speed or noisy signals close to the clock circuit.
- Follow the selected crystal or oscillator datasheet recommendations.

## PCB Requirements

| Item | Requirement |
|---|---|
| PCB layers | 4-layer PCB preferred |
| Grounding | Solid ground reference plane |
| High-speed routing | Controlled-impedance routing for USB3 and Ethernet differential pairs |
| Power routing | Low-impedance power distribution with local decoupling |
| Manufacturability | Suitable for low-volume PCB manufacture |
| Testability | Bring-up test points included |
| Assembly | Components selected with practical package sizes where possible |

## Proposed PCB Stack-Up

A 4-layer stack-up is preferred:

| Layer | Function |
|---|---|
| L1 | Components and high-speed signals |
| L2 | Solid ground plane |
| L3 | Power distribution and secondary routing |
| L4 | Secondary signals and low-speed routing |

## Design-for-Test Requirements

The design should include test points for:

- USB VBUS
- Main regulated power rails
- Ground
- Reset
- LAN7800 clock check point, if practical
- LED/status signals, if useful
- Any enable pins for regulators
- Key configuration strap pins, if useful during bring-up

## Design-for-Manufacture Requirements

- Use practical component packages for hand inspection and low-volume assembly.
- Avoid unnecessarily small passive components unless required for layout.
- Maintain clear silkscreen markings for connectors, LEDs, test points, and polarity-sensitive components.
- Use consistent reference designators.
- Generate Gerbers, drill files, BOM, pick-and-place, and schematic PDFs.
- Run schematic validation and PCB DRC before manufacturing output release.

## Documentation Requirements

The repository should include:

- Design requirements
- Component selection notes
- Power-tree notes
- USB3 and Ethernet layout notes
- Schematic review checklist
- PCB review checklist
- Bring-up and validation test plan
- Manufacturing output folders
- Images of schematic, PCB layout, and 3D view

## Out of Scope

The following are not part of the initial project scope:

- Custom firmware development
- Driver development
- Enclosure design
- EMC pre-compliance testing
- Production test fixture design
- Mass-production release package

These may be added later if the project is extended.

## Initial Design Status

| Area | Status |
|---|---|
| Repository structure | Complete |
| Design requirements | In progress |
| Component selection | Not started |
| Schematic design | Not started |
| PCB layout | Not started |
| Design rules | Not started |
| Manufacturing outputs | Not started |
| Bring-up plan | Not started |

## Next Steps

1. Select the USB connector type.
2. Confirm LAN7800 variant and package.
3. Define the power tree.
4. Select RJ45/magnetics solution.
5. Select USB and Ethernet ESD protection devices.
6. Create the Altium project shell.
7. Start schematic capture.
