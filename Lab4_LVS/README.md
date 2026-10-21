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
| Exercise | What it shows | Result |
|----------|---------------|--------|
| 1 | Net and device mismatch | ___ |
| 2 | Subcircuit comparison, pin order | ___ |
| 3 | Black-box cells and `-blackbox` | ___ |
| 4 | Permuting pins | ___ |
| 5 to 9 | Real designs, fill cells, diodes, property errors | ___ |


