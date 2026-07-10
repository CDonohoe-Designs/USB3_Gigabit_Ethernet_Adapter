# USB3 Gigabit Ethernet Adapter

## Project Overview

This repository documents the hardware design and PCB development of a **USB 3.1 Gen 1 to Gigabit Ethernet adapter** based on the **Microchip LAN7800 USB-to-Ethernet controller**.

The project is being developed in **Altium Designer** as a complete hardware design and PCB layout exercise.

The design work includes:

- Schematic capture and hierarchical design structure
- Component selection
- USB 2.0 and USB 3 SuperSpeed interfaces
- Gigabit Ethernet MDI interface
- Power-tree design and decoupling
- ESD protection
- Controlled-impedance PCB routing
- Differential-pair routing and length matching
- PCB design-rule definition
- Design for Manufacture (DFM)
- Design for Test (DFT)
- Manufacturing outputs
- Board bring-up and validation planning

---

## Project Goals

- Design a LAN7800-based USB 3.1 Gen 1 to Gigabit Ethernet adapter in Altium Designer.
- Select and justify the main components used in the design.
- Create a structured schematic covering USB, power, LAN7800, Ethernet, ESD protection, LEDs, reset and test points.
- Implement a four-layer PCB architecture suitable for USB 3 and Gigabit Ethernet routing.
- Define controlled-impedance and differential-pair PCB design rules.
- Route the USB 3 SuperSpeed, USB 2.0 and Gigabit Ethernet interfaces.
- Prepare manufacturing outputs including Gerbers, drill files, BOM, pick-and-place files and schematic PDFs.
- Document the board bring-up and validation process.

---

## Project Documentation

### Schematic

- [LAN7800 USB Ethernet Schematic PDF](Hardware/Altium/LAN7800_USB_Ethernet_RevA/LAN7800_USB_Ethernet_RevA_Schematic.pdf)

### Engineering Documentation

- [Documentation Folder](Docs/)
- [Design Requirements](Docs/01_Design_Requirements.md)
- [Component Selection](Docs/02_Component_Selection.md)
- [PCB Architecture and Stack-Up](Docs/03_PCB_Architecture_and_Stackup.md)

---

## Design Status

| Area | Status |
|---|---|
| Repository structure | Complete |
| Project requirements | Complete |
| Component selection | Complete |
| Schematic design | Complete |
| PCB architecture and stack-up | Complete |
| PCB design rules | Complete |
| Component placement | In progress |
| USB differential-pair routing | In progress |
| Ethernet differential-pair routing | Not started |
| General PCB routing | Not started |
| Manufacturing outputs | Not started |
| Bring-up plan | Not started |

---

## Main IC

**Microchip LAN7800**

USB 3.1 Gen 1 to 10/100/1000 Gigabit Ethernet controller.

The LAN7800 provides the bridge between the USB interface and the Gigabit Ethernet PHY.

---

## Design Sections

The hardware design contains the following main functional areas:

- USB 3.0 Type-B interface
- USB 2.0 D+ / D− interface
- USB 3 SuperSpeed TX and RX differential pairs
- LAN7800 controller
- Gigabit Ethernet MDI interface
- RJ45 connector and magnetics
- USB VBUS input filtering
- 3.3 V power regulation
- LAN7800 2.5 V and 1.2 V supply rails
- 25 MHz crystal and clock circuitry
- Reset and configuration straps
- Ethernet status LEDs
- USB and Ethernet ESD protection
- Power, reset and bring-up test points

---

## PCB Architecture

The design uses a **4-layer PCB stack-up**.

| Layer | Function |
|---|---|
| L1 – Top | Components, USB, Ethernet and critical signals |
| L2 – GND | Continuous high-speed signal reference plane |
| L3 – GND | Secondary continuous ground plane |
| L4 – Bottom | Power distribution and secondary routing |

USB and Ethernet high-speed differential pairs are routed primarily on the Top Layer and referenced to the continuous L2 ground plane.

The PCB design includes controlled-impedance profiles for:

- USB 2.0 — 90 Ω differential
- USB 3 SuperSpeed — 90 Ω differential
- Gigabit Ethernet MDI — 100 Ω differential

---

## PCB Design Rules

The Altium project includes dedicated design constraints for:

- USB 2.0 differential routing
- USB 3 SuperSpeed differential routing
- Gigabit Ethernet differential routing
- Differential-pair clearance
- Pair-to-pair Ethernet spacing
- USB 3 clearance from unrelated signals
- Power-rail trace widths
- Switching-node routing
- Via dimensions
- Annular ring requirements
- Solder-mask expansion
- Solder-mask sliver
- Silkscreen-to-mask clearance
- Differential-pair length matching

The routing constraints and impedance geometry are derived from the implemented Altium four-layer stack-up.

---

## Repository Structure

```text
USB3_Gigabit_Ethernet_Adapter/
│
├── Docs/
│   ├── 01_Design_Requirements.md
│   ├── 02_Component_Selection.md
│   └── 03_PCB_Architecture_and_Stackup.md
│
├── Hardware/
│   └── Altium/
│       └── LAN7800_USB_Ethernet_RevA/
│           ├── 01_USB_B_and_Power.SchDoc
│           ├── 02_LAN7800_Controller.SchDoc
│           ├── LAN7800_USB_Ethernet_RevA.PcbDoc
│           ├── LAN7800_USB_Ethernet_RevA.PrjPcb
│           └── LAN7800_USB_Ethernet_RevA_Schematic.pdf
│
├── Libraries/
├── Assembly/
├── BOM/
├── Gerbers/
├── PDFs/
│
└── README.md

## Project Files

- [View Schematic PDF](Hardware/Altium/LAN7800_USB_Ethernet_RevA/LAN7800_USB_Ethernet_RevA_Schematic.pdf)
- [View Engineering Documentation](Docs/)
- [Browse Altium Design Files](Hardware/Altium/LAN7800_USB_Ethernet_RevA/)
