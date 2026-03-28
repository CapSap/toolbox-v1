# Linkage mechanism spec

## Overview

An isosceles two-bar linkage where two rigid rods of equal length m meet at a vertex P3, with their other ends at P1 and P2. The goal is to understand the feasible region of the free parameters (x, y, m) subject to constraints.

## Coordinate system

- Origin at (0, 0)
- All units in mm
- Y-axis: positive up, negative down

## Points

| Point  | Position          | Notes                          |
|--------|-------------------|--------------------------------|
| Origin | (0, 0)            | Reference point                |
| P1     | (x, −y)           | Below axis, right of origin    |
| P2     | (286 − x, y)      | Above axis, right of origin    |
| P3     | Derived            | Vertex where the two rods meet |

P1 and P2 are always symmetric about the midpoint (143, 0) horizontally, but antisymmetric vertically (P1 at −y, P2 at +y).

## Links

- Rod 1: P1 → P3, length = m
- Rod 2: P2 → P3, length = m (same as rod 1)
- No rod connects P1 to P2 directly; the 286mm span is a layout dimension, not a physical link

## Free parameters

| Parameter | Range     | Description                              |
|-----------|-----------|------------------------------------------|
| x         | [39, 78]  | Horizontal offset of P1 from origin      |
| y         | > 0       | Vertical offset magnitude for P1 and P2  |
| m         | ≥ m_min   | Rod length (equal for both rods)          |

## Derived values

**Half-distance between P1 and P2:**

    d_half = √((286 − 2x)² + (2y)²) / 2

**Minimum rod length** (P3 collapses onto the P1–P2 midpoint):

    m_min = d_half

**P3 position** (lies on the perpendicular bisector of segment P1–P2):

    midpoint = (143, 0)
    perpendicular direction (normalised) = (−2y, 286 − 2x) / (2 · d_half)
    h = √(m² − d_half²)
    P3 = midpoint ± h · perpendicular direction

There are two solutions for P3 (one on each side of the P1–P2 line). Both are geometrically valid; the choice depends on the physical application.

## Constraints

1. **x range**: 39 ≤ x ≤ 78
2. **Rod length**: m ≥ m_min (otherwise P3 does not exist)
3. **Depth constraint**: |y₃| < y (P3 must stay within the vertical band defined by P1 and P2's y-offsets)

## Key geometric properties

- The horizontal distance between P1 and P2 is always 286 − 2x (ranges from 130mm to 208mm as x goes from 78 to 39)
- The full diagonal distance between P1 and P2 is 2 · d_half = √((286 − 2x)² + 4y²)
- x does not affect the vertical geometry — it only shifts how far apart P1 and P2 are horizontally
- Larger y increases the P1–P2 span and therefore increases m_min
- Larger m pushes P3 further from the P1–P2 line along the perpendicular bisector
- The depth constraint |y₃| < y limits how large m can be relative to the geometry