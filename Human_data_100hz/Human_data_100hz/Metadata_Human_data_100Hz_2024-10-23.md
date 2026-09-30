# Dataset S1: human-tissue session 23 Oct 2024 (17 recordings)

Metadata for the 17 legacy 100 Hz recordings V1–V17 (Eric Schwarz's session). Compiled 30 Sep 2026 (V7/V14 states added 30 Sep, 16:10) from `Metadata_verified_2026-09-28.csv` and `Legacy_Data_Verification_28Sep.md`, whose sources are the DigiVision file headers, the file start times, the data themselves, the professor's `V_Overview.txt` and Schwarz's thesis. Nothing here is taken from the old `Metadata.md`, which is left unchanged.

> All 17 recordings are ex-vivo human abdominal adipose tissue from two tissues, one per operator (Erik: T1, V1–V7; Eric: T2, V8–V17). None is a phantom. The trailing digit 1/2/3 in the file names is the repeat number, not a phantom type; the old folder labels `Artificial_Phantom/Sample_1–3`, 'Phantom_1/2/3', 'L1–L3' and 'Adipose_1/2' are wrong.

## 1. Setup and session facts

| Item | Value |
|---|---|
| Session ID | S1 (thesis Table: S1; earlier suggested label D0) |
| Date, time | 23 Oct 2024, 14:59:57 to 15:38:38 (about 38 min, one continuous session) |
| Specimen | Two human tissues, one per operator (confirmed 30 Sep): tissue H-2024-10-23-T1 with Erik (V1–V7), tissue H-2024-10-23-T2 with Eric (V8–V17). The change falls in the 3 min gap between V7 and V8. Abdominal wall from liposuction patients (Schwarz); no donor demographics reported |
| Material | human abdominal adipose tissue, ex vivo |
| Ethics basis | not stated in the files; predates A 2025-0012 [CONFIRM] |
| Operators | 2: Erik (O1, V1–V7) and Eric (O2, V8–V17), per V_Overview.txt ('2 operators (Erik and Eric)') and filename tokens. Anonymise as O1/O2 in the thesis |
| Handpiece | earlier 3D-printed adapter (Schwarz), not the stainless-steel prototype of the 2026 sessions; Schwarz reports the adapter leaked, so effective vacuum was below nominal, and describes a decreasing adapter preload |
| Sensor | burster load cell, device SN_704988, channel 01, unit N |
| Software, rate | DigiVision, 100 Hz nominal (100.0 Hz measured), no timing gaps in any file |
| Acquisition PC | Eric Schwarz's PC, protocol path `…\Masterarbeit\Versuche\2024\1023\01\` |
| Execution | freehand; specimen held by hand; no bench (Schwarz §4.6) |
| Recording protocol | about 80 s: idle with the cannula inserted, about 60 s of strokes, idle |
| Device states | A: no vacuum, no water; B: vacuum 500 mmHg, no water; C: water Range 2 of 5 + vacuum 500 mmHg (Schwarz §4.6). Levels are nominal |
| Stroke length, depth, rate | not recorded; no cue track |
| Design | operator (Erik, Eric) × state (A, B; C for Eric only) × 3 consecutive repeats, plus one speed-variation recording per operator |
| Quantisation | 0.0001 N |
| Copies | Force arrays of all 17 xlsx files are sample-for-sample identical to the CSVs in `Data_csv/Artificial_Phantom/Sample_1–3/` and `Data_csv/Adipose_Tissue/V7, V14` and to the xlsx files in `Clean _Data`; `force_hash` in the CSV links them |

## 2. Timeline

| Time | Block | Operator | State | Files | Gaps between files |
|---|---|---|---|---|---|
| 14:59:57–15:04:04 | 1 | Erik (O1), T1 | A | V1, V2, V3 | 11 s, 7 s |
| 15:06:09–15:10:29 | 2 | Erik (O1), T1 | B | V4, V5, V6 | 5 s, 17 s |
| 15:12:53–15:14:17 | 3 | Erik (O1), T1 | A, speed variation | V7 | — |
| 15:17:13–15:21:37 | 4 | Eric (O2), T2 | B | V8, V9, V10 | 12 s, 9 s |
| 15:22:50–15:27:03 | 5 | Eric (O2), T2 | A | V11, V12, V13 | 5 s, 3 s |
| 15:27:48–15:29:09 | 6 | Eric (O2), T2 | B, speed variation | V14 | — |
| 15:34:14–15:38:38 | 7 | Eric (O2), T2 | C | V15, V16, V17 | 19 s, 5 s |

Between blocks there are 1–5 min, enough to change the device setting or the specimen. The tissue was changed together with the operator, between V7 (ends 15:14:17) and V8 (starts 15:17:13). Within a block the next recording starts 3–19 s after the previous one ends, too short to change the specimen.

## 3. Recordings

Force statistics are on the raw signal (no baseline removal). Activity onset and active fraction use the 2 s rolling SD > 0.10 N rule; idle median is the median force before the activity onset.

| # | File | Material | Session ID | Block | Operator | Device state | Machine setting | Session type | Repeat | Start | End | Length (s) | Samples | Force min / max (N) | Mean (N) | SD (N) | Activity onset (s) | Idle median (N) | Active fraction | Used by Schwarz | Original file (folder/name) | Additional information |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | V1 | human abdominal adipose tissue | S1 | 1 | Erik (O1), T1 | A | none (motion only) | Freehand | 1 | 14:59:57 | 15:01:24 | 86.5 | 8650 | -2.40 / 3.60 | -0.13 | 0.75 | 12.8 | -0.43 | 0.73 | no | `Artificial_Phantom/Sample_1/V1 Erik ohne Vakuum ohne Wasser 1.xlsx` | First recording of the session. |
| 2 | V2 | human abdominal adipose tissue | S1 | 1 | Erik (O1), T1 | A | none (motion only) | Freehand | 2 | 15:01:35 | 15:02:45 | 70.4 | 7037 | -1.49 / 1.41 | 0.09 | 0.60 | 8.5 | 0.58 | 0.76 | no | `Artificial_Phantom/Sample_2/V2 Erik ohne Vakuum ohne Wasser 2.sum.xlsx` | Starts 11 s after V1 ends. Shortest recording of S1 (70 s). |
| 3 | V3 | human abdominal adipose tissue | S1 | 1 | Erik (O1), T1 | A | none (motion only) | Freehand | 3 | 15:02:52 | 15:04:04 | 71.7 | 7162 | -1.73 / 2.56 | 0.23 | 0.63 | 11.5 | 0.72 | 0.82 | no | `Artificial_Phantom/Sample_3/V3 Erik ohne Vakuum ohne Wasser 3.sum.xlsx` | Starts 7 s after V2 ends. |
| 4 | V4 | human abdominal adipose tissue | S1 | 2 | Erik (O1), T1 | B | vacuum 500 mmHg, no water | Freehand | 1 | 15:06:09 | 15:07:31 | 81.9 | 8187 | -2.45 / 2.23 | -0.97 | 0.69 | 0.0 | — | 0.91 | no | `Artificial_Phantom/Sample_1/V4 Erik mit Vakuum ohne Wasser 1.xlsx` | Activity from the first sample: no contact-free start, so no idle baseline. |
| 5 | V5 | human abdominal adipose tissue | S1 | 2 | Erik (O1), T1 | B | vacuum 500 mmHg, no water | Freehand | 2 | 15:07:36 | 15:08:48 | 72.7 | 7262 | -3.25 / 2.40 | -1.10 | 0.81 | 11.7 | -0.06 | 0.83 | no | `Artificial_Phantom/Sample_2/V5 Erik mit Vakuum ohne Wasser 2.xlsx` | Starts 5 s after V4 ends. |
| 6 | V6 | human abdominal adipose tissue | S1 | 2 | Erik (O1), T1 | B | vacuum 500 mmHg, no water | Freehand | 3 | 15:09:06 | 15:10:29 | 83.4 | 8337 | -3.39 / 1.11 | -1.27 | 0.78 | 10.9 | -0.42 | 0.72 | no | `Artificial_Phantom/Sample_3/V6 Erik mit Vakuum ohne Wasser 3.xlsx` | Starts 17 s after V5 ends. Mean falls across V4–V6 (−0.97, −1.10, −1.27 N). |
| 7 | V7 | human abdominal adipose tissue | S1 | 3 | Erik (O1), T1 | A | none (motion only) | Freehand, speed variation | — | 15:12:53 | 15:14:17 | 83.8 | 8375 | -3.94 / 3.82 | -2.33 | 0.85 | 10.9 | -3.16 | 0.74 | no | `Adipose_Tissue/V7 Erik Variation normal langsam schnell.xlsx` | Speed blocks (V_Overview.txt): 0–10 s idle, 10–30 s normal, 30–50 s very slow, 50–70 s very fast, 70–80 s idle. State A (no vacuum, no water), confirmed by the author 30 Sep; the old Metadata.md entry 'vacuum + water' is wrong. Old label Adipose_1 ('donor 1') is wrong. |
| 8 | V8 | human abdominal adipose tissue | S1 | 4 | Eric (O2), T2 | B | vacuum 500 mmHg, no water | Freehand | 1 | 15:17:13 | 15:18:33 | 80.4 | 8037 | -2.23 / 12.14 | 0.71 | 1.92 | 9.0 | 0.17 | 0.78 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_1/V8 Eric mit Vakuum ohne Wasser 1.xlsx` | Operator change: first recording by Eric, about 3 min after V7. |
| 9 | V9 | human abdominal adipose tissue | S1 | 4 | Eric (O2), T2 | B | vacuum 500 mmHg, no water | Freehand | 2 | 15:18:45 | 15:20:06 | 81.2 | 8112 | -4.31 / 13.13 | -1.12 | 2.21 | 9.1 | -0.99 | 0.77 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_2/V9 Eric mit Vakuum ohne Wasser 2.xlsx` | Starts 12 s after V8 ends. |
| 10 | V10 | human abdominal adipose tissue | S1 | 4 | Eric (O2), T2 | B | vacuum 500 mmHg, no water | Freehand | 3 | 15:20:15 | 15:21:37 | 81.5 | 8150 | -7.17 / 6.82 | -3.53 | 1.94 | 10.5 | -3.77 | 0.76 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_3/V10 Eric mit Vakuum ohne Wasser 3.xlsx` | Starts 9 s after V9 ends. Strong offset drift across V8–V10 (mean +0.71, −1.12, −3.53 N). |
| 11 | V11 | human abdominal adipose tissue | S1 | 5 | Eric (O2), T2 | A | none (motion only) | Freehand | 1 | 15:22:50 | 15:24:12 | 81.8 | 8175 | -2.32 / 9.65 | 0.58 | 2.14 | 9.8 | 0.15 | 0.76 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_1/V11 Eric ohne Vakuum ohne Wasser 1.xlsx` | Mean back near zero after V10 (offset recovers between blocks). |
| 12 | V12 | human abdominal adipose tissue | S1 | 5 | Eric (O2), T2 | A | none (motion only) | Freehand | 2 | 15:24:17 | 15:25:38 | 80.8 | 8075 | -3.00 / 7.46 | -1.26 | 1.65 | 11.0 | -1.99 | 0.75 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_2/V12 Eric ohne Vakuum ohne Wasser 2.xlsx` | Starts 5 s after V11 ends. |
| 13 | V13 | human abdominal adipose tissue | S1 | 5 | Eric (O2), T2 | A | none (motion only) | Freehand | 3 | 15:25:41 | 15:27:03 | 81.3 | 8125 | -5.59 / 18.12 | -1.75 | 3.24 | 10.9 | -2.32 | 0.75 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_3/V13 Eric ohne Vakuum ohne Wasser 3.xlsx` | Starts 3 s after V12 ends. Largest peak of Eric's state-A block (18.1 N). Mean falls across V11–V13 (+0.58, −1.26, −1.76 N). |
| 14 | V14 | human abdominal adipose tissue | S1 | 6 | Eric (O2), T2 | B | vacuum 500 mmHg, no water | Freehand, speed variation | — | 15:27:48 | 15:29:09 | 80.2 | 8012 | -6.84 / 14.96 | -2.16 | 4.06 | 9.0 | -5.56 | 0.79 | no | `Adipose_Tissue/V14 Eric Variation normal langsam schnell.xlsx` | Speed blocks, same filename pattern as V7 (segment times assumed as V7). State B (vacuum, no water), confirmed by the author 30 Sep; the old Metadata.md entry 'vacuum + water' is wrong. Largest SD in S1 (4.06 N). Old label Adipose_2 ('donor 2') is wrong. |
| 15 | V15 | human abdominal adipose tissue | S1 | 7 | Eric (O2), T2 | C | water Range 2 of 5 + vacuum 500 mmHg | Freehand | 1 | 15:34:14 | 15:35:34 | 80.0 | 8000 | -2.63 / 18.45 | 1.37 | 3.19 | 9.9 | -0.60 | 0.77 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_1/V15 Eric mit Vakuum mit Wasser 1.xlsx` | About 5 min after V14 (longest gap in S1; water jet switched on). Largest peak in S1 (18.4 N). |
| 16 | V16 | human abdominal adipose tissue | S1 | 7 | Eric (O2), T2 | C | water Range 2 of 5 + vacuum 500 mmHg | Freehand | 2 | 15:35:53 | 15:37:13 | 80.0 | 8000 | -4.74 / 7.22 | -0.80 | 1.96 | 9.7 | -1.71 | 0.79 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_2/V16 Eric mit Vakuum mit Wasser 2.xlsx` | Starts 19 s after V15 ends. |
| 17 | V17 | human abdominal adipose tissue | S1 | 7 | Eric (O2), T2 | C | water Range 2 of 5 + vacuum 500 mmHg | Freehand | 3 | 15:37:18 | 15:38:38 | 80.7 | 8062 | -3.75 / 7.55 | -0.55 | 1.60 | 2.8 | -1.43 | 0.77 | yes (Table 5 human row, ML human class) | `Artificial_Phantom/Sample_3/V17 Eric mit Vakuum mit Wasser 3.xlsx` | Starts 5 s after V16 ends. Short contact-free start (activity from 2.8 s). Last recording of the session. |

## 4. Groups for analysis

| Group | Files | Use in this thesis |
|---|---|---|
| State A, Erik (O1) | V1–V3 | secondary human reference for RQ4 (other operator; sensitivity analysis only) |
| State A, Eric (O2) | V11–V13 | secondary human reference for RQ4 (other operator; sensitivity analysis only) |
| Operator-and-tissue difference | V1–V6 (Erik, T1) vs V8–V13 (Eric, T2), same states A and B | effect budget: combined operator + tissue scale (not separable) |
| State effect within operator and tissue | Erik A/B (T1); Eric A/B/C (T2) | effect budget: device-state scale (confounded with block order and drift) |
| Speed variation | V7 (Erik, T1, state A), V14 (Eric, T2, state B); the two differ in operator, tissue and state | effect budget: speed scale; stroking-window and activity-mask threshold checks |
| Schwarz's analysed human class | V8–V13, V15–V17 (9 files) | reproduces his Table 5 human row exactly (mean −0.7054 N, SD 2.2043 N, min −3.9705 N, max 11.1706 N; only matching subset) |

## 5. Variables to consider in the analysis

- Operator and tissue (confounded, see below): Erik's recordings have SD 0.60–0.85 N, Eric's 1.60–3.24 N (V14 4.06 N); about ×3.6 on spread. Operator is the largest difference in this session.
- Device state (A, B, C; V7 A, V14 B), always confounded with block order and time within the session; C exists for Eric only.
- Offset drift within blocks: per-recording means fall across consecutive repeats (Erik B −0.97, −1.10, −1.27 N; Eric B +0.71, −1.12, −3.53 N; Eric A +0.58, −1.26, −1.76 N), consistent with the decreasing adapter preload Schwarz describes. Use per-recording baselines; fluctuation descriptors are not affected by a constant offset.
- Missing contact-free start: V4 is active from the first sample, V17 from 2.8 s, so their idle baselines are missing or short.
- Adapter: earlier 3D-printed adapter that leaked; effective vacuum below the nominal 500 mmHg, and the mechanical coupling differs from the stainless-steel handpiece used in 2026.
- Specimen handling: held by hand, no bench; stroke length, depth and rate not controlled or recorded, no cue track.
- Speed-variation recordings: V7 in state A, V14 in state B (author, 30 Sep). Segment times from V_Overview.txt for V7; V14 assumed the same. V7 and V14 differ in operator, tissue and state, so the speed effect is read within each recording (fast vs slow segment), never between them.
- Sampling rate 100 Hz (the 2026 human sessions are 10 Hz). Comparison with the 10 Hz references uses the common 10 Hz track (Section 3.4).
- Two tissues, one per operator: operator and tissue are fully confounded. The Erik-vs-Eric difference (about ×3.6 on spread) is operator plus tissue plus time, not an operator effect alone; report it as a combined operator-and-tissue difference, an upper bound for either. State and speed effects remain within one tissue and one operator.
- Repeat number (1/2/3) is time order within the block, so it is confounded with drift.

## 6. Open confirmations

- [CONFIRM] Ethics basis of S1 (predates A 2025-0012)?
- [CONFIRM] Operator identities for the acknowledgements only; thesis text uses O1/O2.

## 7. File copies

The 17 xlsx files are copied unchanged (SHA-256 identical to the source) into `Desktop\Sensor_DATA_Complete_Thesis_Task\Human_data_100hz\`, with this file. Source: `Clean _Data\Artificial_Phantom\Sample_1–3\` (V1–V6, V8–V13, V15–V17) and `Clean _Data\Adipose_Tissue\` (V7, V14). File names are the original ones; the folder names 'Artificial_Phantom' and 'Adipose_Tissue' in the source are wrong labels and were not carried over.
