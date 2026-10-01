Project Description
Master's thesis: Development of a test setup for data-based evaluation of artificial fat tissue Author: Manish Joshi, Chair of Microfluidics, University of Rostock

1. Project description

Liposuction depends heavily on the surgeon's tactile experience. Yet no training models exist whose mechanical behaviour has been shown to match human fat. Artificial tissue phantoms made from hydrogels could fill this gap. However, their fidelity is usually judged by appearance or by standard material tests, and neither reproduces the loading during water-assisted liposuction (WAL). In WAL a cannula reciprocates through the tissue while a pulsed water jet and suction act at its tip.

This thesis develops and evaluates a data-based method for comparing phantoms with human adipose tissue under the procedure itself. The method uses the axial force measured by a ring load cell (burster 8438, ±100 N, strain-gauge full bridge) in the handpiece of a commercial WAL system (body-jet). The force is recorded with DigiVision at 100 Hz. The project has five parts: test bench, phantoms, measurements, data analysis, and outputs.

1.1 Test bench

A modular bench consists of:

an aluminium-profile frame;
a linear rail and carriage that guide the handpiece along one axis;
end stops that fix the stroke length at 80 mm;
a perforated tray with a screw-driven clamping disc that holds the specimen in a defined position.

The aim is that the recorded force reflects the specimen more than the operator's handling. Stroke rate is paced by an acoustic cue at 1.9 Hz. Velocity is not mechanically fixed, so it remains a stated limitation.

1.2 Phantoms

Five gelatin-based formulations are designed so that each pairwise comparison isolates one compositional factor:

ID	Composition	Isolates
P1	6 % gelatin	baseline matrix
P2	8 % gelatin	gelatin concentration (vs P1)
P3	8 % gelatin + agar–gelatin lobules	lobules without network (vs P2)
P4	6 % gelatin + 1 % chitosan	chitosan second network (vs P1)
P5	P4 + lobules + microhollow spheres	inclusions with network (vs P4)

All formulations share 30 % ethanol and 2 % glycerol. Cast date, age at test, mount and mass change are recorded per block. In total, 11 blocks were tested; P2 and P3 have two blocks each in state C, so the variation between blocks can be estimated.

1.3 Measurements

Phantom sessions:

28 Sep 2026, state A (water jet and vacuum off): one block per formulation, 4 freehand and 4 guided runs per block at fresh insertion sites, 39 runs in total.
29 Sep 2026, state C (water jet Range 3 + vacuum on): guided runs on six blocks. The clamped blocks were interleaved in rounds, so material is not tied to a time slot.

Each run lasts about 80 s: 10 s still, 60 s of strokes, 10 s still.

Sensor-chain checks bracket every session:

zero-drift recordings;
axial pulls to confirm the sign convention;
strokes in air, which measure the handpiece's own dynamics and the load added by jet and vacuum without a specimen.

Human reference: ex-vivo human abdominal fat, freehand, recorded in five sessions (2024–2026):

Session	Donors	Rate	Notes
S1 (2024)	2	100 Hz	earlier 3D-printed adapter; operator and donor coincide
S2 (Dec 2025)	1	10 Hz	five operators
S3 (Mar 2026)	1	10 Hz	the author, states A/B/C, with the bench handpiece
S4 (Mar 2026)	1	10 Hz	
S5 (Apr 2026)	1	10 Hz	device state not recorded
1.4 Data analysis

The analysis turns each raw (time, force) recording into a small set of interpretable numbers. It answers each research question at the level of independent units: phantom blocks and human donors, never windows or repeated recordings.

(a) Data structure and audit.

Hierarchy. Every file is placed in the hierarchy:
for phantoms: formulation → cast → block → insertion (recording) → 10-s window;
for human tissue: donor → operator → device state → recording → window.
Confound audit. Before any analysis, classifiers that see only acquisition metadata (start time, mount, round, day, block age, sampling rate) are run to measure how much of the material label is predictable without force data. Variables that coincide with the material are reported as confounds next to every result.

(b) Signal processing.

Admission. Recordings are split at timing gaps and only regularly sampled stretches are kept; nothing is interpolated.
Phase detection.
Bench runs: the stroke phase is the longest active stretch of a rolling-SD activity detector.
Human recordings: an activity mask removes pauses and repositioning.
Baseline. Each run is referenced to its own contact-free baseline, which removes tare offsets and sensor-reseating steps.
Artefact masks. Artefacts documented on the run sheets are masked before windowing; impact transients are flagged.
Two analysis tracks.
The native 100 Hz track is used for phantom–S1 comparisons.
An anti-aliased 10 Hz track (zero-phase FIR low-pass filter, then decimation) is used for comparisons that include the 10 Hz human sessions.
A dedicated test measures how much each descriptor is distorted by the 10 Hz reduction, in units of the scatter between insertions. Only descriptors that survive it are used on the 10 Hz track.
Descriptors. Nine offset-invariant descriptors in four families are computed on non-overlapping 10-s windows (5 s and 20 s as variants):
spread: standard deviation (the force-fluctuation amplitude, the primary descriptor), interquartile range, 5th–95th percentile range;
shape: skewness, excess kurtosis;
rate: 95th percentiles of loading and unloading rate;
spectrum: spectral centroid and normalised spectral entropy in 0.1–5 Hz (Welch estimate).
The stroke cadence and the mean force above baseline are reported separately. Each recording is summarised by the median of its windows.

(c) RQ1: repeatability and the effect of the bench.

Primary endpoint. The scatter between repeat insertions of log(window SD) within each block is compared between freehand and guided runs with an F-test, reported as an SD ratio with a 95 % CI and the minimum detectable ratio.
Supporting analyses:
guided/freehand response ratios for every descriptor (block fixed effects, robust HC3 errors);
ICC(1) for the share of variance between specimens;
the repeatability coefficient in newtons.

(d) RQ2: effect of composition.

State A. Four planned single-factor contrasts (P2–P1, P3–P2, P4–P1, P5–P4) on the window SD, as ratios with 95 % CIs and Holm correction. They are labelled specimen-level because each formulation has one block. A within-block time-trend bound checks whether drift over the session could explain a contrast.
State C. The two pairs of twin blocks (La/Lb, 8a/8b) give the variation between blocks of one formulation. This is the benchmark a recipe effect must exceed. A formulation-level contrast (P3 vs P2, two blocks each) is then estimated.
Effect budget. Composition, execution, operator, device-state and stroke-speed effects are placed on one multiplicative axis.

(e) RQ3: distinguishing materials.

Models. Fixed, untuned models: majority baseline, L2 logistic regression and a shallow random forest. Scaling is fitted on training data only.
Validation. All windows of a held-out unit stay together:
the primary test trains on one block per formulation and predicts unseen blocks (P2 vs P3);
leave-one-recording-out is used for single-block formulations.
Controls:
negative controls: two blocks of the same material must not be separated better than different materials;
metadata-only baselines under the same folds;
a window-random split, reported only to show how much pseudoreplication inflates accuracy.
Metrics. Held-out blocks correct, recording-level accuracy with Wilson 95 % CIs, and per-class results.

(f) RQ4: similarity to human tissue.

Two-tier human reference:
tier 1: all nine descriptors at 100 Hz against the two S1 donors (matched device state and execution);
tier 2: spread descriptors on the 10 Hz track against all donors in the same device state, including the author's own operator-matched recording.
Distance. Descriptors are standardised by the human data only. The primary distance D is a family-weighted Euclidean distance from each phantom recording to the human centre. Wasserstein-1 and kernel MMD² serve as alternative metrics.
Human scale. D is expressed as a relative index, RI = D / (distance between human donors). RI ≤ 1 means a phantom lies within the variation between human donors.
Uncertainty. A bootstrap with 2000 resamples (recordings within blocks and within donors) gives each formulation's probability of ranking first and confidence intervals for its distance gap to the best formulation.
Robustness.
The ranking is recomputed across metrics, window lengths, descriptor families and human references (135 scenarios). Agreement is summarised with Kendall's W.
Leave-one-donor-out and single-donor rankings check whether one donor drives the result.
Claim rule. A pre-committed rule decides whether a single closest formulation can be named, or only a group that cannot be separated. Equivalence is never claimed.

(g) Software and reproducibility. The pipeline is written in Python (NumPy, pandas, Matplotlib), with statistics and classifiers implemented and checked against textbook values. One script reproduces every table and figure from the raw DigiVision exports, with fixed seeds and a logged manifest. Every departure from the pre-specified analysis plan is recorded as a deviation.

1.5 Outputs

The measured force is treated as the response of the tool–specimen–procedure system, not as a material property. The outcomes are:

a reusable acquisition and analysis methodology;
a ranking of the tested formulations stated with its uncertainty and robustness;
an assessment of how reliably materials can be distinguished once confounding is controlled;
evidence-based recommendations for phantom development and future data collection.

It is not a claim that any phantom is equivalent to human tissue.
