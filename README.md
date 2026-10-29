# MOT_TbD_ByteTrack

**ByteTrack** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Zhang et al., ECCV 2022; official code: `ifzhang/ByteTrack`
- Principle: two-stage association: high-score then low-score detections
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`bytetrack`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (ByteTrack, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | 0.565 | 0.526 | 0.612 | 0.625 | 0.718 | 134 | 0.647 | 0.483 | 0.34 | 35.2 | 0.625 |
| libra_rcnn | 0.542 | 0.500 | 0.595 | 0.531 | 0.679 | 184 | 0.641 | 0.444 | 0.40 | 26.9 | 0.599 |
| faster_rcnn | 0.524 | 0.485 | 0.574 | 0.546 | 0.674 | 166 | 0.624 | 0.424 | 0.38 | 25.3 | 0.582 |
| dynamic_rcnn | 0.521 | 0.481 | 0.569 | 0.526 | 0.671 | 161 | 0.612 | 0.431 | 0.36 | 25.3 | 0.579 |
| atss | 0.505 | 0.454 | 0.567 | 0.522 | 0.668 | 94 | 0.605 | 0.405 | 0.39 | 22.1 | 0.527 |
| gfl | 0.504 | 0.439 | 0.582 | 0.526 | 0.658 | 60 | 0.590 | 0.418 | 0.31 | 21.1 | 0.522 |
| retinanet | 0.500 | 0.453 | 0.556 | 0.537 | 0.658 | 120 | 0.581 | 0.418 | 0.32 | 21.4 | 0.535 |
| v6 | 0.493 | 0.432 | 0.570 | 0.514 | 0.642 | 76 | 0.609 | 0.377 | 0.33 | 6.9 | 0.509 |
| tood | 0.482 | 0.434 | 0.539 | 0.509 | 0.628 | 105 | 0.604 | 0.360 | 0.32 | 25.1 | 0.506 |
| fcos | 0.482 | 0.406 | 0.577 | 0.477 | 0.626 | 53 | 0.591 | 0.372 | 0.34 | 21.9 | 0.493 |
| deformable_detr | 0.462 | 0.401 | 0.539 | 0.467 | 0.622 | 85 | 0.562 | 0.363 | 0.33 | 68.6 | 0.482 |
| ppyoloe | 0.460 | 0.409 | 0.524 | 0.468 | 0.595 | 113 | 0.606 | 0.315 | 0.35 | 6.7 | 0.487 |
| x | 0.443 | 0.380 | 0.522 | 0.441 | 0.586 | 101 | 0.576 | 0.309 | 0.31 | 5.8 | 0.478 |
| rtmdet | 0.442 | 0.377 | 0.522 | 0.454 | 0.586 | 73 | 0.586 | 0.298 | 0.31 | 6.5 | 0.465 |
| v10 | 0.441 | 0.380 | 0.515 | 0.463 | 0.578 | 67 | 0.576 | 0.306 | 0.30 | 8.1 | 0.455 |
| x2 | 0.438 | 0.372 | 0.519 | 0.442 | 0.582 | 64 | 0.582 | 0.293 | 0.32 | 5.3 | 0.452 |
| v8 | 0.437 | 0.364 | 0.533 | 0.441 | 0.571 | 56 | 0.585 | 0.289 | 0.28 | 5.6 | 0.443 |
| v9 | 0.436 | 0.366 | 0.523 | 0.429 | 0.561 | 59 | 0.582 | 0.290 | 0.27 | 12.2 | 0.460 |
| v12 | 0.419 | 0.333 | 0.532 | 0.394 | 0.543 | 51 | 0.551 | 0.287 | 0.28 | 8.7 | 0.424 |
| v11 | 0.417 | 0.337 | 0.523 | 0.397 | 0.534 | 56 | 0.580 | 0.253 | 0.28 | 6.7 | 0.435 |
| centernet | 0.394 | 0.303 | 0.518 | 0.379 | 0.530 | 23 | 0.496 | 0.292 | 0.25 | 7.8 | 0.395 |
| v26 | 0.383 | 0.316 | 0.473 | 0.385 | 0.504 | 43 | 0.569 | 0.197 | 0.28 | 9.1 | 0.390 |
| fairmot | 0.380 | 0.306 | 0.474 | 0.378 | 0.513 | 29 | 0.508 | 0.253 | 0.27 | 8.5 | 0.387 |
| v13 | 0.353 | 0.299 | 0.428 | 0.358 | 0.449 | 62 | 0.569 | 0.138 | 0.28 | 10.9 | 0.372 |
| v1 | 0.330 | 0.309 | 0.358 | 0.342 | 0.434 | 188 | 0.458 | 0.201 | 0.28 | 6.2 | 0.374 |
| ssd | 0.282 | 0.239 | 0.373 | 0.283 | 0.356 | 74 | 0.516 | 0.048 | 0.25 | 29.5 | 0.288 |

### Score-threshold sensitivity (ByteTrack, HOTA with one common threshold)

| detector | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 |
|---|---|---|---|---|---|
| deformable_detr | 0.476 | 0.468 | 0.462 | 0.446 | 0.396 |
| faster_rcnn | 0.515 | 0.520 | 0.524 | 0.528 | 0.533 |
| fcos | 0.503 | 0.500 | 0.482 | 0.450 | 0.408 |
| libra_rcnn | 0.528 | 0.537 | 0.542 | 0.545 | 0.547 |
| ppyoloe | 0.463 | 0.468 | 0.460 | 0.432 | 0.391 |
| rtmdet | 0.467 | 0.461 | 0.442 | 0.395 | 0.320 |
| v10 | 0.465 | 0.453 | 0.441 | 0.415 | 0.360 |
| v11 | 0.445 | 0.440 | 0.417 | 0.386 | 0.321 |
| v12 | 0.447 | 0.443 | 0.419 | 0.382 | 0.250 |
| v13 | 0.378 | 0.368 | 0.353 | 0.326 | 0.268 |
| v26 | 0.415 | 0.408 | 0.383 | 0.304 | 0.239 |
| v6 | 0.504 | 0.509 | 0.493 | 0.468 | 0.441 |
| v8 | 0.454 | 0.451 | 0.437 | 0.404 | 0.353 |
| v9 | 0.459 | 0.452 | 0.436 | 0.421 | 0.352 |
| x | 0.450 | 0.450 | 0.443 | 0.435 | 0.368 |
| x2 | 0.460 | 0.451 | 0.438 | 0.400 | 0.335 |

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers bytetrack --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: bytetrack)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
