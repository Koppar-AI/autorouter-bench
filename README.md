# autorouter-bench

A benchmark for PCB autorouters on real, professionally routed open-hardware
boards, with KiCad as the referee.

Each router gets the same eight boards with their routing removed, the same
placement, the same design rules and the same wall-clock cap. What comes back
is scored by KiCad, never by the router:

- **Completion**: `100 × (1 − unconnected / connections)`, both counted by
  KiCad's ratsnest on the board the router returned.
- **DRC**: `kicad-cli pcb drc --severity-error` with the board's benchmark
  rules, with any zones the router drew refilled. Reported as the errors a router added over the
  human board's own findings (two upstream boards carry an unclosed outline or
  a courtyard overlap).
- **Vias, track length and wall-clock seconds**, as measured.

A router that reports 100% and leaves a pad stranded scores the stranded pad.

## The boards

| Board | Layers | Source | Licence |
| --- | --- | --- | --- |
| pic-programmer | 2 | [KiCad demos, tag 10.0.4](https://gitlab.com/kicad/code/kicad/-/tree/10.0.4/demos/pic_programmer) | GPL-3.0-or-later |
| rp2040-minimal | 2 | Raspberry Pi RP2040 minimal design, revision 2 ([archived download](https://web.archive.org/web/20240521000034/https://datasheets.raspberrypi.com/rp2040/Minimal-KiCAD.zip)) | Raspberry Pi design files |
| pico-vga | 4 (ground planes inside) | Raspberry Pi Pico VGA, SD and audio base ([archived download](https://web.archive.org/web/20211203134822/https://datasheets.raspberrypi.com/rp2040/VGA-KiCAD.zip)) | Raspberry Pi design files |
| cm5io | 4 | [Raspberry Pi CM5 IO board, revision 2](https://pip.raspberrypi.com/categories/1098-design-files) | Raspberry Pi design files |
| rk3328-som-evb | 4 | [OLIMEX RK3328-SOM-EVB](https://github.com/OLIMEX/RK3328-SOM-EBV/tree/0b6bb8aefd9b1f46acbfe0997752294316314ef4) | GPL-3.0 / CERN-OHL-1.2 |
| scalenode-cm4 | 4 | [Antmicro Scalenode CM4 baseboard](https://github.com/antmicro/scalenode-cm4-baseboard/tree/77f5bf281d13e43154cac9645f7cc22a82e56971) | Apache-2.0 |
| stmp157-som-evb | 4 | [OLIMEX STMP157-BASE-SOM-EVB](https://github.com/OLIMEX/STMP157-BASE-SOM-EVB/tree/75648b2100a4b125dc0a1575a7d5913c11e080d4) | GPL-3.0 |
| imx8mp-som-evb | 4 | [OLIMEX iMX8MP-SOM-EVB](https://github.com/OLIMEX/iMX8MP-SOM-EVB/tree/54724b6c9ba75aaab09046f3e3a27aca5d20024d) | GPL-3.0 |

No board is stored in this repository. `scripts/fetch_boards.py` downloads
each one from its pinned upstream source and checks it against
`boards/checksums.json`. The two older Raspberry Pi archives are fetched from
the Internet Archive, because the live URLs now serve a later revision.

The fetched board is loaded and saved once in KiCad 10, which upgrades the
file format and leaves the geometry alone. That is the human reference. The
input every router gets is its placement only: the tracks, vias and copper
zones are deleted, and the outline, footprints and keepout areas stay. Every
net is the router's to connect, ground included; a router may pour planes of
its own.

### The 25 public boards (set `zap25`)

The 25 boards Zap! (Mutual Solutions) published its comparison on
([zap.mutual.solutions/compare](https://zap.mutual.solutions/compare), measured
12-13 October 2026), pinned to the same commits and listed in
`boards/manifest-zap25.json`. They have no benchmark rules file: each board
runs under its own project's rules, as in that comparison. They are selected
with `BOARD_SET=zap25`; without it every script sees the eight boards above.
Two of them ship custom design rules (`.kicad_dru`: seven, stm32h7-hdmi-sodimm);
they are fetched beside the board as `circuit.kicad_dru`, so every router and the
referee judge by them. Koppar's run on this set, beside the numbers Zap! published
for every router, is `results/2026-10-zap25/summary.md`.

| Board | Layers | Source | Licence |
| --- | --- | --- | --- |
| cm4-lvds-adapter | 6 | [Antmicro CM4 baseboard LVDS adapter](https://github.com/antmicro/cm4-baseboard-lvds-adapter/tree/4af945ed558e58e4b8aea6fe909fc33d78b63f6f) | Apache-2.0 |
| ecp5-dc-scm | 8 | [Antmicro ECP5 DC-SCM](https://github.com/antmicro/ecp5-dc-scm/tree/0019313fd2e214f618788e5e61636a4a023ee361) | Apache-2.0 |
| ftdi-jtag-programmer | 4 | [FTDI JTAG programmer](https://github.com/anthony-bernaert/ftdi-jtag-programmer/tree/c33005ef528526c137ba8fd1e9cf4e8ceab63a1f) | CERN-OHL-P-2.0 |
| trellis-core | 4 | [Trellis Core](https://github.com/protolux-electronics/trellis_core/tree/db4fe71623c14bcea47d7457d0db4c99d3899124) | CERN-OHL-P-2.0 |
| bitaxe-ultra | 4 | [Bitaxe Ultra (fork)](https://github.com/BastelPichi/bitaxe/tree/0c3e71fd54fc0edef4c19c06d2320ef5468adc6a) | CERN-OHL-S-2.0 |
| ender3-loadcell | 2 | [Ender-3 load-cell bed-levelling sensor](https://github.com/jujojujo2003/Ender-3-3DPrinter-Load-Cell-Bed-Leveling-Sensor/tree/eae5c6f3e67d0b7f83a500bfb3d1aef38cb69b0b) | MIT |
| rp2040-devboard | 2 | [RP2040 development board](https://github.com/acornitum/fucked-up-rp2040-devboard/tree/d94328619f4fcaef2f2d62aa42c62c789a463d56) | MIT |
| discretesim-hwtest | 2 | [discretesim test board](https://github.com/cnlohr/discretesim/tree/f7a169ee07b18b6c857d23582474b8ba20185436) | MIT |
| water-level-monitor | 2 | [Arduino water-level monitor](https://github.com/Srushti-D-Hebbar/arduino-water-level-monitor/tree/7b47f46949e99d8075590de0c5a08a550d646d84) | MIT |
| ecp5-bga381-ft2232 | 4 | [ECP5 BGA-381 FT2232HQ FIFO board](https://github.com/gildobjanschi/ECP5_BGA381_FT2232HQ_FIFO_EXT/tree/81403f7487a9eded36c6500b8c8b6c12a6705f81) | MIT |
| emberone | 6 | [EmberOne](https://github.com/256foundation/emberone00-pcb/tree/b21b32ca49710b99cb75f86406b0df5190c9beb4) | CERN-OHL-S-2.0 |
| argos-demo | 4 | [Argos demo board](https://github.com/CNES/argos-demo-board/tree/1eccb3f20cb9004c046dba82b72bf85c500efcaa) | CERN-OHL-S-2.0 |
| rp2350-pico2-bb48 | 4 | [RP2350-PICO2-BB48](https://github.com/OLIMEX/RP2350-PICO2-BB48/tree/74b030363ca03eea5bfa6dac59cbcd9e4277e910) | MIT |
| cvbs-mipi-bridge | 4 | [Antmicro CVBS-to-MIPI bridge](https://github.com/antmicro/cvbs-mipi-bridge/tree/7cbcec2bceaf6e1efd25cce1d73ff4989dfcfe02) | Apache-2.0 |
| dual-ipex-csi-interposer | 4 | [Antmicro dual IPEX CSI interposer](https://github.com/antmicro/dual-ipex-csi-interposer/tree/6b6bd0af5aafe13c02377d534a23a6373922f350) | Apache-2.0 |
| gmsl-serializer | 4 | [Antmicro GMSL serializer](https://github.com/antmicro/gmsl-serializer/tree/58641df7b331050bbb4456cb4cb73e3975ae9de9) | Apache-2.0 |
| pmod-i3c-sensor | 4 | [Antmicro PMOD I3C sensor board](https://github.com/antmicro/pmod-i3c-sensor-board/tree/5ee5d34ff918422fe7af59f7ffdc9d4bdabf18a7) | Apache-2.0 |
| si-test-board | 4 | [Antmicro signal-integrity test board](https://github.com/antmicro/signal-integrity-test-board/tree/de0b5922c372481bb146cbd1d0a9f3b7e97c124a) | Apache-2.0 |
| stm32h7-hdmi-sodimm | 6 | [Antmicro STM32H7 HDMI SO-DIMM board](https://github.com/antmicro/stm32h7-hdmi-board-sodimm/tree/27e3ac9968983f236155c288ded30beb1a2d24a1) | Apache-2.0 |
| tiliqua-motherboard | 6 | [Tiliqua (apfaudio)](https://github.com/apfaudio/tiliqua-hardware/tree/4ee5878ae821a6b7096f6aed6795dc1349475cb5) | CERN-OHL-S-2.0 |
| buildbotics-controller | 4 | [Buildbotics controller](https://github.com/buildbotics/bbctrl-pcb-new/tree/1a2f36ddc4797ac05e45405fb5664ff1f7ca7974) | CERN-OHL-S-2.0 |
| hackrf-pro | 6 | [HackRF Pro](https://github.com/greatscottgadgets/hackrf-pro/tree/359b98f2451395408bc25dae64efa9fc518e93d0) | CERN-OHL-P-2.0 |
| seven | 4 | [Seven](https://github.com/id8-engineering/seven-hardware/tree/7c69a1482ffd1dddc206294a55602477c55e17d8) | CERN-OHL-P-2.0 |
| kintex-pcie | 8 | [Kintex PCIe board](https://github.com/piotr-binkowski/kintex-pcie-board/tree/056792c009a8920d4ef11e76ba3284ee58376078) | Apache-2.0 |
| xerxes | 6 | [Xerxes](https://github.com/rapidanalysis/xerxes/tree/43abf5730d092358bc6d10e9faa7233818b5412e) | Apache-2.0 |

### The benchmark rules

`boards/rules/<board>.json` lists every change from the upstream project's
rules; the fetch script applies exactly that, and every router and the DRC
referee get the result. The changes set one floor (0.1 mm clearance and tracks
on the 4-layer carriers) and drop the impedance classes and cm5io's PoE
spacing, so the table measures routing under that floor, not each design's own
constraints. The 25-board set runs under each board's own rules.

### PCBWorld-Bench

The real-board test sets of [PCBWorld](https://github.com/LGAI-Research/PCBWorld)
(LG AI Research): D3-A (99 boards) and D3-B (10), built from the public PCBench
collection by PCBWorld's own preparation chain. `pcbworld/` holds the script that
builds them and the clean-pass scorer; `pcbworld/README.md` says how.

## Running it

Needs Linux, KiCad 10 (`kicad-cli` and a python that imports `pcbnew`),
Python 3.10+ and Node 22+.

```sh
export KICAD_PYTHON=/usr/bin/python3        # a python that imports pcbnew
python3 scripts/fetch_boards.py             # the eight boards, checked and prepared
BOARD_SET=zap25 python3 scripts/fetch_boards.py   # the 25 public boards of Zap!'s comparison

tools/install.sh freerouting                # Freerouting 2.5.0 and Java 25
tools/install.sh node                       # tscircuit 0.0.979, KiCad Routing Tools 0.1.9
tools/install.sh tracemaker                 # TraceMaker 0.9.0, built from source (CUDA)

python3 harness/run.py freerouting          # or tscircuit, krt, tracemaker, koppar, koppar_filled, zap; optional board names
python3 scripts/collect.py                  # results/<campaign>/summary.md
```

`CAP_S` sets the wall-clock cap per board (default 1200 s). Results merge by
board into `results/<campaign>/<tool>.json`.

## How each router is run

- **Freerouting 2.5.0**: the board exported to Specctra DSN by KiCad, routed
  with `-mp 100 -mt 8`, and the session imported back by KiCad. Freerouting
  writes its result only when it finishes, so a run past the cap has no board
  to score.
- **tscircuit capacity autorouter 0.0.979**: the board as a SimpleRouteJson
  (KiCad's bounding box for every pad, hole, copper graphic and keepout; one
  connection per net, ground included), routed with
  `AutoroutingPipelineSolver`, and the returned traces written back onto the
  board as returned.
- **KiCad Routing Tools 0.1.9** (`@tscircuit/krt-wasm`): the same input, on a
  0.05 mm grid with the board's default clearance. The package routes a whole
  board or nothing: when it gives up inside the cap, the harness routes one net
  at a time with the copper routed so far as obstacles and keeps what closes.
  The package does not include the project's rip-up and reroute, which is
  Python; results here are for the WASM router core only.
- **TraceMaker 0.9.0**: reads and writes KiCad boards directly, given the cap
  as its time limit.
- **Koppar**: a hosted service. Its results are produced by the service on the
  same machine, with the same inputs and cap, and scored by the same
  collector. `harness/run.py koppar` sends a board and its project to the public
  endpoint at tools.koppar.ai; a board past 300 connections needs an account API
  key, read from `KOPPAR_API_KEY`. `koppar` keeps every via out of pin pads (the
  default); `koppar_filled` lets vias sit in pin pads, for a board ordered with
  filled and capped vias.

- **Zap!** (Mutual Solutions): a hosted service. `harness/run.py zap` sends the
  board and its project to zap.mutual.solutions with `fab_floor=board` (the
  board's rules, as every other tool gets) and the service defaults otherwise
  (its own pours, no vias in pads). Time is the job's run time on the service,
  not its queue; a job still running at the cap is cancelled. The API key is
  read from `ZAP_KEY_FILE` (default `~/.zap-key`).

Every router runs with its defaults and the board's rules. A router's author
may know settings that do better; the harness is here so anyone can show it.

## Results

`results/2026-10-placement/summary.md` is the October 2026 campaign: one workstation
(24 cores, one RTX 5090), 1200 s per board, KiCad 10.0.4 as referee. How each
column was produced, and what it does not score, is in
`results/2026-10-placement/NOTES.md`.

Boards fully routed (100% completion) with no DRC error added, out of eight:

| Router | Boards |
| --- | --- |
| Koppar | 8 |
| Koppar (filled vias) | 8 |
| TraceMaker 0.9.0 | 5 |
| Zap! | 3 |
| Freerouting 2.5.0 | 0 |
| tscircuit 0.0.979 | 0 |
| KiCad Routing Tools 0.1.9 | 0 |

### The 25 public boards

`results/2026-10-zap25/summary.md`: Koppar, one run per board (measured
2026-10-18), beside the numbers Zap! published for itself, TraceMaker, Freerouting
and tscircuit (which we did not re-run). Each board under its own rules.

| Router | Fully connected | Clean (0 open, 0 errors) | Connected, no more errors than the human board |
| --- | --- | --- | --- |
| Koppar | 12 | 9 | 12 |
| Zap! | 14 | 6 | 9 |
| TraceMaker | 7 | 3 | 4 |
| Freerouting | 11 | 2 | 2 |
| tscircuit | 10 | 0 | 0 |

### PCBWorld-Bench

`results/pcbworld-2026-10/summary.md`: clean-pass rate, one attempt per board.
Koppar 1.000 on D3-A and 1.000 on D3-B; DeepPCB reports 0.929 and 0.800, and the
PCBWorld paper's baselines are lower (the full table, as DeepPCB published it, is
in the summary).

## Electrical quality

Completion is not quality. `scripts/quality.py` measures, on every routed board and the
human reference alike: the share of high-speed track over a ground plane (and over any
plane), ground vias beside high-speed layer changes, differential pair length mismatch and
the share routed side by side, the narrowest track on each power net, and the routed path
from each decoupling capacitor to its part (length and vias). `scripts/quality_campaign.py`
runs it over a campaign: `results/2026-10-placement/quality.md`.

Nets are classified by name (pairs by `_P`/`_N`-style suffixes, clocks by `CLK`, rails by
voltage-style names); the patterns are in the script.

## What this does not measure

Current is not stated on these boards, so rail widths are reported, not judged against a
current. Impedance needs each board's stackup and is not scored. No router in the table
matches the human layouts on every measure.

## Licence

The code in this repository is MIT licensed. The boards are not part of it;
each keeps its upstream licence.
