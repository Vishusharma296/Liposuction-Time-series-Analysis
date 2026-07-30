# Formal Academic Problem Statement

## 1. Context and Problem Domain

The development of advanced medical devices and training methodologies for water-jet assisted liposuction (WAL) is heavily restricted by the limited availability and ethical boundaries governing the use of genuine human subcutaneous adipose tissue. Synthetic hydrogel phantoms offer a viable surrogate for this constrained tissue supply; however, conventional material characterization protocols applied to such phantoms remain financially prohibitive and lack clinical simulation validity.

Present material validation strategies are further bottlenecked by manual, unstandardized surgical execution: multi-axial user movement introduces severe kinematic noise into the collected sensor streams, effectively masking the true physical properties of the underlying tissue matrices. This masking effect constitutes the central obstacle that the present research confronts, since any data-driven claim about phantom fidelity is only as credible as the signal from which it is derived.

---

## 2. The Core Gap

Bridging this gap requires a data-driven sensory methodology capable of automatically quantifying phantom fidelity against real tissue. Two primary challenges persist in pursuit of this methodology:

1. **Manual operational variability:** Standard data acquisition workflows fail to decouple variable manual operational velocities from pure material resistance profiles, such that the force signal conflates operator behavior with material response rather than isolating the latter.

2. **Non-linear formulation complexity:** High-dimensional biopolymer formulation spaces—comprising gelatin, chitosan, and glycerol—exhibit highly non-linear mechanical property responses, rendering manual trial-and-error optimization of these formulations highly inefficient.

Both challenges directly motivate the core research goal of this thesis: **to replace uncontrolled, manually mediated tissue characterization with a standardized, quantifiable, and computationally optimized pipeline for validating and synthesizing high-fidelity artificial fat surrogates.**

---

## 3. Statement of Research Intent and Scope

This master's thesis resolves the challenges identified above by executing a three-fold data-based optimization architecture.

### Objective 1: System Standardization and Kinematic Validation

Objective 1 eliminates manual operational variability through the design and manufacture of a modular, one-degree-of-freedom (1-DOF) mechanical clamping test bench.

A machine learning framework is deployed to classify handling variances between unrestricted freehand execution and bench-stabilized insertion, thereby mathematically validating the system's capacity to isolate true tissue resistance from operator interference.

This objective directly addresses the first core-gap challenge by establishing a classifiable, quantified boundary between freehand and bench-stabilized operation. It converts an unverified assumption of kinematic noise reduction into an evidenced, data-supported claim—the foundation upon which any subsequent fidelity measurement in this thesis depends.

### Objective 2: Haptic Fidelity Characterization via High-Frequency Classification

Objective 2 employs a sensor-enhanced cannula operating at **100 Hz** to capture raw axial force-time profiles across real human fat and synthesized multi-component phantoms.

Time-series machine learning models—**XGBoost** and **Random Forest**—are developed to establish a proximity ranking metric, converting standard classification probabilities into a mathematical index of haptic mimicry.

This objective operationalizes the core research goal by transforming the qualitative notion of *phantom fidelity* into a quantifiable, model-derived metric, generated only after the kinematic noise problem has been resolved by Objective 1.

### Objective 3: Closed-Loop Multi-Component Synthesis Optimization

Objective 3 bypasses inefficient manual laboratory iteration through the implementation of a **Gaussian Process Regression (GPR)** surrogate optimization model.

This algorithm maps the non-linear formulation boundaries of gelatin, chitosan, and glycerol ratios directly to a distance-metric loss function against human tissue, computing the globally optimal biopolymer composition required to yield a high-fidelity artificial fat surrogate.

This objective closes the loop of the thesis's data-based architecture. The haptic mimicry index established in Objective 2 becomes the optimization target that Objective 3 minimizes, directly fulfilling the core research goal of replacing manual trial-and-error formulation with a computationally optimal, data-derived synthesis outcome.
