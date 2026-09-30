# Metadata: DATA_no-vaccum_no-water (bench session 28 Sep 2026)

One row per file in this folder. The files are renamed copies of the DigiVision summary exports (`.sum.xlsx`); the original file names are inside each file and in `Methods_Data_Analysis/Bench_2026-09-28/raw_xlsx/FILE_MAP_original_to_copy.csv`. The notes come from the run sheet, clarified with the session records (`Dataset_2026-09-28.md`, `Deviations_2026-09-28.md`, `LOGBOOK_2026-09-28.md`).

## Session conditions (apply to every file)

- **Device state:** A: water jet off, vacuum off (WAL unit out of service); hoses attached and held by hand, not taped
- **Acquisition:** DigiVision, **100 Hz**, channel 01, device #271; burster 8438-5100 ring load cell (±100 N); unit N. Checked: the number of samples per file matches its length × 100 Hz
- **File structure:** Sheet 1 is an overview (original path). Sheet 2 has a header (start time, part number = file number), then columns Counter, Time [sec] and Measured value [N]
- **Cannula:** body-jet WAL cannula, 3.8 × 0.25 × 300 mm, 4 suction holes
- **Cue:** acoustic cue track 1.9 Hz, 80 s, for all stroking runs (expect a stroke fundamental near 1.9 Hz)
- **Stroke length:** 80 mm, except R33–R35 (40 mm by mistake)
- **Tare:** once at 14:00, never repeated. Baselines drift (C01 0.25 N to C08 2.44 N) and jump after each reseating of the sensor: **subtract a per-run baseline**
- **Recording length:** about 80–90 s per block run; the start of a run can include set-up before stroking begins, so use an activity detector
- **Recurring artefacts:** (1) the sensor housing coming out of its seat (a drop and then a spike on reseating, often with a baseline shift); (2) the cannula hitting the metal housing or frame (isolated sharp spike). Both are marked per file below
- **Time order:** Blocks were run as P4 → P5 → P1 → P2 → P3 (D4), so material is confounded with session time; keep the start time as a covariate
- **Suspected:** gelatin clogging inside the cannula lumen, noticed on 29 Sep; onset on 28 Sep unknown
- **Excluded from this folder:** taped vacuum-hole files 00010–00034 (void, D1); unlogged or aborted files; R22 (lost, see FLAGGED_FOR_REVIEW.txt)

## Blocks

Cast dates, acid, dimensions and spacing as in the uploaded run sheet (block log, section 3). Age = time from casting to the test on 28 Sep 2026.

| Block | Formulation | Cast | Age at test | Acid | W × L × H (mm) | Insertion spacing | Notes |
|---|---|---|---|---|---|---|---|
| P1-B1 | 6 % gelatin | 15 Aug 2026 | about 6 weeks | none | 110 × 160 × 30 | 15 mm | chipping loss |
| P2-B1 | 8 % gelatin | 26 Aug 2026 | about 1 month | none | 200 × 260 × 80 | 15 mm | free-standing block; chipping loss |
| P3-B1 | 8 % gelatin + lobules | 26 Aug 2026 | about 1 month | none | 112 × 120 × 50 | 15 mm | sticky note on the block wrongly reads 'P2-B1'; chipping loss |
| P4-B1 | 6 % gelatin + 1 % chitosan | December 2025 | about 9–10 months | citric acid | 110 × 160 × 30 | 15 mm | cracks across the top after testing (photo 17:02); chipping loss |
| P5-B1 | complete composite (P4 matrix + lobules + microhollow spheres) | December 2025 | about 9–10 months | citric acid | 80 × 170 × 20 | 10 mm | thin block; entry end chipped; chipping loss |

**Age confound:** the two chitosan blocks (P4, P5) are about 9–10 months old; P1–P3 are 1–1.5 months old. Chitosan network and block age cannot be separated in this session, so any P4/P5 vs P1–P3 difference (contrasts C3, C4 and the RQ4 ranking) must be reported with this limitation.

**Block mass (column removed):** mass was not recorded consistently (before-mass missing for P3 and P4, after-mass missing for P3), so it is left out of this table. It matters for later analysis because:
- **Material loss per block** (before − after, as g and % of the block): the cannula chips material out, and a larger loss means the tunnels widen and later insertions meet less material. This can explain a rise or fall in force fluctuation across rounds R1 to R4 within a block.
- **Specimen change under the jet (states C on 29/30 Sep):** mass change is one of the few direct measures of erosion or water uptake. Without a before-mass, a block cannot enter that analysis.
- **Comparing blocks of different size:** mass with W × L × H gives density and lets loss be normalised to block size (by dimensions, P2 is about 15 times the volume of P5).
- **Recommendation:** weigh every block immediately before clamping and immediately after the last run, on the same scale, and record 'not recorded' explicitly when missed.

## Files

Mode: G = guided on the linear rail, F = freehand. Loc = insertion site and Round = insertion round (R1–R4); both are useful covariates for within-block position and time effects. Start = start of the recording (from the file). Baseline = median force over the first 5 s, raw (before processing). Use = suggested handling in the analysis.

| File name | Tissue type | Frequency | Mode | Rep | Loc | Round | Stroke | Written clock | Start | Length (s) | Baseline (N) | Use | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `C01_CHK-DRIFT_28_305.xlsx` | None (sensor check, no block) | 100 Hz | — |  |  |  | none | 14:10 | 14:10:28 | 576 | 0.254 | Level-1 check | Zero-drift recording, 10 min, cannula hanging free with no contact. Reference for the sensor noise floor and short-term drift after the only tare (14:00). Drift across the session: 0.25 N (C01) to 2.44 N (C08). |
| `C02_CHK-LOAD_17_153.xlsx` | None (sensor check, no block) | 100 Hz | — |  |  |  | none | 14:30 | 14:30:17 | 282 | 2.000 | Do not use for calibration | Known-load check, judged a faulty procedure (Deviation D8): cannula hand-pressed on a kitchen scale and the scale read by eye; the sensor assembly dislocated several times and the scale reading fluctuated. Reset was pressed instead of Tare at the 0 g step. Plateaus cap at about 9.8 N; the zero between presses wanders 0.23–0.71 N; the down branch reads 25–60 % below the up branch. Not evaluable as a gain check. Absolute forces rely on the factory calibration. About 14:23, just before this file, the sensor housing came off violently and was reseated. |
| `C03_CHK-PULL_59_749.xlsx` | None (sensor check, no block) | 100 Hz | — |  |  |  | none | 14:36 | 14:36:59 | 39 | 2.148 | Level-1 check | Three gentle axial pulls, about 25 N each; the sensor assembly came off on the 3rd pull and was reseated. Useful for the sign convention and pull response. The final segment contains the detachment and reseating artefact. Baseline is already 2.1 N (not re-tared). |
| `C04_AIR_G_02_191.xlsx` | None (air strokes, no block) | 100 Hz | Guided (rail) |  |  |  | 80 mm (assumed) | 14:49 | 14:48:02 | 90 | 0.284 | Air reference (start) | Guided strokes in air, no block. Handpiece and rail dynamics without tissue: subtract or compare to get the air/tissue variance share for the guided runs. Written clock is about the end of the recording. |
| `C05_AIR_F_22_179.xlsx` | None (air strokes, no block) | 100 Hz | Freehand |  |  |  | 80 mm (assumed) | 14:51 | 14:50:22 | 84 | 4.026 | Air reference (start) | Freehand strokes in air, no block. Contains one sudden spike where the cannula hit the metal housing; mask it before computing fluctuation descriptors. Baseline is high (4.0 N). |
| `R23_BLOCK_P4-B1_G_rep-4_39_937.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Guided (rail) | 4 | L7 | R4 | 80 mm | 16:35 | 16:35:39 | 82 | 1.316 | Primary | First valid block run after the tape was removed from the vacuum-control hole (earlier readings from 15:03–16:21 were void). First recording of the main session, so the most exposed to time drift. Clean per the operator. Followed by an aborted 57 s file (00036, not in this dataset). |
| `R24_BLOCK_P4-B1_F_rep-4_39_297.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Freehand | 4 | L8 | R4 | 80 mm | 16:41 | 16:41:39 | 87 | 0.998 | Primary | Clean per the operator. Most likely a repeat of an aborted freehand try (00036, 57 s) at 16:37. |
| `R21_BLOCK_P4-B1_F_rep-3_04_411.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Freehand | 3 | L6 | R3 | 80 mm | 16:50 | 16:50:04 | 80 | 0.324 | Primary | Clean per the operator. Recorded right after the lost R22 attempt (00038). Freehand stroke pattern confirmed in the data (checked 29 Sep). |
| `R20_BLOCK_P4-B1_F_rep-2_37_193.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Freehand | 2 | L3 | R2 | 80 mm | 16:52 (end) | 16:51:37 | 83 | 0.438 | Primary; mask start | Sensor housing came off at the start and was refixed, so expect drops and spikes in the initial phase. Trim or mask the first seconds before windowing. The written time is the end time (D7). |
| `R19_BLOCK_P4-B1_G_rep-2_56_047.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Guided (rail) | 2 | L4 | R2 | 80 mm | 16:56 (end) | 16:54:56 | 83 | 0.721 | Primary | Clean per the operator. The written time is the end time, read from the saved directory (D7). |
| `R18_BLOCK_P4-B1_G_rep-1_06_694.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Guided (rail) | 1 | L1 | R1 | 80 mm | 16:57 | 16:57:06 | 83 | 0.446 | Primary | Clean per the operator. |
| `R17_BLOCK_P4-B1_F_rep-1_01_577.xlsx` | Phantom P4: 6 % gelatin + 1 % chitosan | 100 Hz | Freehand | 1 | L2 | R1 | 80 mm | 16:58 | 16:59:01 | 91 | 1.112 | Primary | Clean per the operator. The written clock (16:58) is 1 min before the file start, so the file is identified by sequence. Last P4 run: the block had cracks across its top surface after testing (photo 17:02). |
| `R09_BLOCK_P5-B1_G_rep-1_03_977.xlsx` | Phantom P5: complete composite | 100 Hz | Guided (rail) | 1 | L1 | R1 | 80 mm | 17:09 | 17:10:03 | 83 | 1.440 | Primary | Clean per the operator. Restart after an aborted 34 s attempt (00044). P5 is a thin block (20 mm high) with insertion sites only 10 mm apart (15 mm on the other blocks), so the cannula runs close to the surfaces and tunnels may merge. |
| `R10_BLOCK_P5-B1_F_rep-1_38_105.xlsx` | Phantom P5: complete composite | 100 Hz | Freehand | 1 | L2 | R1 | 80 mm | 17:12 | 17:12:38 | 90 | 2.050 | Primary; mask spike | One sudden large spike where the cannula hit the metal frame. It is not a tissue response, so mask it or use robust descriptors. |
| `R11_BLOCK_P5-B1_F_rep-2_39_603.xlsx` | Phantom P5: complete composite | 100 Hz | Freehand | 2 | L3 | R2 | 80 mm | 17:14 | 17:14:39 | 86 | 0.931 | Primary; mask 10–15 s | The sensor came off at about 10–15 s and was reattached, so expect a drop followed by a spike there. Mask that segment; the baseline may shift after reattachment. |
| `R12_BLOCK_P5-B1_G_rep-2_11_822.xlsx` | Phantom P5: complete composite | 100 Hz | Guided (rail) | 2 | L4 | R2 | 80 mm | 17:17 | 17:17:11 | 83 | 0.538 | Primary; mask mid-run | The sensor housing came off about halfway through, and for about 2–4 s the cannula travelled between the phantom and the bottom plate. That segment reflects plate contact, not tissue, so mask it; the baseline may shift after it. |
| `R13_BLOCK_P5-B1_G_rep-3_55_295.xlsx` | Phantom P5: complete composite | 100 Hz | Guided (rail) | 3 | L6 | R3 | 80 mm | 17:21 (end) | 17:19:55 | 83 | 2.458 | Primary; mask start | The sensor had come off and was fixed at the start, giving an initial spike; trim the start. The baseline is elevated (2.46 N). The written time is the end time, taken from when the file was saved (D7). |
| `R14_BLOCK_P5-B1_F_rep-3_55_391.xlsx` | Phantom P5: complete composite | 100 Hz | Freehand | 3 | L5 | R3 | 80 mm | 17:22 | 17:22:55 | 84 | 0.462 | Primary | Clean per the operator. |
| `R15_BLOCK_P5-B1_F_rep-4_46_674.xlsx` | Phantom P5: complete composite | 100 Hz | Freehand | 4 | L8 | R4 | 80 mm | 17:24 | 17:24:46 | 87 | 1.486 | Primary | Clean per the operator. |
| `R16_BLOCK_P5-B1_G_rep-4_33_919.xlsx` | Phantom P5: complete composite | 100 Hz | Guided (rail) | 4 | L7 | R4 | 80 mm | 17:27 | 17:27:33 | 85 | 1.240 | Primary; mask 10–20 s + spike | The sensor came out of the housing between 10 and 20 s and was fixed (mask that segment). Afterwards the cannula hit the housing once, so any isolated extraordinary spike is an impact artefact. |
| `R01_BLOCK_P1-B1_F_rep-1_18_010.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Freehand | 1 | L1 | R1 | 80 mm | 17:34 | 17:34:18 | 79 | 1.284 | Primary | Clean per the operator. |
| `R02_BLOCK_P1-B1_G_rep-1_47_029.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Guided (rail) | 1 | L2 | R1 | 80 mm | 17:36 | 17:36:47 | 84 | 0.663 | Primary | Clean per the operator. |
| `R03_BLOCK_P1-B1_G_rep-2_46_614.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Guided (rail) | 2 | L3 | R2 | 80 mm | 17:38 | 17:38:46 | 84 | 0.534 | Primary | Clean per the operator. |
| `R04_BLOCK_P1-B1_F_rep-2_01_354.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Freehand | 2 | L4 | R2 | 80 mm | 17:40 | 17:41:01 | 83 | 1.120 | Primary | Clean per the operator. |
| `R05_BLOCK_P1-B1_F_rep-3_39_901.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Freehand | 3 | L5 | R3 | 80 mm | 17:42 | 17:42:39 | 85 | 1.306 | Primary; mask start + spike | Initial inactivity (a flat, dull segment while the sensor was out of its seat), then a sudden spike from the cannula hitting the metal frame. Trim the inactive start (the activity detector should exclude it) and mask the spike. |
| `R06_BLOCK_P1-B1_G_rep-3_21_822.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Guided (rail) | 3 | L6 | R3 | 80 mm | 17:45 | 17:45:21 | 83 | 0.693 | Primary | Clean per the operator. |
| `R07_BLOCK_P1-B1_G_rep-4_21_591.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Guided (rail) | 4 | L8 | R4 | 80 mm | 17:47 | 17:47:21 | 83 | 2.122 | Primary | Clean per the operator. The baseline is elevated (2.12 N) compared with the neighbouring P1 runs, so subtract a per-run baseline. |
| `R08_BLOCK_P1-B1_F_rep-4_40_400.xlsx` | Phantom P1: 6 % gelatin | 100 Hz | Freehand | 4 | L7 | R4 | 80 mm | 17:49 | 17:49:40 | 83 | 1.174 | Primary | Clean per the operator. |
| `R25_BLOCK_P2-B1_G_rep-1_14_356.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Guided (rail) | 1 | L2 | R1 | 80 mm | 18:02 | 18:02:14 | 82 | 1.395 | Primary | Clean per the operator. P2-B1 is a large, free-standing block (200 × 260 × 80 mm), not the aquarium. |
| `R26_BLOCK_P2-B1_F_rep-1_16_570.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Freehand | 1 | L1 | R1 | 80 mm | 18:04 | 18:04:16 | 83 | 1.457 | Primary | Clean per the operator. |
| `R27_BLOCK_P2-B1_F_rep-2_49_883.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Freehand | 2 | L3 | R2 | 80 mm | 18:05 | 18:05:49 | 85 | 0.995 | Primary | Clean per the operator. |
| `R28_BLOCK_P2-B1_G_rep-2_13_830.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Guided (rail) | 2 | L4 | R2 | 80 mm | 18:08 | 18:08:13 | 83 | 0.737 | Primary | Clean per the operator. |
| `R29_BLOCK_P2-B1_G_rep-3_04_152.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Guided (rail) | 3 | L5 | R3 | 80 mm | 18:12 | 18:12:04 | 83 | 0.747 | Primary | Clean per the operator. Preceded by three short aborted files (00065–00067, not in this dataset). |
| `R30_BLOCK_P2-B1_F_rep-3_03_828.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Freehand | 3 | L6 | R3 | 80 mm | 18:13 | 18:14:03 | 83 | 1.233 | Primary; mask start | Starts with the sensor dislocating and being refixed, so expect sudden drops and spikes at the start; trim before windowing. |
| `R31_BLOCK_P2-B1_F_rep-4_06_052.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Freehand | 4 | L8 | R4 | 80 mm | 18:15 | 18:16:06 | 85 | 1.942 | Primary | Clean per the operator. Preceded by an aborted 6 s file (00070). |
| `R32_BLOCK_P2-B1_G_rep-4_20_362.xlsx` | Phantom P2: 8 % gelatin | 100 Hz | Guided (rail) | 4 | L7 | R4 | 80 mm | 18:18 | 18:18:20 | 88 | 2.128 | Primary | Clean per the operator. The baseline is elevated (2.13 N). |
| `R33_BLOCK_P3-B1_F_rep-1_12_675.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Freehand | 1 | L2 | R1 | 40 mm (mistake) | 18:29 | 18:29:12 | 84 | 0.796 | Primary; drop in sensitivity analysis | Stroke length 40 mm instead of 80 mm by mistake (D2): shorter strokes at the same 1.9 Hz cue mean lower speed and a different force profile per stroke. Kept in the primary analysis, excluded in the sensitivity analysis. P3 was the last block of the day, so it is the most exposed to time drift. |
| `R34_BLOCK_P3-B1_G_rep-1_10_053.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Guided (rail) | 1 | L1 | R1 | 40 mm (mistake) | 18:31 | 18:31:10 | 87 | 0.846 | Primary; drop in sensitivity analysis | Stroke length 40 mm by mistake (D2); see R33. |
| `R35_BLOCK_P3-B1_G_rep-2_59_072.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Guided (rail) | 2 | L4 | R2 | 40 mm (mistake) | 18:33 | 18:32:59 | 87 | 1.651 | Primary; drop in sensitivity analysis | Stroke length 40 mm by mistake (D2); see R33. |
| `R36_BLOCK_P3-B1_F_rep-2_52_908.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Freehand | 2 | L3 | R2 | 80 mm | 18:35 | 18:35:52 | 86 | 1.364 | Primary | Stroke length back to 80 mm. The paper note '(60)' is superseded: 80 mm. |
| `R37_BLOCK_P3-B1_F_rep-3_10_943.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Freehand | 3 | L5 | R3 | 80 mm | 18:38 | 18:38:10 | 81 | 2.027 | Primary | Clean per the operator. Preceded by an aborted 9 s file (00077). The baseline is elevated (2.03 N). |
| `R38_BLOCK_P3-B1_G_rep-3_53_641.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Guided (rail) | 3 | L6 | R3 | 80 mm | 18:40 | 18:40:53 | 86 | 0.828 | Primary | Clean per the operator. |
| `R39_BLOCK_P3-B1_G_rep-4_25_138.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Guided (rail) | 4 | L7 | R4 | 80 mm | 18:42 | 18:42:25 | 83 | 0.800 | Primary | Clean per the operator. |
| `R40_BLOCK_P3-B1_F_rep-4_58_693.xlsx` | Phantom P3: 8 % gelatin + lobules | 100 Hz | Freehand | 4 | L8 | R4 | 80 mm | 18:44 | 18:43:58 | 87 | 0.063 | Primary; mask end spike | A spike near the end where the cannula hit the metal frame; mask it. The baseline is near zero (0.06 N), unlike the neighbouring runs. |
| `C06_AIR_G_05_998.xlsx` | None (air strokes, no block) | 100 Hz | Guided (rail) |  |  |  | 80 mm (assumed) | 18:48 | 18:48:05 | 85 | 1.349 | Air reference (end) | Guided strokes in air, end of session. Compare with C04 for change in handpiece dynamics over the session, and use for the air/tissue variance share. |
| `C07_AIR_F_50_890.xlsx` | None (air strokes, no block) | 100 Hz | Freehand |  |  |  | 80 mm (assumed) | 18:49 | 18:49:50 | 84 | 1.635 | Air reference (end) | Freehand strokes in air, end of session. Compare with C05. |
| `C08_CHK-DRIFT_00_555.xlsx` | None (sensor check, no block) | 100 Hz | — |  |  |  | none | 18:51 | 18:52:00 | 201 | 2.444 | Level-1 check | Zero-drift recording, 3 min, end of session. The baseline of 2.44 N versus 0.25 N at C01 gives the total drift since the only tare. Use it with C01 to bound session-time drift. |

## Counts

| Block | Freehand | Guided | Total |
|---|---|---|---|
| P1-B1 | 4 | 4 | 8 |
| P2-B1 | 4 | 4 | 8 |
| P3-B1 | 4 | 4 | 8 |
| P4-B1 | 4 | 3 | 7 |
| P5-B1 | 4 | 4 | 8 |
| Checks and air | | | 8 (C01–C08) |

Total files: 47. Block runs: 39.

## Suggested extra entries for later analysis

- **Artefact windows in seconds** (start–end) for each file with a sensor-reseating or impact event. The notes above give the operator's approximate timing; confirm these from the signal and then fix them, so masking is reproducible.
- **Active-stroking interval** (start and end of stroking, from the activity detector). Most runs include idle time before and after the 80 s cue track.
- **Measured stroke frequency** (dominant frequency near the 1.9 Hz cue) per run, to check cue adherence, especially in freehand runs.
- **Baseline after artefact** for runs with reseating (R05, R11, R12, R13, R16, R20, R30), because the zero can shift mid-run.
- **Minutes since tare** (or since block removal from the fridge) as a drift and time covariate, given the P4 → P3 order.
- **Insertion depth** was not recorded. Keep it as an explicit 'not recorded' column so it is not assumed later.
- **Operator code** (O1) and **device state** (A), so these files pool cleanly with the 29 and 30 Sep WAL sessions (states A and C).
- **Sampling note for human comparison:** the human state-C references are at 10 Hz. Keep a 'resampled to 10 Hz (anti-aliased)' flag per derived file.
