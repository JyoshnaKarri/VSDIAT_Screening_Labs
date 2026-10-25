# Lab 4: LVS Exercises

## Objective
Compare layout and schematic netlists with Netgen, and learn to read mismatches in `comp.out`.

## Tools
Netgen 1.5.325 with `sky130A_setup.tcl`.

## Method
```bash
netgen -batch lvs "netA.spice test" "netB.spice test" sky130A_setup.tcl comp.out -json | tee lvs.log
```

For every exercise I ran the comparison, opened `comp.out`, and noted whether I got a match, a net mismatch or a device mismatch.

## Exercises
| Exercise | What it shows | 
|----------|---------------|
| 1 | Net and device mismatch | 
| 2 | Subcircuit comparison, pin order | 
| 3 | Black-box cells and `-blackbox` | 
| 4 | Permuting pins |
| 5 to 9 | Real designs, fill cells, diodes, property errors |


