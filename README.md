# USB3 Gigabit Ethernet Adapter

## Project Overview

This repository documents the design of a USB3.1 Gen 1 to Gigabit Ethernet adapter based on the Microchip LAN7800 USB-to-Ethernet controller.

The project is being developed in Altium Designer as a hardware design and PCB layout exercise. The focus is on schematic capture, component selection, USB3 routing, Gigabit Ethernet layout, power-tree design, ESD protection, PCB design rules, manufacturing outputs, and board bring-up planning.

## Project Goals

- Design a LAN7800-based USB3.1 Gen 1 to Gigabit Ethernet adapter in Altium Designer.
- Select and justify the main components used in the design.
- Create a clean schematic structure for USB, power, LAN7800, Ethernet, ESD, LEDs, reset, and test points.
- Define PCB design rules for USB3 and Gigabit Ethernet routing.
- Prepare manufacturing outputs including Gerbers, BOM, assembly files, and schematic PDFs.
- Document the bring-up and validation plan.

## Design Status

| Area | Status |
|---|---|
| Repository structure | Complete |
| Project requirements | Complete |
| Component selection | Complete |
| Schematic design |  Complete |
| Design rules | Complete |
| PCB layout | Not started |
| Manufacturing outputs | Not started |
| Bring-up plan | Not started |

## Main IC

- Microchip LAN7800 USB3.1 Gen 1 to Gigabit Ethernet controller

## Design Sections

- USB-C / USB3 interface
- LAN7800 controller section
- Gigabit Ethernet RJ45 / magnetics section
- Power rails and decoupling
- 25 MHz crystal / clock section
- Reset and configuration straps
- Status LEDs
- USB and Ethernet ESD protection
- Test points for bring-up
- 4-layer PCB stack-up
