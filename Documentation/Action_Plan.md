# ML Model Training Action Plan

## Objective
Train machine learning models to determine which artificial phantoms most closely mimic human adipose tissue and quantify the fidelity of each phantom's behavior.

---

## Understanding Your Data Structure

### Current Data Assets (Updated)

**Real Human Tissue Samples:**
- Adipose_1 through Adipose_5 (5 samples)
- Multiple test runs per sample with varying conditions
- Adipose_3 has dual sampling rates (100 Hz and 10 Hz variants)

**Artificial Phantom Samples:**
- Phantom_1, Phantom_2, Phantom_3 (3 samples)
- Each has multiple test runs under different conditions
- Consistently sampled at 100 Hz

**Test Conditions:**
- Vacuum: ON/OFF
- Water (jet-assisted liposuction): ON/OFF
- Insertion speeds: slow, normal, fast (varies by tissue type)

**Sampling Rates:**
- 100 Hz: Adipose_1, Adipose_2, Phantom_1-3, Adipose_3 (selected runs)
- 10 Hz: Adipose_3, Adipose_4, Adipose_5 (primary sampling)

**Data Format:**
- Primarily `.sum` files (binary sensor dumps)
- Some `.csv` files for processed data
- **Metadata.md** catalogs all recordings with tissue type, sampling frequency, file names, and test condition descriptions

### Metadata.md Summary

The repository now includes comprehensive metadata tracking:

| Tissue Type | Count | Sampling Frequency | Key Characteristics |
|-------------|-------|-------------------|-------------------|
| **Phantom_1** | 5 recordings | 100 Hz | Baseline phantom; tested with vacuum/water variations |
| **Phantom_2** | 5 recordings | 100 Hz | Second phantom formulation; tested with vacuum/water variations |
| **Phantom_3** | 5 recordings | 100 Hz | Third phantom formulation; tested with vacuum/water variations |
| **Adipose_1** | 2 recordings | 100 Hz | Insertion speed variations (normal, slow, fast); vacuum ON + water ON |
| **Adipose_2** | 2 recordings | 100 Hz | Insertion speed variations (normal, slow, fast); vacuum ON + water ON |
| **Adipose_3** | 6 recordings | 10 Hz + 100 Hz | Real tissue; multiple trials under consistent conditions |
| **Adipose_4** | 2 recordings | 10 Hz | Real tissue; duplicate file naming suggests data quality check |
| **Adipose_5** | 4 recordings | 10 Hz | Real tissue; comprehensive condition testing (vacuum/water variations) |

**Total Dataset:** 32 recordings across 8 tissue samples

### Critical Questions to Answer

1. **Data Format & Availability** ✓ *Updated*
   - All `.sum` files are documented in Metadata.md
   - Metadata provides sampling frequency and condition descriptions for each file
   - **Action:** Confirm binary format specifications and parsing requirements

2. **Ground Truth Definition**
   - Adipose_3 and Adipose_5 have comprehensive condition coverage
   - Adipose_1, Adipose_2 focus on insertion speed variations
   - **Decision Needed:** Should ground truth weight all real tissue equally or prioritize high-frequency samples?

3. **Phantom Formulation Data**
   - Are the exact gelatin/chitosan/glycerol ratios known for Phantom_1, Phantom_2, Phantom_3?
   - Is this data available in the repository, or needs to be added?

4. **Data Quality** ✓ *Partially Updated*
   - Adipose_4 has duplicate filenames suggesting redundancy or validation runs
   - Metadata shows consistent test conditions for each tissue type
   - **Action:** Verify all files are complete and uncorrupted

---

## High-Level Strategy

### Phase 1: Establish Baseline Understanding

**Goal:** Can we reliably distinguish real tissue from artificial phantom?

**Approach:**
- Visualize raw force-time traces side-by-side for real vs. phantom
- Compare signal characteristics under different conditions (vacuum, water, speed)
- Investigate whether the bench-stabilized vs. freehand distinction (Objective 1 in thesis) is visible in raw data
- Document qualitative observations: noise patterns, peak magnitudes, recovery behavior
- Leverage Adipose_3 and Adipose_5's multi-condition coverage for robust comparison

**Why This Matters:**
- Visual patterns inform feature engineering strategy
- If raw signals are indistinguishable, ML models won't perform well
- Identifies which conditions most clearly reveal tissue differences
- Multi-frequency sampling (100 Hz vs. 10 Hz) may reveal different signal characteristics

**Deliverable:** Visualization report with comparative signal plots and frequency analysis

---

### Phase 2: Design Feature Engineering Strategy

**Goal:** Reduce high-dimensional time-series data into a compact numerical fingerprint.

**Three Feature Categories to Consider:**

**1. Static Properties (single numbers per recording):**
- Peak force (maximum recorded force)
- Average force (mean over recording duration)
- Force variability (standard deviation, coefficient of variation)
- Min/max force and range
- Measures of signal roughness (derivative-based metrics)

**2. Dynamic Properties (how signal evolves):**
- Energy required (integral of force over time)
- Rate of force change (speed to reach peak)
- Force recovery behavior (how quickly force drops after peak)
- Time to peak force
- Slope changes and inflection points

**3. Frequency Content (spectral characteristics):**
- Dominant frequency bands
- Spectral entropy (measure of spectral complexity)
- Peak frequency location
- Frequency distribution shape (multiple peaks vs. smooth rolloff)
- High-frequency noise vs. low-frequency trends
- **Note:** Consider aliasing effects when comparing 10 Hz vs. 100 Hz data

**Physiological Rationale:**
- Real adipose tissue has complex fiber networks → expect irregular force patterns
- Synthetic phantoms are more uniform → expect smoother, more predictable signals
- Frequency content may differ due to material composition differences
- Multiple sampling rates provide multi-scale temporal information

**Planning Decisions:**
- Which features have strongest biological justification?
- How to normalize features across different sampling rates (10 Hz vs. 100 Hz)?
- Should we use domain expertise to select features, or use automated feature importance methods?

**Deliverable:** Feature extraction pipeline with sampling-rate normalization and justification document

---

### Phase 3: Choose Classification Strategy

**Four options with trade-offs:**

#### Option A: Binary Classifier (Simplest)
- **Training:** All real tissue = "Class 1", All phantoms = "Class 0"
- **Output:** For unknown sample: is it real or fake? + confidence score
- **Pros:** Straightforward implementation; tells if sample is phantom-like
- **Cons:** Doesn't distinguish between different phantoms; less granular

#### Option B: Multi-class Classifier (More Granular)
- **Training:** Real = Class 0, Phantom_1 = Class 1, Phantom_2 = Class 2, Phantom_3 = Class 3
- **Output:** Which phantom (or real tissue) does this most resemble?
- **Pros:** Ranks phantoms by similarity to real tissue
- **Cons:** Requires more data per phantom; risk of overfitting; harder to generalize

#### Option C: Continuous Similarity Score / Ranking (Aligned with Thesis)
- **Approach:** Don't classify into buckets; compute continuous score from 0–1
- **Method:** Calculate distance from each phantom to real tissue "center" (mean of all real samples)
- **Output:** Phantom_2 = 0.87 fidelity, Phantom_1 = 0.72, Phantom_3 = 0.65 (ranked)
- **Pros:** Captures gradations; easier to optimize later; aligns with Objective 2 of thesis
- **Cons:** Depends on distance metric choice (Euclidean? Mahalanobis? Wasserstein?)

#### Option D: Hybrid Approach
- **Approach:** Use classifier probabilities as foundation, convert to fidelity score
- **Method:** Probability of being "real tissue" directly becomes fidelity metric
- **Pros:** Combines interpretability of classification with ranking capability
- **Cons:** Adds conversion step with arbitrary scaling choices

**Recommendation:** Option C (continuous scoring) best matches your thesis framing of "proximity ranking metric" (Objective 2)

---

### Phase 4: Handle Test Conditions

**The Complication:** Real tissue tested under multiple conditions (vacuum ON/OFF, water ON/OFF). Which is ground truth?

#### Strategy 1: Average Across All Conditions
- **Method:** Compute mean force signature across all real tissue samples and all conditions
- **Use as:** Single reference point for phantom comparison
- **Pros:** Robust to noise; captures "typical" real tissue behavior; maximizes training data
- **Cons:** Loses condition-specific insights; assumes conditions are interchangeable

#### Strategy 2: Condition-Matched Comparison
- **Method:** Compare each phantom tested under "Condition X" only to real tissue tested under "Condition X"
- **Pros:** Fair comparison; isolates material properties from equipment effects
- **Cons:** Requires sufficient data per condition; sparse conditions reduce statistical power
- **Note:** Adipose_3 and Adipose_5 have comprehensive condition coverage enabling this approach

#### Strategy 3: Hierarchical Scoring
- **Method:** Compute per-condition mimicry score, then average across all conditions
- **Pros:** Balances fairness and robustness; captures condition variance
- **Cons:** More complex implementation; needs appropriate weighting scheme

**Planning Decisions:**
- How much data exists per phantom per condition? (see Metadata.md)
- Are certain conditions (e.g., Vacuum ON + Water ON) more clinically relevant?
- Should we weight conditions by realism or equal importance?

**Recommended Approach:** Start with Strategy 3 (hierarchical scoring) leveraging Adipose_3 and Adipose_5's multi-condition data, then validate with Strategy 2 for specific high-value conditions

---

### Phase 5: Bridging to Optimization (Objective 3)

**End Goal:** Connect phantom ranking to formulation optimization

**The Logic:**
- If Phantom_1 (gelatin 10%, chitosan 2%, glycerol 5%) scores 0.72 fidelity
- And Phantom_2 (gelatin 12%, chitosan 1%, glycerol 4%) scores 0.87 fidelity
- Then: which component change(s) improved mimicry? (↑ gelatin? ↓ chitosan?)

**Requirements:**
- Mapping of phantom ID → exact formulation ratios (gelatin %, chitosan %, glycerol %)
- Sufficient phantom samples (ideally 5–10) to fit a surrogate model
- Surrogate model type (Gaussian Process Regression or polynomial regression) to predict fidelity from formulation

**Surrogate Model Workflow:**
1. Create dataset: (formulation_ratio_vector, fidelity_score) pairs
2. Train GP/polynomial to learn: fidelity = f(gelatin, chitosan, glycerol)
3. Query model: "What ratio achieves fidelity = 0.95?"
4. Validate predicted optimal formulation experimentally

**Planning Decision:**
- Do you have formulation ratios for the 3 current phantoms, or is this still being collected?

---

## Feature Engineering Deep Dive

### Candidate Features by Category

**Statistical Features (9 features):**
- Mean force
- Standard deviation
- Min force, max force, range
- Skewness, kurtosis
- Coefficient of variation

**Derivative-Based Features (4 features):**
- Mean absolute force rate (|dF/dt|)
- Max force rate
- Variance of force rate
- Number of zero-crossings in first derivative

**Energy Features (3 features):**
- Total energy (∫F dt)
- Energy in first half vs. second half (asymmetry)
- Peak power (max(dF/dt × F))

**Frequency-Domain Features (5 features):**
- Peak frequency (from FFT)
- Spectral entropy (disorder measure)
- Frequency centroid (weighted average frequency)
- Bandwidth (spread of frequencies)
- Power in high frequencies vs. low frequencies ratio

**Advanced Features (4 features):**
- Approximate entropy (regularity measure)
- Wavelet energy (multi-scale decomposition)
- Fractal dimension (Hurst exponent)
- Permutation entropy

**Total: ~25 candidate features**

**Feature Selection Strategy:**
1. Compute all candidates for all samples
2. Rank by correlation with tissue type (real vs. phantom)
3. Remove highly correlated pairs (keep only most interpretable)
4. Validate feature stability across different sampling rates
5. Final set: 8–12 features balancing predictiveness and interpretability

---

## Modeling Approach Selection

### Recommended Model Candidates

**For Classification/Ranking (Phase 3):**

1. **XGBoost or LightGBM**
   - **Why:** Excellent feature importance analysis; handles non-linear relationships; robust to small datasets
   - **Output:** Classification probabilities → convert to fidelity score
   - **Pros:** Fast training; interpretable; works well with hand-crafted features
   - **Cons:** May struggle with mixed sampling rates if not properly normalized

2. **Random Forest**
   - **Why:** Inherently produces confidence scores; resistant to overfitting
   - **Output:** Probability of "real tissue" → use as fidelity metric
   - **Pros:** Stable; handles feature interactions; good baseline
   - **Cons:** Less powerful than XGBoost for complex patterns

3. **Support Vector Machine (SVM)**
   - **Why:** Works well in high-dimensional feature spaces; robust margins
   - **Output:** Distance from decision boundary → convert to fidelity score
   - **Pros:** Theoretically grounded; good generalization
   - **Cons:** Less interpretable; slower on large datasets

4. **Deep Learning (LSTM or 1D-CNN)**
   - **Why:** Learns features directly from raw time-series
   - **Output:** Network activation → fidelity score
   - **Pros:** Potential for better feature discovery; handles variable-length sequences
   - **Cons:** Requires more training data; harder to interpret; needs careful handling of mixed sampling rates

**Recommended:** Start with XGBoost or Random Forest (well-understood, fast, interpretable). If data grows, revisit deep learning.

**For Optimization (Phase 5):**

1. **Gaussian Process Regression (GPR)**
   - **Best for:** Small datasets with uncertainty quantification
   - **Advantage:** Provides confidence bands on predictions
   - **Use case:** "Predict fidelity for formulation (12%, 1%, 5%) and confidence"

2. **Polynomial Regression**
   - **Best for:** Simple patterns; quick approximation
   - **Advantage:** Computationally cheap; interpretable terms
   - **Use case:** "Fidelity roughly quadratic in chitosan content?"

3. **Bayesian Optimization**
   - **Best for:** Finding global optimum efficiently
   - **Advantage:** Guides experimentation toward better formulations
   - **Use case:** "What formulation ratio should we test next?"

---

## Data Preprocessing Steps

### Before Feature Extraction:

1. **File Parsing** ✓ *Updated*
   - Load `.sum` files; determine exact data structure
   - Identify which columns are force, time, position, etc.
   - Handle dual sampling rates (10 Hz and 100 Hz)

2. **Temporal Alignment** ✓ *Updated*
   - Identify recording start/end (when is needle inserted? When removed?)
   - Segment by activity phase (insertion, steady-state liposuction, extraction)
   - Resample heterogeneous data: convert 100 Hz and 10 Hz to common rate (e.g., 50 Hz)
   - **Critical for comparison:** Ensure all signals are aligned to same temporal grid

3. **Normalization**
   - Handle absolute force scaling (different cannula diameters? Sensor calibration?)
   - Normalize by time duration (length-dependent metrics)
   - Standardize force units (kPa? Newtons? Normalized pressure?)
   - **Sampling-rate adjustment:** Scale derivative-based features by sampling frequency

4. **Outlier Handling**
   - Detect and flag anomalous recordings (equipment malfunction? Incomplete data?)
   - Cross-check Adipose_4 duplicates for data quality
   - Decide: remove, clip, or keep with warning flag?

5. **Missing Data**
   - Any gaps in time-series? Interpolation strategy?
   - Any incomplete files (truncated recordings)?
   - Handle edge cases from mixed sampling rates

**Deliverable:** Data preprocessing pipeline with validation checks and sampling-rate harmonization

---

## Validation & Performance Metrics

### Metrics for Classification (Phase 3)

**For Binary / Multi-class:**
- Accuracy, Precision, Recall, F1-score
- ROC-AUC (Receiver Operating Characteristic curve)
- Confusion matrix (which phantoms get misclassified as real? How often?)

**For Continuous Ranking:**
- Correlation between predicted and actual fidelity scores
- Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE)
- Ranking consistency (does model agree on Phantom_2 > Phantom_1 > Phantom_3?)

### Validation Strategy

**Cross-Validation:**
- Leave-one-sample-out (if data is small): test on Phantom_1, train on Adipose + Phantom_2 + Phantom_3
- k-fold cross-validation (if data permits): 5–10 folds
- Stratified by tissue type and sampling rate (ensure balanced train/test splits)

**Hold-Out Test Set:**
- Reserve 20–30% of data for final evaluation
- Stratified by tissue type, sampling rate, and condition

**Ablation Studies:**
- Remove one feature at a time; does performance drop?
- Test robustness to sampling rate differences
- This identifies which features actually matter vs. noise

### Metrics for Optimization (Phase 5)

- R² score (variance explained by GPR model)
- Leave-one-out cross-validated error
- Prediction intervals: is uncertainty reasonable?
- Validation of predicted optimal formulation (does it actually test better?)

---

## Implementation Roadmap

### Stage 1: Exploration & Validation (Weeks 1–2)
- [ ] Confirm all `.sum` files referenced in Metadata.md are accessible
- [ ] Understand binary format and parse files successfully
- [ ] Load and visualize raw force traces (real vs. phantom, by sampling rate)
- [ ] Document signal characteristics and qualitative differences
- [ ] Identify and handle mixed sampling rate data (100 Hz vs. 10 Hz)
- [ ] Acquire missing information (formulation ratios, exact sampling specifications)
- [ ] Verify data quality (especially Adipose_4 duplicates)

### Stage 2: Feature Engineering (Weeks 2–3)
- [ ] Implement feature extraction pipeline with sampling-rate normalization
- [ ] Compute all candidate features for all samples
- [ ] Analyze feature stability across different sampling rates
- [ ] Perform feature selection analysis
- [ ] Document final 8–12 features and their biological justification

### Stage 3: Model Training & Ranking (Weeks 3–4)
- [ ] Prepare labeled dataset (tissue type + features + sampling rate metadata)
- [ ] Train XGBoost / Random Forest classifier
- [ ] Convert predictions to continuous fidelity scores
- [ ] Rank phantoms by mimicry quality
- [ ] Generate feature importance plot
- [ ] Cross-validation and performance analysis
- [ ] Sensitivity analysis: model robustness to sampling rate variation

### Stage 4: Optimization (Weeks 4–5)
- [ ] Confirm formulation ratios for all phantoms
- [ ] Fit Gaussian Process or polynomial model
- [ ] Predict optimal formulation(s)
- [ ] Generate uncertainty estimates
- [ ] Plan validation experiments

### Stage 5: Documentation & Validation (Weeks 5–6)
- [ ] Write final methodology document with sampling-rate discussion
- [ ] Prepare results tables and figures
- [ ] Code all scripts with documentation
- [ ] Conduct hold-out test validation
- [ ] Recommendations for next formulation candidates
- [ ] Update Metadata.md with any additional collected data

---

## Key Decisions Required Before Implementation

| Decision | Options | Recommendation |
|----------|---------|-----------------|
| Scoring approach | Binary / Multi-class / Continuous ranking | Continuous ranking (Option C) |
| Condition handling | Average across / Match conditions / Hierarchical | Hierarchical with Adipose_3/5 multi-condition data |
| Sampling rate strategy | Resample all / Separate models / Rate-aware features | Resample to common rate (50 Hz) with validation |
| Feature strategy | Manual extraction / Deep learning | Manual extraction (XGBoost/RF compatible) |
| Model type | XGBoost / RF / SVM / Deep learning | XGBoost or Random Forest |
| Optimization model | GPR / Polynomial / Bayesian optimization | GPR (uncertainty quantification) |
| Validation method | Hold-out / k-fold / Leave-one-out | k-fold (5–10 folds) with hold-out test, stratified by rate |
| Data preprocessing | Resampling strategy | Resample 100 Hz and 10 Hz to common 50 Hz rate |

---

## Expected Outcomes

### Phase 3 Deliverables
- Ranked list of phantoms by fidelity score
- Feature importance analysis (which characteristics distinguish real from phantom?)
- Classification model accuracy and uncertainty bounds
- Sampling-rate impact analysis
- Interpretation: "Phantom_2 is 87% as realistic as human tissue; mainly differs in energy dissipation"

### Phase 5 Deliverables
- Predictive model: fidelity = f(gelatin%, chitosan%, glycerol%)
- Predicted optimal formulation ratios
- Confidence intervals on predictions
- Recommendations for next phantom candidates to test

---

## Repository Next Steps

1. **Update `/Code/` directory:**
   - Add Python scripts for each pipeline stage (exploration, feature extraction, modeling, optimization)
   - Include README with execution order and dependencies
   - Add data parsing utilities for `.sum` files

2. **Expand `/Documentation/`:**
   - Add detailed feature engineering document with sampling-rate considerations
   - Add model training methodology
   - Add results interpretation guide
   - Keep Action_Plan.md synchronized with progress

3. **Create `/Results and analysis/` content:**
   - Populate with fidelity rankings
   - Add visualizations (signal comparisons by sampling rate, feature importance plots, fidelity curves)

4. **Add `/Data_Processing/` (if needed):**
   - Scripts for `.sum` file parsing with sampling rate detection
   - Data validation and cleaning utilities
   - Preprocessing pipeline with resampling

5. **Maintain Metadata.md:**
   - Continue cataloging new tissue files
   - Document sampling rates and test conditions for each recording
   - Track data quality notes

---

## Questions to Resolve Immediately

1. **Are all `.sum` files referenced in Metadata.md in the repo?** If not, where are they stored?
2. **What's the exact file format?** (binary structure, byte order, sample format, metadata headers)
3. **Do we have formulation ratios** for Phantom_1, Phantom_2, Phantom_3?
4. **How many total recordings** do we have per tissue sample? (Verify against Metadata.md)
5. **Are there any baseline/control recordings** (e.g., needle without liposuction)?
6. **Data quality:** Are all files complete, or are some truncated/corrupted? (Especially Adipose_4 duplicates)
7. **Sampling rate verification:** Confirm exact sampling frequencies for all files listed in Metadata.md
8. **File organization:** Are data files in `/Clean _Data/` directory accessible? Structure and naming scheme?

---

## References & Tools

**Python Libraries:**
- Data handling: pandas, numpy
- Feature extraction: scipy (signal processing), scikit-learn
- Resampling: scipy.signal.resample, scipy.interpolate
- Modeling: scikit-learn (XGBoost, RandomForest), xgboost, lightgbm
- Optimization: scikit-learn (GaussianProcessRegressor)
- Visualization: matplotlib, seaborn, plotly

**Potential Advanced Methods:**
- Wavelet decomposition: pywt (PyWavelets)
- Approximate entropy: sampropy
- Deep learning: PyTorch, TensorFlow (if data grows)
- Sampling rate handling: librosa (audio/signal resampling utilities)

---

## Notes

- This plan assumes feature-based ML approach (vs. end-to-end deep learning). If dataset grows significantly (100+ samples), revisit deep learning.
- **Mixed sampling rates (10 Hz vs. 100 Hz) are a key preprocessing challenge.** Resampling to common rate (50 Hz) recommended to preserve information while enabling fair comparison.
- Phantom ranking is sensitive to feature choice and distance metric. Multiple validation approaches recommended.
- Optimization phase (Phase 5) assumes smooth relationship between formulation and fidelity. Non-linear or multi-modal surfaces may require adaptive sampling.
- **Adipose_3 and Adipose_5 provide comprehensive condition coverage** — prioritize these for ground truth definition and condition-matched comparisons.
