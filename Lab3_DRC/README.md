# Lab 3: DRC Issues

## Objective
Find and fix design rule violations in Magic using the sky130A rules, and check density rules.

## Tools
Magic 8.3.685 with the sky130A tech file.

## Method
For each exercise I loaded the layout, ran DRC, read the violation with `drc why`, fixed the layout, and checked again until the error count reached 0.

```
drc style drc(full)
drc check
drc why
drc find
```

## Exercises
| Exercise | Rule | 
|----------|------|
| 1 | Width, spacing, notch | 
| 2 | Vias | 
| 3 | Minimum area and hole | 
| 4 | Wells and deep nwell | 


## Density check
I ran `check_density.py` on `exercise_11.gds`. It reported that the layout is smaller than 700 µm x 700 µm, so the density check cannot run on it. I also ran `generate_fill.py` on the GDS file. Passing the `.mag` file gave "Project is not a GDS file!", so it needs the GDS.

## Issues faced and fixes
- `Project is not a GDS file!`: the script needs a `.gds` input, not a `.mag` file.
- `getcell ... couldn't be read`: the fill file did not exist because the script had failed.


