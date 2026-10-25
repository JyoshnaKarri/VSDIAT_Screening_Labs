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

# Lab 0: Tool Installation and Setup

## Objective
Set up a Linux environment on Windows and install the open-source tools needed for the physical verification labs: Magic, Netgen, Xschem, ngspice and the sky130A PDK.

## Environment
- Windows laptop with WSL2, using a separate Ubuntu distro for these labs so my other work environment stayed untouched.
- Terminal commands are run inside Ubuntu.

## Tools installed

| Tool | Version | Purpose |
|------|---------|---------|
| Magic | 8.3.685 | Layout editor, DRC, extraction |
| Netgen | 1.5.325 | LVS (layout vs schematic) |
| Xschem | 3.4.8RC | Schematic capture |
| ngspice | 42 | Circuit simulation |
| sky130A PDK | via Volare | Process design kit |

## Steps

### Step 1: Install build dependencies
```bash
sudo apt update
sudo apt install -y build-essential git x11-apps m4 tcsh csh libx11-dev tcl-dev tk-dev libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
```

### Step 2: Check that GUI apps work
I ran `xeyes` to confirm that graphical windows open from WSL.



### Step 3: Build and install Magic
```bash
git clone https://github.com/RTimothyEdwards/magic.git
cd magic
./configure
make
sudo make install
magic --version
```



### Step 4: Build and install Netgen
```bash
git clone https://github.com/RTimothyEdwards/netgen.git
cd netgen
./configure
make
sudo make install
```

### Step 5: Build and install Xschem and ngspice
```bash
git clone https://github.com/StefanSchippers/xschem.git xschem_git
cd xschem_git
./configure
make
sudo make install
xschem --version
sudo apt install -y ngspice
ngspice --version
```

### Step 6: Install the sky130A PDK
I used Volare, which downloads a prebuilt PDK, instead of cloning every library with open_pdks.

```bash
python3 -m venv ~/vsd-venv
source ~/vsd-venv/bin/activate
pip install volare
volare enable --pdk sky130 --pdk-root ~/pdk c6d73a35f524070e85faff4a6a9eef49553ebc2b
sudo mkdir -p /usr/local/share/pdk
sudo ln -s ~/pdk/volare/sky130/versions/c6d73a35f524070e85faff4a6a9eef49553ebc2b/sky130A /usr/local/share/pdk/sky130A
ls /usr/local/share/pdk/sky130A
```

The listing shows `libs.ref` and `libs.tech`, so the PDK is in place.

### Step 7: Verify the setup
Add a screenshot of Magic opening with the sky130A technology, and the version outputs for all tools.



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
