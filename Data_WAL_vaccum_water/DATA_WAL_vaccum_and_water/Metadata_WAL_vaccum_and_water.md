# Metadata: DATA_WAL_vaccum_and_water (WAL session 29 Sep 2026, Session_Id 2)

One row per data file in this folder. The files are renamed copies of the DigiVision summary exports (`.sum.xlsx`) from `OneDrive\Sensor_Data\2026\0929\__SUM_PROT__` (source unchanged). The map from each run-sheet "File no." (taken from the raw `.meas9206` name) to the original `.sum.xlsx` and to the copy is in section 8. Each `.sum.xlsx` names its `.meas9206` source on its Overview sheet, and that was used to match the files.

The notes come from the uploaded run sheet (`Run_sheet_WAL_session_29_Sep_2026_Session_Id_2.md`), checked against the session records (`WAL_2026-09-29/RunSheet_and_Logs_2026-09-29.md`, `Datasheet_Sessions.md`, Amendments 3, 3a, 3b) and the 28 Sep records (`Bench_2026-09-28/Block_log.csv`, `Dataset_2026-09-28.md`, `Deviations_2026-09-28.md`, `metadata_no-vaccum_no-water.md`). The signal columns in section 5 were measured from the files on 30 Sep. They are screening values for orientation, not results of the frozen pipeline.

## 1. Session conditions (apply to every file)

- **Date and time:** 29 Sep 2026, 18:18–20:20 (evening). Operator Manish (O1). Room 22 °C; gel temperature not recorded.
- **Device state:** **C** = water jet Range 3 + vacuum on (maximum setting) for all block runs except W00, and for air runs C14, AR1–AR3 and AQ-air. **A** = jet and vacuum off for C11, C13, W00 and C17. The file name does not carry the state; use the Mode column below.
- **Acquisition:** DigiVision, **100 Hz** nominal (measured 99.94–99.95 Hz from the time stamps), channel 01, burster 9206 amplifier (SN 704988, SG 15 mV DC, excitation 5 V, averaging 2), unit N. All 27 files have continuous counters. The only timing irregularity is one missing sample in C13 at 44.9 s.
- **Force scaling:** stored two-point teach-in, 0 N at −0.607189 mV and 15 N at 1.389047 mV. The known-load check (C12) was not possible (D9), so absolute forces rest on the teach-in. Forces above 15 N (8b peaks up to 47 N, O13) are extrapolated.
- **File structure:** sheet `Overview` holds the paths of the `.sum` and `.meas9206` files. Sheet `1) 9206-704988-01` has a header (start time, batch 272, part number = file number, unit, minimum, maximum), then the columns Counter, Time [sec] and Measured value [N]. openpyxl 3.1.5 raises a stylesheet error on these exports, so read the sheet XML directly or use the reader the 28 Sep pipeline used.
- **Execution:** all runs guided on the rail, stroke 80 mm, cue track 1.9 Hz; each recording is planned as 10 s still, 60 s strokes, 10 s still. The measured active phase is about 60–68 s in most files (section 5).
- **Tare:** before every run with the device off (on 28 Sep: only once, at 14:00). Despite this, files start between −6.0 and +7.5 N (D13), and the still level after stroking differs from the level before by −3.9 to +5.7 N. **Use a per-run baseline from the pre-stroke still phase and check it against the post-stroke still phase.** Several files start near (a small positive value − the reading before tare), e.g. R1-4, R3-1, AQ-1 and AQ-3, so the tare may have captured a load. This is worth checking before absolute levels are interpreted.
- **Jet and vacuum load:** in state C the force level rises when stroking starts, also without tissue (air runs: +4.1 to +8.2 N). In state A air (C13) it rises by only 0.2 N. Absolute or mean force is therefore not comparable between states; compare **fluctuation descriptors** after baseline removal. The air run in state C already fluctuates (O12), so the rig contributes to every state-C signal.
- **Still phases:** in every file, including state C, the quiet part of the still phases shows only the sensor noise floor (SD about 0.003 N, the same as the device-off drift check C11). The jet and vacuum signal therefore appears only while stroking. Check whether the unit was running during the still phases, because this decides which segment can serve as the "jet without motion" baseline.
- **Stroke frequency:** only C14 has its main spectral peak near the 1.9 Hz cue (1.76 Hz). In the other files the peaks sit near 2.5–3.4 Hz and/or 0.4–0.7 Hz. C13 (air, state A) peaks at 2.7 Hz, so this peak comes from the stroke motion itself and not from the jet. Confirm the actual stroke rate before using 1.9 Hz as a fixed reference.
- **Mounts and time order:** blocks K, La, Lb and 8a (clamp) were interleaved in three rounds (18:58–19:55; order changed within rounds, D11). Blocks 6 and 8b (aquarium mount) were run as a batch at the end (20:00–20:13; D12), so mount and session time are confounded for these two blocks.
- **Specimen damage:** block La cracked open at the site in R1-2 (run sheet). Under full WAL load the gelatin-based phantoms broke apart to varying degrees; the composite K showed no visible cracking (O10).
- **Block masses:** not recorded (block log columns empty), so the planned erosion measure (mass change per block) is not available.
- **Not in this folder:** file 00030 (13.6 s aborted start, EXCL). File numbers 00004, 00015 and 00016 were never saved (aborted starts). Spare lines X1–X3 were not used; C12 (weights) was not done.

## 2. Blocks and their relation to the 28 Sep session

28 Sep (Session 1) was a bench session in **state A only** (jet and vacuum off, vacuum-control hole taped until 16:21), with guided (G) and freehand (F) runs on one block per formulation, P1-B1 to P5-B1, all clamped by a top disc on a threaded rod. The state effect (C vs A) in this session is therefore **cross-day and cross-block** (D10), except for 8a, which has the same-day state-A bridge run W00.

| Block | Phantom / formulation | Cast | Age at test | Mount | Files (runs) | 28 Sep counterpart | Relation and caveats |
|---|---|---|---|---|---|---|---|
| 8a | P2: 8 % gelatin, 30 % ethanol, 2 % glycerol, no acid | 26 Aug 2026 | 34 days | clamp | W00 (A), R1-4, R2-2, R3-4 (C) | P2-B1 (G: R25, R28, R29, R32) | Same formulation and cast date as P2-B1, per the block log. It is a separate block from the same cast (Amendment 3b: tonight's blocks differ in mould and curing); it is not recorded as the same physical block. The block log text says "same as P3-B1 of 28 Sep". This matches the 28 Sep sticky-note mix-up (O4: the lobule block was labelled "P2-B1"), so by composition the counterpart is P2-B1. W00 gives the day and block offset in state A. |
| 8b | P2: 8 % gelatin (as 8a) | 26 Aug 2026 | 34 days | aquarium | AQ-2, AQ-3, AQ-6 (C) | P2-B1 | Same cast as 8a, but aquarium mount (28 Sep P2-B1 was free-standing and clamped) and tested at the end of the session (D12). 8a vs 8b is therefore not a clean same-material twin. |
| La | P3: 8 % gelatin + agar–gelatin lobules, no acid | 26 Aug 2026 | 34 days | clamp | R1-2, R2-1, R3-2 (C) | P3-B1 (G: R34, R35 at 40 mm; R38, R39 at 80 mm) | Same formulation and cast date as P3-B1 (block log text "same as P2-B1 of 28 Sep" = the sticky-note label, O4). Only R38 and R39 are 80 mm guided references on 28 Sep. La cracked open in R1-2. |
| Lb | P3 (as La) | 26 Aug 2026 | 34 days | clamp | R1-3, R2-4, R3-3 (C) | P3-B1 | Twin of La (one batch). La vs Lb is the same-formulation control for C2 (P3 − P2), the only contrast detected on 28 Sep. |
| K | P5: complete composite (P4 matrix: 6 % gelatin + 1 % chitosan in citric acid; + lobules + microhollow spheres 3M K1) | December 2025 on the run sheet (28 Sep block log: April 2026, corrected 30 Sep) | about 10 months (or about 5–6 months) | clamp | R1-1, R2-3, R3-1 (C) | P5-B1 (G: R09, R12, R13, R16) | Same composition as P5-B1, per the block log. The cast date conflicts with the corrected 28 Sep record; confirm it. Whether K is the same physical block as P5-B1 is not recorded (Amendment 3b plans a small block, P5-s, with 3 sites). No cracking under WAL load (O10). |
| 6 | P1: 6 % gelatin + glycerol + ethanol, no acid | 22 Sep 2026 (run sheet) | 7 days | aquarium | AQ-1, AQ-4, AQ-5 (C) | P1-B1 (G: R02, R03, R06, R07) | **Composition only** is the same as P1-B1 (cast 15 Aug, about 6 weeks old on 28 Sep, refrigerated). This is a new, much younger cast in a different mount. `RunSheet_and_Logs` instead says "same batch as 28 Sep, room-temperature cured" (P1-B2 of Amendment 3a); resolve this before pooling or contrasting with 28 Sep P1. |
| — (air) | none | — | — | rail only | C13 (A); C14, AR1, AR2, AR3, AQ-air (C) | Air runs C04 (G) and C06 (G), state A | C13 is the direct counterpart of the 28 Sep guided air runs. The state-C air runs have no 28 Sep counterpart; C14/AR/AQ-air minus C13 gives the jet + vacuum contribution without tissue. |
| — (checks) | none | — | — | handpiece hanging free | C11, C17 (A) | Zero-drift checks C01, C08 | 3 min each, device off, tared (28 Sep: 10 min, one tare for the whole day). |

## 3. Files (requested columns)

Mode: A = jet and vacuum off, C = water jet Range 3 + vacuum on. All runs are guided on the rail (G), 80 mm stroke, cue 1.9 Hz. Rep = insertion site on the block (for the three 8a round runs the site was not recorded on the day and was set to 1, 2, 3 by the operator on 30 Sep).

| File name | Tissue type | Frequency | Mode | Notes | Relation to 28 Sep tissue |
|---|---|---|---|---|---|
| `C11_CHK-DRIFT_30_501.xlsx` | None (sensor check, no block) | 100 Hz | A | Zero drift at session start, planned 3 min (file 222 s), device off, handpiece hanging free. Level 0.59 N throughout (drift < 0.01 N), SD 0.003 N: this is the **sensor noise floor** for the session. Reading before tare 0.5952 N equals the file level, so the recording is not tared. | Counterpart of 28 Sep C01 (10 min, state A). |
| `C13_AIR_G_18_089.xlsx` | None (air strokes, no block) | 100 Hz | A | Guided air strokes 10/60/10 s with jet and vacuum off. Very low load: level rises only 0.2 N while stroking, fluctuation SD 0.07 N. Main spectral peak 2.7 Hz (stroke motion without jet). One missing sample at 44.9 s. **State-A rig and rail reference.** | Direct counterpart of 28 Sep guided air runs C04 and C06 (state A). |
| `C14_AIR_G_15_502.xlsx` | None (air strokes, no block) | 100 Hz | C | First air run with jet and vacuum on (maximum setting); the jet sprayed into a tray. Level rises 5.2 N while stroking and stays 2.4 N higher afterwards. Fluctuation SD 0.43 N (six times C13). Vacuum gauge entry on the run sheet ("500 bar") needs its unit checked (section 6). **State-C air reference at session start.** | No 28 Sep counterpart (no jet on 28 Sep). C14 − C13 = jet + vacuum contribution without tissue. |
| `W00_BLOCK_P2-8a_G_rep-1_06_676.xlsx` | Phantom P2: 8 % gelatin (block 8a, clamp) | 100 Hz | A | **Bridge run** to 28 Sep in state A on block 8a, site 1. Clean single stroking phase, 7–74 s; peak 12.1 N; the still level after stroking is 2.7 N higher. The reading before tare (1.2039 N) is entered in the gauge column of the run sheet. | Same formulation, cast date and state (A) as 28 Sep P2-B1 guided runs R25, R28, R29, R32; separate block. Gives the day and block offset for 8a. |
| `R1-1_BLOCK_P5-K_G_rep-1_21_367.xlsx` | Phantom P5: complete composite (block K) | 100 Hz | C | Round 1, K site 1. First tissue run in state C. Stroking 13–76 s; the still level after stroking is 4.0 N higher. Strong low-frequency component (main peak 0.5 Hz). | Same composite as 28 Sep P5-B1 (state A, G: R09, R12, R13, R16); cast date to confirm. Cross-day, cross-state comparison. |
| `R1-2_BLOCK_P3-La_G_rep-1_29_491.xlsx` | Phantom P3: 8 % gelatin + lobules (block La) | 100 Hz | C | Round 1, La site 1. **The phantom cracked open at the site** (run sheet). Stroking ends at about 60 s (other runs: about 74 s) and the mean force falls from about 12 N to about 4 N across the run, consistent with the block opening up. Use 14–58 s and flag as compromised material. Reading before tare 5.2319 N on the run sheet, blank in the session log. | Same formulation and cast as 28 Sep P3-B1 (80 mm G references R38, R39). |
| `R1-3_BLOCK_P3-Lb_G_rep-1_59_104.xlsx` | Phantom P3: 8 % gelatin + lobules (block Lb) | 100 Hz | C | Round 1, Lb site 1. Clean. Still level after stroking 5.2 N higher than before (one of the largest shifts); activity continues to about 81 s. | Same formulation and cast as 28 Sep P3-B1; twin of La. |
| `R1-4_BLOCK_P2-8a_G_rep-1_52_713.xlsx` | Phantom P2: 8 % gelatin (block 8a, clamp) | 100 Hz | C | Round 1, 8a (site set to 1 on 30 Sep; W00 is also recorded at site 1, so check whether it is the same insertion site). File starts at −5.2 N (reading before tare 6.3053 N). Clean stroking 14–78 s. | Same formulation and cast as 28 Sep P2-B1. W00 (same block, state A, same day) is the within-block state reference. |
| `AR1_AIR_G_41_475.xlsx` | None (air strokes, no block) | 100 Hz | C | Air run after round 1 (state C). Level rise 4.1 N, fluctuation SD 0.45 N. Starts at −1.2 N (reading before tare −1.3876 N). Use as the rig reference for round 1. | No 28 Sep counterpart (state C). |
| `R2-1_BLOCK_P3-La_G_rep-2_56_061.xlsx` | Phantom P3: 8 % gelatin + lobules (block La) | 100 Hz | C | Round 2, La site 2 (run before 8a in this round, D11). Longest recording (90.9 s), activity 11–87 s. High mean load during stroking (+15.4 N) with large slow level changes (SD 4.6 N vs fluctuation SD 0.64 N). Reading before tare −0.2299 N on the run sheet, blank in the session log. | Same formulation and cast as 28 Sep P3-B1. |
| `R2-2_BLOCK_P2-8a_G_rep-2_16_610.xlsx` | Phantom P2: 8 % gelatin (block 8a, clamp) | 100 Hz | C | Round 2, 8a (site set to 2 on 30 Sep). Clean. Highest level rise of the clamp blocks (+15.8 N); the still level after stroking is 5.1 N higher. Strongest single spectral peak of the session (2.7 Hz, 21 % of 0.3–8 Hz power). | Same formulation and cast as 28 Sep P2-B1. |
| `R2-3_BLOCK_P5-K_G_rep-2_00_567.xlsx` | Phantom P5: complete composite (block K) | 100 Hz | C | Round 2, K site 2. Device switched off 5 s before tare (session log). The level steps up by about 0.8 N at 7 s, before stroking. One sharp transient at 13.8 s (+9 N above the local level) at stroke onset. | Same composite as 28 Sep P5-B1. |
| `R2-4_BLOCK_P3-Lb_G_rep-2_48_077.xlsx` | Phantom P3: 8 % gelatin + lobules (block Lb) | 100 Hz | C | Round 2, Lb site 2. Clean. Largest shift of the still level after stroking in the clamp blocks (+5.7 N). | Same formulation and cast as 28 Sep P3-B1. |
| `AR2_AIR_G_15_742.xlsx` | None (air strokes, no block) | 100 Hz | C | Air run after round 2. The file starts at 7.07 N, equal to the reading before tare (7.0553 N), so the tare did not take effect. Level rise 7.7 N, fluctuation SD 0.40 N. Rig reference for round 2. | No 28 Sep counterpart (state C). |
| `R3-1_BLOCK_P5-K_G_rep-3_21_464.xlsx` | Phantom P5: complete composite (block K) | 100 Hz | C | Round 3, K site 3 (K run first in this round, D11; last free site on K). File starts at −5.5 N (reading before tare 6.7532 N); the still level after stroking is 5.6 N higher. | Same composite as 28 Sep P5-B1. |
| `R3-2_BLOCK_P3-La_G_rep-3_25_778.xlsx` | Phantom P3: 8 % gelatin + lobules (block La) | 100 Hz | C | Round 3, La site 3 (the block had cracked in R1-2). Handling from about 6 s, strokes from about 12 s. Highest peak of the clamp blocks (26.7 N). | Same formulation and cast as 28 Sep P3-B1. |
| `R3-3_BLOCK_P3-Lb_G_rep-3_37_992.xlsx` | Phantom P3: 8 % gelatin + lobules (block Lb) | 100 Hz | C | Round 3, Lb site 3. File starts at −3.8 N. Two sharp transients, at 24.4 s (21 N) and 72.2 s (at stroke end); mask them or use robust descriptors. | Same formulation and cast as 28 Sep P3-B1. |
| `R3-4_BLOCK_P2-8a_G_rep-3_40_520.xlsx` | Phantom P2: 8 % gelatin (block 8a, clamp) | 100 Hz | C | Round 3, 8a (site set to 3 on 30 Sep). Clean. Still level after stroking 2.7 N higher. | Same formulation and cast as 28 Sep P2-B1. |
| `AR3_AIR_G_33_134.xlsx` | None (air strokes, no block) | 100 Hz | C | Air run after round 3. The file starts at 7.5 N, then the level drops about 5 N at 6 s and fluctuates before strokes start at about 13 s, so the pre-stroke baseline is ambiguous. Use 13–72 s. Highest air fluctuation of the session (SD 0.60 N). | No 28 Sep counterpart (state C). |
| `AQ-1_BLOCK_P1-6_G_rep-1_55_344.xlsx` | Phantom P1: 6 % gelatin (block 6, aquarium) | 100 Hz | C | First aquarium run, 6 site 1. Long still phase: **strokes only from about 24 s to 85 s** (95.4 s file). Handling spike at 5.5 s in the still phase (+13 N). File starts at −5.4 N; the still level after stroking is 5.7 N higher. Reading before tare 7.0588 N on the run sheet vs 1.058 N in the session log. | Same composition as 28 Sep P1-B1, but a new cast (22 Sep, 7 days old) in an aquarium; not the same block or cure. |
| `AQ-2_BLOCK_P2-8b_G_rep-1_43_896.xlsx` | Phantom P2: 8 % gelatin (block 8b, aquarium) | 100 Hz | C | 8b site 1. **Many sharp transients between 23 and 52 s, up to 47.1 N** (session maximum; above the 15 N teach-in point, O13). Fluctuation about three to four times that of 8a. Cause not recorded (possible contact with the aquarium, or the gel breaking apart, O10); mask the transients or use robust descriptors, and report the 8b vs 8a difference with the mount confound. | Same cast as 28 Sep P2-B1 but aquarium mount (P2-B1 was free-standing). |
| `AQ-3_BLOCK_P2-8b_G_rep-2_28_798.xlsx` | Phantom P2: 8 % gelatin (block 8b, aquarium) | 100 Hz | C | 8b site 2. Sharp transients throughout (17.8–68.3 s, up to 42.0 N); the highest fluctuation of the session. File starts at −6.0 N; the still level after stroking is 5.5 N higher. | As AQ-2. |
| `AQ-4_BLOCK_P1-6_G_rep-2_44_486.xlsx` | Phantom P1: 6 % gelatin (block 6, aquarium) | 100 Hz | C | 6 site 2. Starts at 5.4 N and ends 3.9 N lower (the only large negative shift). Small level rise while stroking (+1.6 N) with slow wander. Reading before tare −0.3763 N on the run sheet, blank in the session log. | Same composition as 28 Sep P1-B1; new cast. |
| `AQ-5_BLOCK_P1-6_G_rep-3_45_530.xlsx` | Phantom P1: 6 % gelatin (block 6, aquarium) | 100 Hz | C | 6 site 3. **Very low load:** level rise only 0.2 N, peak 7.2 N (lowest block run). Check whether the cannula ran in intact gel or in a broken or water-filled region before using it as a tissue run. | Same composition as 28 Sep P1-B1; new cast. |
| `AQ-6_BLOCK_P2-8b_G_rep-3_06_371.xlsx` | Phantom P2: 8 % gelatin (block 8b, aquarium) | 100 Hz | C | 8b site 3. Sharp transients at 12.6 s and 17.1 s (42.0 N). Stroking ends at about 70 s. Reading before tare 5.2847 N on the run sheet vs 2.847 N in the session log. | As AQ-2. |
| `AQ-air_AIR_G_04_127.xlsx` | None (air strokes, no block) | 100 Hz | C | End air run on the aquarium set-up. Level rise 8.2 N (largest of the air runs), fluctuation SD 0.40 N. Rig reference for the aquarium batch. Reading before tare −0.6415 N on the run sheet vs +0.6415 N in the session log. | No 28 Sep counterpart (state C). |
| `C17_CHK-DRIFT_31_825.xlsx` | None (sensor check, no block) | 100 Hz | A | Zero drift at session end, planned 3 min (file 189 s), device off. Drift −0.09 N over the recording, one small blip at 40 s (0.3 N). No reading before tare recorded. Starts 18 s after the aborted file 00030. | Counterpart of 28 Sep C08. |

## 4. Counts

| Group | State A | State C | Files |
|---|---|---|---|
| Block 8a (P2, clamp) | 1 (W00) | 3 | 4 |
| Block 8b (P2, aquarium) | – | 3 | 3 |
| Block La (P3, clamp) | – | 3 | 3 |
| Block Lb (P3, clamp) | – | 3 | 3 |
| Block K (P5, clamp) | – | 3 | 3 |
| Block 6 (P1, aquarium) | – | 3 | 3 |
| Air runs | 1 (C13) | 5 | 6 |
| Zero-drift checks | 2 | – | 2 |
| **Total** | 4 | 23 | **27** |

Block runs: 19 (18 in state C, 1 in state A). Formulation level, state C: P2 6 runs on 2 blocks, P3 6 runs on 2 blocks, P5 3 runs on 1 block, P1 3 runs on 1 block.

## 5. Signal screening per file (suggested extra columns)

Measured on 30 Sep from the copies in this folder. Active = interval with movement above the noise floor (includes any handling just before the first stroke). Pre = median of the still phase before activity. Rise = median during activity − Pre. Shift = still level after activity − Pre. Fluct. SD = SD of the signal minus its 1-s moving median, during activity (a simple, baseline-free fluctuation measure; not the frozen-pipeline window SD). Peak = maximum of the file. Spectral peak = largest peak of the 0.3–8 Hz spectrum over 12–68 s. Transients = samples more than 8 N above the 1-s moving median.

| File | Start | Length (s) | Active (s) | Pre (N) | Rise (N) | Shift (N) | Fluct. SD (N) | Peak (N) | Spectral peak (Hz) | Transients | Suggested use |
|---|---|---|---|---|---|---|---|---|---|---|---|
| C11_CHK-DRIFT_30_501 | 18:18:30 | 221.7 | – | 0.59 | – | – | 0.003 | 0.6 | – | none | Level-1 check (noise floor) |
| C13_AIR_G_18_089 | 18:32:18 | 83.5 | 13–73 | 0.59 | 0.24 | +0.14 | 0.07 | 1.8 | 2.69 | none | Air reference, state A |
| C14_AIR_G_15_502 | 18:42:15 | 86.9 | 16–76 | 0.96 | 5.15 | +2.41 | 0.43 | 8.4 | 1.76 | none | Air reference, state C (start) |
| W00_BLOCK_P2-8a_G_rep-1_06_676 | 18:53:06 | 90.4 | 7–74 | 0.99 | 7.28 | +2.70 | 0.60 | 12.1 | 2.54 | none | Bridge (state A, 8a) |
| R1-1_BLOCK_P5-K_G_rep-1_21_367 | 18:58:21 | 84.5 | 13–76 | 1.22 | 6.66 | +3.97 | 0.82 | 13.8 | 0.49 | none | Primary |
| R1-2_BLOCK_P3-La_G_rep-1_29_491 | 19:02:29 | 82.8 | 13–60 | 1.04 | 7.63 | +0.13 | 0.81 | 15.0 | 2.88 | none | Primary, compromised (block cracked); use 14–58 s |
| R1-3_BLOCK_P3-Lb_G_rep-1_59_104 | 19:06:59 | 84.2 | 14–81 | 1.08 | 5.13 | +5.23 | 0.73 | 16.5 | 2.88 | none | Primary |
| R1-4_BLOCK_P2-8a_G_rep-1_52_713 | 19:12:52 | 83.0 | 14–78 | −5.17 | 9.00 | +3.77 | 0.55 | 7.6 | 2.59 | none | Primary |
| AR1_AIR_G_41_475 | 19:17:41 | 84.8 | 9–75 | −1.24 | 4.08 | +0.94 | 0.45 | 7.6 | 0.68 | none | Air reference, round 1 |
| R2-1_BLOCK_P3-La_G_rep-2_56_061 | 19:20:56 | 90.9 | 11–87 | 1.15 | 15.42 | +0.48 | 0.64 | 21.7 | 2.98 | none | Primary |
| R2-2_BLOCK_P2-8a_G_rep-2_16_610 | 19:26:16 | 82.7 | 10–74 | 1.19 | 15.82 | +5.08 | 0.72 | 21.8 | 2.69 | none | Primary |
| R2-3_BLOCK_P5-K_G_rep-2_00_567 | 19:30:00 | 87.9 | 7–73 | 5.00 | 8.84 | +1.07 | 0.80 | 19.3 | 0.39 | 13.8 s | Primary; mask onset transient |
| R2-4_BLOCK_P3-Lb_G_rep-2_48_077 | 19:34:48 | 84.9 | 9–76 | 1.14 | 14.73 | +5.71 | 0.92 | 24.2 | 2.73 | none | Primary |
| AR2_AIR_G_15_742 | 19:40:15 | 81.2 | 9–71 | 7.07 | 7.67 | −0.38 | 0.40 | 23.6 | 0.49 | none | Air reference, round 2 |
| R3-1_BLOCK_P5-K_G_rep-3_21_464 | 19:43:21 | 84.4 | 10–74 | −5.51 | 14.04 | +5.55 | 0.52 | 13.5 | 3.08 | none | Primary |
| R3-2_BLOCK_P3-La_G_rep-3_25_778 | 19:46:25 | 82.4 | 6–74 | 5.71 | 10.61 | +0.70 | 0.76 | 26.7 | 0.59 | none | Primary (block already cracked) |
| R3-3_BLOCK_P3-Lb_G_rep-3_37_992 | 19:49:37 | 82.2 | 8–73 | −3.83 | 13.48 | +3.15 | 0.41 | 21.0 | 0.59 | 24.4, 72.2 s | Primary; mask transients |
| R3-4_BLOCK_P2-8a_G_rep-3_40_520 | 19:52:40 | 83.8 | 7–74 | 5.24 | 10.01 | +2.73 | 0.55 | 20.8 | 0.49 | none | Primary |
| AR3_AIR_G_33_134 | 19:55:33 | 82.4 | 5–73 (strokes from about 13) | 7.48 | 4.43 | −0.44 | 0.60 | 18.4 | 3.12 | none | Air reference, round 3; baseline ambiguous |
| AQ-1_BLOCK_P1-6_G_rep-1_55_344 | 20:00:55 | 95.4 | 24–86 | −5.35 | 9.94 | +5.70 | 0.89 | 17.3 | 3.03 | 5.5 s (still phase) | Primary; window from 24 s |
| AQ-2_BLOCK_P2-8b_G_rep-1_43_896 | 20:03:43 | 84.8 | 10–74 | 6.60 | 8.40 | +0.81 | 2.16 | 47.1 | 0.59 | 9 events, 23–52 s | Primary with care; mask transients; mount confound |
| AQ-3_BLOCK_P2-8b_G_rep-2_28_798 | 20:06:28 | 84.9 | 15–76 | −5.96 | 14.69 | +5.51 | 2.56 | 42.0 | 0.68 | 9 events, 18–68 s | Primary with care; mask transients; mount confound |
| AQ-4_BLOCK_P1-6_G_rep-2_44_486 | 20:08:44 | 85.7 | 11–74 | 5.43 | 1.59 | −3.93 | 0.83 | 24.0 | 0.44 | none | Primary |
| AQ-5_BLOCK_P1-6_G_rep-3_45_530 | 20:10:45 | 85.5 | 9–74 | 1.17 | 0.21 | +4.10 | 0.55 | 7.2 | 0.44 | none | Check contact before use |
| AQ-6_BLOCK_P2-8b_G_rep-3_06_371 | 20:13:06 | 81.2 | 10–70 | −0.03 | 8.71 | −0.66 | 0.93 | 42.0 | 0.63 | 12.6, 17.1 s | Primary; mask transients; mount confound |
| AQ-air_AIR_G_04_127 | 20:15:04 | 84.2 | 9–77 | 4.74 | 8.22 | +1.22 | 0.40 | 19.0 | 0.39 | none | Air reference, aquarium batch |
| C17_CHK-DRIFT_31_825 | 20:17:31 | 188.7 | – | −0.01 | – | −0.09 (drift) | 0.014 | 0.3 | – | none | Level-1 check (end) |

**Rig contribution per round (screening, Fluct. SD):** (air SD ÷ median tissue SD of the same round)² = round 1: 0.34; round 2: 0.28; round 3: 1.26; aquarium batch: 0.19. In round 3 the air run fluctuates more than the median tissue run, so round-3 tissue fluctuation is not clearly above the rig level on this measure. The largest air SD ÷ the smallest = 1.5 (< 2, the stability rule of Amendment 3a). Recompute both with the frozen-pipeline descriptor before reporting.

## 6. Records that disagree or need confirmation

| Item | Uploaded run sheet | Other record | Action |
|---|---|---|---|
| Reading before tare, AQ-1 | 7.0588 N | 1.058 N (session log) | Confirm from the paper sheet |
| Reading before tare, AQ-6 | 5.2847 N | 2.847 N (session log) | Confirm |
| Reading before tare, AQ-air | −0.6415 N | +0.6415 N (session log) | Confirm the sign |
| Reading before tare, R1-2, R2-1, AQ-4 | 5.2319, −0.2299, −0.3763 N | blank (session log) | Run-sheet values used |
| Reading before tare, R1-3, R2-4, AQ-2, AQ-3 | 1.1657, 6.1398, 0.3693, 7.4856 N | 1.1654, 6.139, 0.3695, 7.4857 N | Rounding or transcription; negligible |
| W00 | 1.2039 in the gauge column | 1.2039 N as the reading before tare (session log) | Treat as the reading before tare |
| Vacuum setting | "500 bar (max setting)" | "about 340 mmHg in air" (session log); target "about 500 mbar" (Amendment 3) | 500 bar is not physically possible for a vacuum; likely 500 mbar (setting). Record the unit and the gauge reading |
| Block K cast date | December 2025 | April 2026 (28 Sep block log, corrected by the operator on 30 Sep) | Confirm; affects block age (about 10 vs about 5–6 months) |
| Block 6 origin | cast 22 Sep 2026; "only composition same as P1-B1" | "same batch as 28 Sep, room-temperature cured" (session log; P1-B2 of Amendment 3a, cast 15 Aug) | Confirm; decides whether block 6 can be linked to 28 Sep P1 |
| 28 Sep labels in the block log | 8a/8b "same as P3-B1", La/Lb "same as P2-B1" | 28 Sep O4: the lobule block's sticky note read "P2-B1" | By composition: 8a/8b ↔ P2-B1, La/Lb ↔ P3-B1 (used in this file) |
| Site of the 8a round runs | blank | blank (session log, datasheet) | Set to 1, 2, 3 by the operator on 30 Sep; W00 is also site 1 on 8a |
| Session log "Anything unusual: no" | – | R1-2 block cracked; O10, O12, O13 | Informational |

## 7. Suggested extra entries for later analysis

- **State-specific baseline segment:** mark per file which segment is the baseline (pre-stroke still) and whether the post-stroke still is usable as a check. The pre/post shifts of up to 5.7 N make a single constant baseline unsafe.
- **Artefact windows in seconds** for the transients listed in section 5 (8b runs, R2-3, R3-3, AQ-1) and the post-crack part of R1-2. Confirm them from the signal and fix them in a table so masking is reproducible.
- **Measured stroke rate** per run (count strokes or use the autocorrelation of the displacement-driven component), because the spectra do not peak at the 1.9 Hz cue.
- **Round and position in session** (round 1–3 or aquarium batch; minutes since first run), as covariates for time, specimen damage and gel warming in an evening session.
- **Site condition:** intact / near an earlier tunnel / cracked. This matters for La after R1-2 and for block 6 (AQ-5).
- **Block mass before and after** (not recorded here); keep an explicit "not recorded" entry so erosion is not assumed.
- **Gel temperature** at the start and end (planned in Amendment 3b, not recorded).
- **Jet/vacuum on-time:** whether the unit ran during the still phases (see section 1), so "jet without motion" can be defined.
- **Operator code (O1), Session_Id (2) and device state (A/C)** as explicit columns, so these files pool cleanly with the 28 Sep (Session 1) and 30 Sep sessions.
- **Sampling note for the human comparison:** the human state-C references are at 10 Hz. Keep a "resampled to 10 Hz (anti-aliased)" flag per derived file.

## 8. File map

Name pattern: Row_Type_Phantom-Block_Cond_rep-Site_<last five digits of the original `.sum.xlsx` name>.xlsx (empty fields left out, `.sum` dropped, as in `DATA_no-vaccum_no-water`). The last five digits therefore differ from the run sheet's File no., which comes from the `.meas9206` name.

| File in this folder | Run-sheet File no. (.meas9206) | Original .sum.xlsx |
|---|---|---|
| `C11_CHK-DRIFT_30_501.xlsx` | 494.01 | `#272~00001@18_18_30_501.sum.xlsx` |
| `C13_AIR_G_18_089.xlsx` | 057.01 | `#272~00002@18_32_18_089.sum.xlsx` |
| `C14_AIR_G_15_502.xlsx` | 499.01 | `#272~00003@18_42_15_502.sum.xlsx` |
| `W00_BLOCK_P2-8a_G_rep-1_06_676.xlsx` | 674.01 | `#272~00005@18_53_06_676.sum.xlsx` |
| `R1-1_BLOCK_P5-K_G_rep-1_21_367.xlsx` | 363.01 | `#272~00006@18_58_21_367.sum.xlsx` |
| `R1-2_BLOCK_P3-La_G_rep-1_29_491.xlsx` | 489.01 | `#272~00007@19_02_29_491.sum.xlsx` |
| `R1-3_BLOCK_P3-Lb_G_rep-1_59_104.xlsx` | 102.01 | `#272~00008@19_06_59_104.sum.xlsx` |
| `R1-4_BLOCK_P2-8a_G_rep-1_52_713.xlsx` | 711.01 | `#272~00009@19_12_52_713.sum.xlsx` |
| `AR1_AIR_G_41_475.xlsx` | 473.01 | `#272~00010@19_17_41_475.sum.xlsx` |
| `R2-1_BLOCK_P3-La_G_rep-2_56_061.xlsx` | 059.01 | `#272~00011@19_20_56_061.sum.xlsx` |
| `R2-2_BLOCK_P2-8a_G_rep-2_16_610.xlsx` | 607.01 | `#272~00012@19_26_16_610.sum.xlsx` |
| `R2-3_BLOCK_P5-K_G_rep-2_00_567.xlsx` | 564.01 | `#272~00013@19_30_00_567.sum.xlsx` |
| `R2-4_BLOCK_P3-Lb_G_rep-2_48_077.xlsx` | 074.01 | `#272~00014@19_34_48_077.sum.xlsx` |
| `AR2_AIR_G_15_742.xlsx` | 740.01 | `#272~00017@19_40_15_742.sum.xlsx` |
| `R3-1_BLOCK_P5-K_G_rep-3_21_464.xlsx` | 462.01 | `#272~00018@19_43_21_464.sum.xlsx` |
| `R3-2_BLOCK_P3-La_G_rep-3_25_778.xlsx` | 770.01 | `#272~00019@19_46_25_778.sum.xlsx` |
| `R3-3_BLOCK_P3-Lb_G_rep-3_37_992.xlsx` | 989.01 | `#272~00020@19_49_37_992.sum.xlsx` |
| `R3-4_BLOCK_P2-8a_G_rep-3_40_520.xlsx` | 517.01 | `#272~00021@19_52_40_520.sum.xlsx` |
| `AR3_AIR_G_33_134.xlsx` | 132.01 | `#272~00022@19_55_33_134.sum.xlsx` |
| `AQ-1_BLOCK_P1-6_G_rep-1_55_344.xlsx` | 342.01 | `#272~00023@20_00_55_344.sum.xlsx` |
| `AQ-2_BLOCK_P2-8b_G_rep-1_43_896.xlsx` | 894.01 | `#272~00024@20_03_43_896.sum.xlsx` |
| `AQ-3_BLOCK_P2-8b_G_rep-2_28_798.xlsx` | 795.01 | `#272~00025@20_06_28_798.sum.xlsx` |
| `AQ-4_BLOCK_P1-6_G_rep-2_44_486.xlsx` | 483.01 | `#272~00026@20_08_44_486.sum.xlsx` |
| `AQ-5_BLOCK_P1-6_G_rep-3_45_530.xlsx` | 523.01 | `#272~00027@20_10_45_530.sum.xlsx` |
| `AQ-6_BLOCK_P2-8b_G_rep-3_06_371.xlsx` | 369.01 | `#272~00028@20_13_06_371.sum.xlsx` |
| `AQ-air_AIR_G_04_127.xlsx` | 125.01 | `#272~00029@20_15_04_127.sum.xlsx` |
| `C17_CHK-DRIFT_31_825.xlsx` | 822.01 | `#272~00031@20_17_31_825.sum.xlsx` |
