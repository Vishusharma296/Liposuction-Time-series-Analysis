## Dataset Documentation & Metadata Specification
This documentation file serves as the definitive structural and context guide for the 17 experimental sensor datasets (V1 to V17) collected during water-jet assisted liposuction (WAL) validation procedures. It details the data acquisition architecture, preprocessing loops, structural labeling conventions, and algorithmic features mapped to the master's thesis data architecture from the University of Rostock.
------------------------------
## 1. Project Background & Objective
The primary engineering task of the pipeline is automated multi-class tissue characterization. Using a single inline mechanical pressure transducer, the machine learning models are trained to:

* Distinguish artificial, synthetic hydrogel tissue formulations (phantoms) from ex-vivo human abdominal adipose tissue (menschliches Fettgewebe).
* Evaluate the bio-fidelity of different phantom recipes by tracking model confusion trends and replication match indices.

------------------------------
## 2. Experimental Hardware & Signal Acquisition Setup

* Surgical Device Platform: Human Med AG body-jet clinical water-jet assisted liposuction device.
* Transducer Sub-System: A Burster Model 8438-5100 Miniature Ring Load Cell based on piezoresistive strain gauge (DMS) technology.
* Mechanical Integration: The ring sensor features a 5mm central bore, integrated directly behind the stainless-steel cannula within a custom 3D-printed adapter shroud (produced via Fused Deposition Modeling and MultiJet Modeling) to record axial forces without obstructing fluid suction pathways.
* Logging Constraints:
* Sampling Rate: Continuous tracking at 100 Hz ($dt = 0.01\text{ s}$), exceeding standard baseline research setups to preserve transient mechanical behaviors.
   * Software Interface: Real-time signal streaming conducted via USB interface into the Burster DigiVision digital instrumentation logging suite.
   * Recording Window: Minimum sequence duration of 80 seconds per file.

------------------------------
## 3. File Directory & Class Categorization Reference
The 17 data spreadsheets map to distinct material compounds (Classes) and machine operating variables (Device Configurations):
## A. Target Materials (The 4 Machine Learning Prediction Classes)

   1. menschliches Fettgewebe (Human Adipose Tissue): Native biological reference tissue extracted ex-vivo from abdominal surgeries.
   2. Phantom 1: A composite heterogeneous specimen consisting of a 12% (m/m) water-gelatine base embedded with approximately 400 pre-cast 2% agar hemispheres (200 ml total volume) to replicate multi-layered tissue textures.
   3. Phantom 2: A soft, compliant, homogeneous gel block formulated from a 2% (m/m) Agar-Water mixture.
   4. Phantom 3: A highly rigid, dense, homogeneous gel block formulated from a 4% (m/m) Agar-Water mixture.

## B. Device Configurations (Operating Parameters)

* Configuration A: Pure mechanical cannula translation into the substrate. Fluid infiltration pump and vacuum suction are completely turned off.
* Configuration B: Suction active. Vacuum pump engaged at a stable operating pressure of 500 mmHg; fluid infiltration jet turned off.
* Configuration C: Full operational WAL simulation. Continuous vacuum suction active at 500 mmHg coupled with an active fächerförmig (fan-shaped) pulsating water-jet set to Range 2 of 5 (generating localized fluid micro-jets up to 110 bar).

## C. Point-to-Point Master Mapping Table
The 17 workspace files trace to the experimental matrix:

| Index | Target Filename | Decoded Tissue Class | Operating Profile |
|---|---|---|---|
| 0 | V1 Erik ohne Vakuum ohne Wasser 1.xlsx | Phantom 3 (4% Agar) | A (Mechanical Only) |
| 1 | V10 Eric mit Vakuum ohne Wasser 3.xlsx | Phantom 3 (4% Agar) | B (Suction Active) |
| 2 | V11 Eric ohne Vakuum ohne Wasser 1.xlsx | Phantom 3 (4% Agar) | A (Mechanical Only) |
| 3 | V12 Eric ohne Vakuum ohne Wasser 2.xlsx | Phantom 2 (2% Agar) | A (Mechanical Only) |
| 4 | V13 Eric ohne Vakuum ohne Wasser 3.xlsx | Phantom 3 (4% Agar) | A (Mechanical Only) |
| 5 | V14 Eric Variation normal langsam schnell.xlsx | Phantom 3 (4% Agar) | Variable Operator Speed |
| 6 | V15 Eric mit Vakuum mit Wasser 1.xlsx | Phantom 3 (4% Agar) | C (Full WAL Mode) |
| 7 | V16 Eric mit Vakuum mit Wasser 2.xlsx | Human Adipose Tissue | C (Full WAL Mode) |
| 8 | V17 Eric mit Vakuum mit Wasser 3.xlsx | Human Adipose Tissue | C (Full WAL Mode) |
| 9 | V2 Erik ohne Vakuum ohne Wasser 2.sum.xlsx | Phantom 2 (2% Agar) | A (Mechanical Only) |
| 10 | V3 Erik ohne Vakuum ohne Wasser 3.sum.xlsx | Phantom 3 (4% Agar) | A (Mechanical Only) |
| 11 | V4 Erik mit Vakuum ohne Wasser 1.xlsx | Phantom 2 (2% Agar) | B (Suction Active) |
| 12 | V5 Erik mit Vakuum ohne Wasser 2.xlsx | Phantom 2 (2% Agar) | B (Suction Active) |
| 13 | V6 Erik mit Vakuum ohne Wasser 3.xlsx | Phantom 2 (2% Agar) | B (Suction Active) |
| 14 | V7 Erik Variation normal langsam schnell.xlsx | Phantom 2 (2% Agar) | Variable Operator Speed |
| 15 | V8 Eric mit Vakuum ohne Wasser 1.xlsx | Phantom 3 (4% Agar) | B (Suction Active) |
| 16 | V9 Eric mit Vakuum ohne Wasser 2.xlsx | Human Adipose Tissue | B (Suction Active) |

------------------------------
## 4. Tabular Structure & Internal Column Definitions
Each individual spreadsheet contains an identical 18-line plaintext device configuration header block (e.g., Messprotokolldatei, Anzahl Messwerte), which is skipped positionally. The structural tabular data matrix starting at Row 19 tracks three continuous arrays:

   1. Zähler (Index / Column 0): A continuous, whole-number integer stepping counter vector logging tracking points sequentially from 0 to the run termination boundary ($N \approx 7,000 \text{ to } 8,600$).
   2. Zeit [s] (Time / Column 1): The temporal runtime array tracking the exact elapsed duration of the surgical session in seconds (Resolution: 0.01s steps).
   3. Messwert / Kraft [N] (Force / Column 2): The physical load cell output string array tracking axial forces in Newtons ($N$).
   * Compression Resistance: Represented by positive scalar force paths ($+N$), mapping the insertion stress during the inward stroke.
      * Viscoelastic Adhesion: Represented by negative scalar force paths ($-N$), mapping tissue stiction, drag friction, and surface tension pulling backward against the inline sensor head during the tool retraction stroke.
   
------------------------------
## 5. Algorithmic Feature Engineering & Preprocessing Guidelines
To prepare the continuous sensor streams for the machine learning classifiers, the raw signals are processed through two distinct strategies:
## A. Digital Signal Conditioning Stack

* Baseline Subtraction: Linear detrending can be selectively used to eliminate slow sensor drift caused by mechanical pre-tension or tool-tightening offsets during assembly. However, to extract Eric's exact absolute values, raw baseline extraction must be used since the true human tissue mean rests at a non-zero baseline of -0.7055 N.
* Savitzky-Golay Filter: Smooths electronic background noise from the transducer. Configured with a polynomial order of 1 and a window size of 101 or 251 to preserve sharp material puncture boundaries.

## B. Machine Learning Input Frameworks

* Dataset Variant A (TSC Neural Format): Continuous time-series slices are linearly interpolated to fixed length shapes (e.g., $L=5000$) to feed directly into the XceptionTime (XTM) deep neural network. This allows depthwise separable convolutional filters to learn raw wave contours automatically.
* Dataset Variant B (Engineered Tabular Format): Long files are split into smaller augmentation windows ($W=500$, representing 5-second active blocks) to extract 6 structural statistical predictors for training XGBoost (XGB) and Random Forest (RF) models:
1. Mean Force ($N$): The baseline resistance threshold of the substrate matrix.
   2. Standard Deviation ($N$): Measures cannula translation fluctuations to differentiate homogeneous gels from multi-layered matrices.
   3. Minimum Force ($N$): Captures viscoelastic adhesion pull during cannula retraction.
   4. Maximum Force ($N$): Tracks absolute penetration peak failure limits.
   5. Peak-to-Peak ($N$): The absolute mechanical range indicating general material elasticity.
   6. Signal Variance: Captures fine-scale micro-texture differences in the substance layer.

