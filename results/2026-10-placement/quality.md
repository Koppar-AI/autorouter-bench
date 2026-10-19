# Quality, campaign 2026-10-placement

Measured with `scripts/quality.py` on each routed board; `human` is the upstream design. A dash: not measured (no board, or nothing of that kind on it).

## High-speed track over a ground plane (% of length)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | — | — | — | — | — | — | — | — |
| rp2040-minimal | 98.7% | 83.3% | 74.4% | 0.0% | 0.6% | 0.4% | — | 81.8% |
| pico-vga | 87.5% | 0.7% | 0.0% | 0.7% | 0.7% | 0.7% | 0.7% | 97.7% |
| cm5io | 97.2% | 65.3% | 63.8% | 0.4% | no board | — | 1.6% | 97.2% |
| rk3328-som-evb | 77.6% | 59.4% | 62.7% | 1.0% | 1.2% | 0.7% | 0.7% | 94.4% |
| scalenode-cm4 | 74.2% | 44.9% | 56.2% | 1.5% | no board | 1.5% | 1.4% | 95.2% |
| stmp157-som-evb | 47.6% | 38.6% | 44.6% | 1.6% | no board | — | 0.0% | 90.0% |
| imx8mp-som-evb | 56.0% | 41.2% | 49.0% | 0.6% | no board | 1.3% | 0.0% | 93.2% |

## High-speed track over any plane (% of length)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | — | — | — | — | — | — | — | — |
| rp2040-minimal | 98.7% | 83.3% | 74.4% | 0.0% | 0.6% | 0.4% | — | 84.3% |
| pico-vga | 87.5% | 85.9% | 90.8% | 0.7% | 0.7% | 0.7% | 0.7% | 97.7% |
| cm5io | 97.2% | 65.3% | 63.8% | 0.4% | no board | — | 1.6% | 97.2% |
| rk3328-som-evb | 90.1% | 86.6% | 86.6% | 1.0% | 1.2% | 0.7% | 0.7% | 94.4% |
| scalenode-cm4 | 90.2% | 74.4% | 80.7% | 1.5% | no board | 1.5% | 1.4% | 95.2% |
| stmp157-som-evb | 92.5% | 72.4% | 75.1% | 1.6% | no board | — | 0.0% | 90.0% |
| imx8mp-som-evb | 92.8% | 74.8% | 77.9% | 0.6% | no board | 1.3% | 0.0% | 93.2% |

## High-speed vias with a ground via within 1.5 mm (%)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | — | — | — | — | — | — | — | — |
| rp2040-minimal | — | 100.0% | 100.0% | — | 0.0% | 0.0% | — | 83.3% |
| pico-vga | — | 0.0% | 0.0% | 0.0% | — | 0.0% | — | — |
| cm5io | 100.0% | 75.5% | 75.7% | 16.4% | no board | — | 0.0% | 92.9% |
| rk3328-som-evb | 16.7% | 62.7% | 40.0% | 4.1% | 0.0% | 15.0% | 0.0% | 70.6% |
| scalenode-cm4 | 43.1% | 73.0% | 65.4% | 6.1% | no board | 12.2% | 0.0% | 83.7% |
| stmp157-som-evb | 6.7% | 51.7% | 38.3% | 6.9% | no board | — | 0.0% | 61.4% |
| imx8mp-som-evb | 9.8% | 43.8% | 63.3% | 6.2% | no board | 7.1% | 0.0% | 78.2% |

## Differential pairs: median length mismatch (mm)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | — | — | — | — | — | — | — | — |
| rp2040-minimal | 0.104 | 0.443 | 0.384 | 0.14 | 0.151 | 0.104 | — | 0.095 |
| pico-vga | — | — | — | — | — | — | — | — |
| cm5io | 0.04 | 0.0 | 0.0 | 1.824 | no board | — | — | 0.494 |
| rk3328-som-evb | 0.0 | 0.01 | 0.262 | 0.617 | 3.302 | 1.21 | 3.372 | 0.166 |
| scalenode-cm4 | 0.018 | 0.003 | 0.001 | 1.477 | no board | 3.106 | 3.917 | 0.134 |
| stmp157-som-evb | 0.0 | 0.142 | 0.968 | 1.36 | no board | — | 4.203 | 0.788 |
| imx8mp-som-evb | 0.0 | 0.01 | 0.01 | 1.678 | no board | 2.014 | 0.896 | 0.228 |

## Differential pairs: median share routed side by side (%)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | — | — | — | — | — | — | — | — |
| rp2040-minimal | 100.0% | 100.0% | 96.0% | 4.3% | 0.0% | 0.0% | — | 98.9% |
| pico-vga | — | — | — | — | — | — | — | — |
| cm5io | 92.8% | 57.35% | 66.0% | 0.3% | no board | — | — | 22.3% |
| rk3328-som-evb | 87.1% | 54.0% | 66.0% | 5.7% | 14.5% | 9.9% | 0.0% | 77.9% |
| scalenode-cm4 | 94.5% | 45.75% | 64.0% | 4.1% | no board | 4.1% | 0.7% | 67.3% |
| stmp157-som-evb | 82.1% | 48.3% | 50.35% | 2.1% | no board | — | 35.5% | 39.75% |
| imx8mp-som-evb | 84.4% | 50.4% | 66.3% | 9.0% | no board | 6.6% | 7.0% | 60.4% |

## Decoupling: median track path, capacitor to pin (mm)

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | 35.12 | 39.56 | — | 17.25 | 35.0 | 17.25 | 17.25 | — |
| rp2040-minimal | 2.595 | 7.17 | 7.47 | 3.06 | 3.9 | 3.15 | 8.61 | 2.46 |
| pico-vga | 4.07 | 10.17 | 11.37 | 5.89 | 5.23 | 5.89 | 14.2 | 5.52 |
| cm5io | 4.18 | 4.17 | 8.915 | 5.63 | no board | — | — | 1.92 |
| rk3328-som-evb | 4.38 | 11.99 | 12.365 | 4.43 | 4.17 | 5.89 | — | 1.45 |
| scalenode-cm4 | 1.86 | 5.41 | 5.07 | 5.3 | no board | 7.015 | — | 1.34 |
| stmp157-som-evb | 4.58 | 17.77 | 12.565 | 5.39 | no board | — | 84.39 | 3.53 |
| imx8mp-som-evb | 2.7 | 4.405 | 3.905 | 1.795 | no board | 3.19 | 35.7 | 1.45 |

## Decoupling: median vias on that path

| Board | human | koppar | koppar_filled | tracemaker | freerouting | tscircuit | krt | zap |
|---|---|---|---|---|---|---|---|---|
| pic-programmer | 0 | 0 | — | 0 | 0 | 0 | 0 | — |
| rp2040-minimal | 0.0 | 2 | 0 | 0 | 0 | 0 | 0 | 0.0 |
| pico-vga | 0.0 | 0 | 0.0 | 0 | 0.0 | 0 | 0.0 | 0 |
| cm5io | 0 | 0.0 | 0.0 | 1 | no board | — | — | 0.0 |
| rk3328-som-evb | 0 | 0 | 0.0 | 0 | 0 | 0.0 | — | 0 |
| scalenode-cm4 | 0.0 | 0 | 0 | 0.0 | no board | 0.5 | — | 0.0 |
| stmp157-som-evb | 0.0 | 3 | 2.0 | 0.0 | no board | — | 4 | 0.0 |
| imx8mp-som-evb | 0 | 0.0 | 0.0 | 0.0 | no board | 0.0 | 0 | 0 |
