# Campaign 2026-10-placement

Every router got the placement only: tracks, vias and copper zones removed, keepout areas kept,
every net (ground included) left to the router; 1200 s per board, one workstation (24 cores,
one GPU), KiCad 10.0.4 as referee. Runs on 2026-10-14 and 2026-10-15; the Koppar rows, both
modes, on 2026-10-16, from one build.

- Freerouting 2.5.0, tscircuit 0.0.979, KiCad Routing Tools 0.1.9, TraceMaker 0.9.0 and Zap!
  were run with this repository's harness.
- Koppar is a hosted service; its boards were produced on the same machine, from the same
  fetched boards, and scored by the same collector. It was run in two modes, both reported:
  `koppar` keeps every via out of pin pads (the default; the board needs no special fab
  process), and `koppar_filled` lets vias sit in pin pads, for a board ordered with filled and
  capped vias (the extra-cost process the via-in-pad column refers to).
- Zap! (Mutual Solutions, hosted; service 2026.10.14.60) was run with `harness/run.py zap`:
  `fab_floor=board`, service defaults otherwise, cancelled at the cap. It refused scalenode-cm4
  (`footprints_outside_board`: footprint M1 lies off the outline in the human design) and was
  cancelled at 1200 s on cm5io and imx8mp-som-evb.
- `finishedAtS`: when a tool reached the board it returned (Koppar: the first time the scored
  board's count was reached; Freerouting: its best-scoring pass; TraceMaker: its winning
  variant's end, an upper bound since a finished variant keeps cleaning up until the limit;
  tscircuit, KiCad Routing Tools and Zap!: their run time). `seconds`: how long the run took.
- A Koppar run that goes past the cap is scored on the last board it saved inside the cap; no
  run in these rows went past it.
- Vias in pin pads (SMD pads under 2 mm across, counted with `scripts/habits.py`): a via there
  needs a filled and capped via at the fab, and KiCad's DRC does not flag a via in its own
  net's pad. Koppar 0 on every board; Koppar (filled vias) 1 to 379; TraceMaker (its defaults)
  14 to 200 per board; KiCad Routing Tools 0 to 61; Freerouting, tscircuit and Zap! 0 to 1.
  `viasInPinPads` in each tool's results.
- Not scored: plane integrity. TraceMaker, Freerouting, tscircuit and KiCad Routing Tools pour
  no planes (ground is routed as tracks); Koppar and Zap! pour ground planes.
