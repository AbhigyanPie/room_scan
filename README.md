# roomscan

Phone capture → dimensioned, stitched floor plan with intervals on every number, at three
input tiers (LiDAR, video, photos). Capture route: **stock apps** (`docs/capture_protocol.md`).

## Fresh machine to first plan (≈10 min)

```bash
git clone <this repo> && cd roomscan
python3 -m venv .venv && source .venv/bin/activate      # Python 3.10–3.12
pip install -r requirements.txt                          # ~3 min, no GPU, no downloads at run time
python -m roomscan run <capture> --out out/demo          # one command per capture
open out/demo/plan.png                                   # plan.json, plan.svg, ortho/ next to it
```

`<capture>` is a Stray Scanner export folder (LiDAR), a `.MOV/.mp4` file (video) or a folder of
per-room photo folders (photo). The tier is auto-detected; force it with `--tier`.

Options: `--no-drift` (ablation: poses as-is), `--no-damage`, `--step N` (LiDAR frame stride).
Optional dense depth for video/photo: `bash scripts/fetch_weights.sh` then export
`ROOMSCAN_DEPTH_MODEL` (disclosed pretrained model; off by default, live path needs nothing).

## Layout

| Path | What |
|---|---|
| `roomscan/io_stray.py` | Stray loader; pose convention pinned empirically (`tools/check_convention.py`) |
| `roomscan/fuse.py` | confidence-filtered depth → world points + normals, time-chunked |
| `roomscan/drift.py` | plane-anchored chunk pose graph (drift accountability) |
| `roomscan/layout.py` | Manhattan frame, floor, wall faces, room segmentation, orthogonal polygons |
| `roomscan/measure.py` | per-room floor/ceiling levels, openings on wall elevation grids |
| `roomscan/plan.py` | rooms → measured, non-overlapping, adjacency, typing (shared by all tiers) |
| `roomscan/intervals.py` | error budget + calibration factors → 95% intervals |
| `roomscan/damage.py` | surface orthophotos, damage proposals, concealed-damage rules, scope |
| `roomscan/mono.py`, `tier_video.py`, `tier_photo.py` | SfM, gravity, metric scale, camera-only tiers |
| `tools/` | evaluate (gates), calibrate, repeatability, ablation, head-to-head, schema check |
| `schema/plan.schema.json` | published output schema |
| `docs/` | capture protocol, device matrix, compliance matrix, technical report, fix loop |

## Reproducing the benchmark

```bash
bash scripts/run_benchmark.sh data/ out/       # every capture, drift on + off, all tools
```

Every number in `docs/technical_report.md` is produced by that script from raw captures in
`data/` and ground truth in `benchmark/ground_truth/`. Runs are deterministic (fixed seeds, no
model calls on the default path).
