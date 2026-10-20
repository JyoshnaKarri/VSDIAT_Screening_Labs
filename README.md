# VSDIAT Screening Labs: Physical Verification with SKY130A

This repository documents the labs I completed independently for the VSDIAT screening. It covers setting up the open-source toolchain, designing and verifying an inverter, and DRC and LVS exercises on the SkyWater 130 nm (sky130A) process.

## Environment

- Windows laptop with WSL2 (Ubuntu 24.04 distro named `VSD`)
- Magic 8.3.685
- Netgen 1.5.325
- Xschem 3.4.8RC
- ngspice 42
- sky130A PDK installed with Volare

## Labs

| Lab | Topic | Folder |
|-----|-------|--------|
| 0 | Tool installation and setup | [Lab0_Tool_Installation](Lab0_Tool_Installation/) |
| 1 | Inverter design flow: schematic, simulation, layout, LVS | [Lab1_inverter](Lab1_inverter/) |
| 2 | DRC and LVS fundamentals | [Lab2_fundamentals](Lab2_fundamentals/) |
| 3 | DRC issues and fixes | [Lab3_DRC](Lab3_DRC/) |
| 4 | LVS exercises | [Lab4_LVS](Lab4_LVS/) |

## Repository structure

Each lab folder has its own `README.md` with the objective, commands, screenshots, results, and the issues I hit along the way, plus an `images/` folder.



# Lab 0: Tool Installation and Setup

## Objective
Set up a Linux environment on Windows and install the tools needed for the labs: Magic, Netgen, Xschem, ngspice, and the sky130A PDK.

## Environment setup
I used WSL2 with a separate Ubuntu distro for these labs, so my other development environment stayed untouched.

## Tools installed

| Tool | Version | Purpose |
|------|---------|---------|
| Magic | 8.3.685 | Layout editor, DRC, extraction |
| Netgen | 1.5.325 | LVS |
| Xschem | 3.4.8RC | Schematic capture |
| ngspice | 42 | Circuit simulation |
| sky130A | via Volare | Process design kit |

## Steps
### Step 1: Check that GUI apps work
I ran `xeyes` to confirm graphics work in WSL.

![xeyes window](images/xeyes_gui_test.jpeg)

### Step 2: Install and verify the tools
(Add your commands, version outputs, and screenshots.)

## Issues faced and fixes

**1. Disk switched to read-only during a large download.**
Cause: heavy disk writes during the open_pdks download caused I/O errors. Fix: restarted WSL, let the filesystem recover, and installed the PDK with Volare instead of cloning every library.

**2. Magic closed immediately after starting.**
Cause: `sky130A.magicrc` pointed to a build folder that does not exist on my machine. Fix: changed `PDK_ROOT` to `/usr/local/share/pdk`.

**3. Magic menus missing.**
Cause: `sky130A.tcl` had the same hard-coded build path in `TECHPATH`. Fix: pointed it to the installed PDK.

**4. `BadAlloc` display error with `magic -d XR`.**
Fix: used `magic -d X11`.

## Author

Jyoshna Karri
