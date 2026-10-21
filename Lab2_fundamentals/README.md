# Lab 2: DRC on AND2_1 Standard Cell

## Objective
Run Design Rule Check on sky130_fd_sc_hd__and2_1 using Magic.

## Commands
gds read /usr/local/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/gds/sky130_fd_sc_hd.gds
load sky130_fd_sc_hd__and2_1
drc style drc(full)
drc check
drc why

## Result
No errors found.


