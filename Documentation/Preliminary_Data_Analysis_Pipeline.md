
### Modular Flowchart 1: Preprocessing & Signal Reconstruction

This stage focuses on handling the physical signal conditioning, correcting non-uniform sampling, repairing structured gaps, and stripping environmental offsets.

```mermaid
graph TD
    A[Raw Multi-Sample CSV Files] --> B[Sort by Time & Uniform Resampling <br/> Target Frequency: 10 Hz]
    B --> C{Missing Gaps Detected?}
    
    C -->|Yes: e.g., 15_21_28_091| D[Iterative Singular Spectrum Analysis <br/> SSA Gap Reconstruction]
    C -->|No| E[Continuous Timeline Consolidation <br/> e.g., Dr6 Stitching]
    
    D --> E
    E --> F[Adaptive Outlier & Spike Filter <br/> MAD-Based Filtering]
    F --> G[1st-Order High-Pass Butterworth Filter <br/> Cutoff: 0.1 Hz, Order: 1]
    G --> H[Isolate Dynamic Force AC Component <br/> Eliminating Vacuum & Water DC Offsets]
    
    style A fill:#ffccd5,stroke:#333,stroke-width:2px
    style D fill:#daf0ff,stroke:#333,stroke-width:2px
    style H fill:#d8f3dc,stroke:#333,stroke-width:2px
```


### Modular Flowchart 2: Multi-Domain Sliding-Window Feature Extraction

This stage segments the continuous filtered timeline into overlapping windows to capture localized tissue interaction patterns across four diverse mathematical domains.

```mermaid
graph TD
    A[Isolated Dynamic AC Force] --> B[Sliding Window Partitioning <br/> 5-Second Windows, 50% Overlap]
    
    B --> C1[Domain 1: Core Statistics & Energy]
    C1 --> C1a[Standard Deviation, Peak Force, <br/> Loading Rate, Energy, Mean Force]
    
    B --> C2[Domain 2: Spectral & Complexity]
    C2 --> C2a[Spectral Centroid, Spectral Entropy, <br/> High/Low Power Ratio, Sample & Fuzzy Entropy]
    
    B --> C3[Domain 3: Stroke Kinematics]
    C3 --> C3a[Stroke Cycle Count, Average Period, <br/> Period CV, Derivative Variance / Roughness]
    
    B --> C4[Domain 4: Physics-Informed Metrics]
    C4 --> C4a[Skewness, Kurtosis, <br/> Permutation Entropy]
    
    C1a & C2a & C3a & C4a --> D[Fused Integrated Feature Matrix <br/> Shape: 1768 x 22]
    
    style A fill:#d8f3dc,stroke:#333,stroke-width:2px
    style D fill:#daf0ff,stroke:#333,stroke-width:2px
```


### Modular Flowchart 3: Rigorous Validation & Benchmarking Architecture

This stage maps out the rigorous LODO validation, machine state confounding controls, statistical significance profiling, and phantom authenticity ranking.

```mermaid
graph TD
    A[Fused Integrated Feature Matrix] --> B1[Grouped Leave-One-Subject-Out <br/> LOSO Cross-Validation]
    A --> B2[Empirical Sample Distributions]
    A --> B3[Confounding Control Model]
    
    B1 --> C1[Optimal 9-Feature Tabular Subset <br/> via Sequential Ablation Study]
    C1 --> C2a[Primary Model: Random Forest]
    C1 --> C2b[Secondary Model: XGBoost]
    C1 --> C2c[Exploratory Sequence Models: <br/> LSTM & 1D-CNN / XceptionTime]
    
    C2a & C2b & C2c --> D1["Validation Metrics <br/> Accuracy: 87.83% - 95% CI: 80.41% - 95.25% <br/> Permutation Test p-value: 0.0100"]
    
    B3 --> D2[Metadata-Only Model <br/> Score: 62.96%]
    
    D1 & D2 --> E1{Model is Bias-Free? <br/> Tissue Mechanics > Metadata}
    E1 -->|Yes| E2[Authentic Tissue Classification <br/> Confirmation]
    
    B2 --> F1[Distance Space Comparison <br/> Multivariate MMD & Wasserstein Distances]
    F1 --> F2[Phantom Fidelity Benchmarking <br/> Best Mimic Rank: V7, V5, V1]
    
    style A fill:#daf0ff,stroke:#333,stroke-width:2px
    style D1 fill:#d8f3dc,stroke:#333,stroke-width:2px
    style D2 fill:#fde2e4,stroke:#333,stroke-width:2px
    style E2 fill:#b5e2fa,stroke:#333,stroke-width:2px
    style F2 fill:#ffdf00,stroke:#333,stroke-width:2px
```