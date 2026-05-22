# Amphibian Monitoring: Open-Source Solutions and AI-Based Detection with Examples from Patagonia
This repository contains the technical framework, protocols, and custom classifiers developed during the project **"Open-Source Solutions for Amphibian Monitoring: Adapting Autonomous Recording Devices (ARDs) and AI-Based Detection in Patagonia"**, funded by **WILDLABS.net** and **Arm**.
## 🐸 Project Description

Passive Acoustic Monitoring (PAM) generates massive volumes of data. This project addresses the analytical bottleneck by consolidating an end-to-end, reproducible workflow for the automatic detection of acoustic signals using custom classifiers within the **BirdNET-Analyzer** framework.

While this repository uses Patagonian amphibians as a core baseline, the underlying methodology is globally applicable. It demonstrates how leveraging BirdNET's pre-computed acoustic embeddings allows researchers to train highly accurate non-avian classifiers with significantly less computational effort and smaller training datasets than building a neural network from scratch.

## 🛠️ Implemented Workflow Structure

The workflow is organized into three critical stages, built upon practical field experience with acoustic data:

* **Stage I (Data Curation and Labeling Criteria):** Focuses on defining a rigorous "Gold Standard". Signal quality categories may be used during manual curation, but training is performed using a binary presence/absence approach. A precautionary principle is applied: if a signal cannot be confidently identified by an experienced observer, it is excluded to avoid introducing ambiguity into the model's learning process.
* [Protocol 01: Labeling](protocols/01_labeling.md)

* **Stage II (Custom Model Training and Analysis):** A guide for binary training (presence/absence) using embeddings. Special emphasis is placed on creating a robust "Noise" class that captures the biotic and abiotic variability of the local soundscape (wind, rain, technical interference, other species) to drastically minimize false positives.
* [Protocol 02: Training](protocols/02_training.md)
* [Protocol 03: Analysis](protocols/03_analysis.md)

* **Stage III (Evaluation, Validation, and Troubleshooting):** A protocol to measure real-world performance. We address critical technical challenges, such as implementing relative time tracking (`File Offset`) in Raven Pro and generating manual duration columns to ensure temporal alignment between expert annotations and BirdNET's fixed analysis windows.
* [Protocol 04: Validation](protocols/04_validation.md)
* [Protocol 05: Common Problems](protocols/05_common_problems.md)


## 📂 Repository Structure

```text
repository/
│
├── README.md               # Overview, project mission, and links to protocols
├── CITATION.cff            # Academic citation metadata
├── LICENSE                 # Project open-source license
│
├── classifiers/                  # Custom BirdNET classifiers for six amphibian species
│   ├── Rhinoderma_darwinii/
│   ├── Batrachyla_leptopus/
│   ├── Batrachyla_taeniata/
│   ├── Batrachyla_antartandica/
│   ├── Hylorina_sylvatica/
│   └── Pleurodema_thaul/
│
├── protocols/              # Step-by-step workflow documentation
│   ├── 01_labeling.md
│   ├── 02_training.md
│   ├── 03_analysis.md
│   ├── 04_validation.md
│   └── 05_common_problems.md
│
├── examples/               # Reproducible case studies and validation datasets
│   ├── Rhinoderma_darwinii/
│   │   ├── *.wav
│   │   ├── gold_standard_labels.csv
│   │   ├── birdnet_output.txt
│   │   ├── results_evaluation_table.csv
│   │   ├── Evaluation_data_table.csv
│   │   └── screenshots/
│   │
│   ├── Batrachyla_leptopus/
│   ├── Batrachyla_taeniata/
│   ├── Batrachyla_antartandica/
│   ├── Hylorina_sylvatica/
│   ├── Pleurodema_thaul/
│   └── README.md                 # Instructions for reproducing the examples
│
├── scripts/                # Utility scripts for workflow automation
│   └── optional/           # Non-essential but helpful scripts (e.g., CSV formatting)
│
└── figures/                # Global figures (workflow diagrams, project logos)

```


## 🦎 Core Methodological Principles

To guarantee a robust and reliable machine learning model, the protocols in this repository enforce strict data curation rules:

* **Evident Signals Only:** Label acoustic events only if they are clearly audible and distinctly visible on the spectrogram.

* **The Golden Rule #1 (Precautionary Principle):** *"If you are not sure it is correct, consider it incorrect."* Labeling faint, highly masked, or ambiguous signals weakens the clear acoustic signature the model is attempting to learn.

* **The Golden Rule  #2 (Noise Purity):** *The NOISE folder (non-event class) must have an absolute absence of the target species' signal. Including even faint traces of the target species in this folder sends contradictory messages to the algorithm.

* **Representativeness:** The training dataset must encompass spatial (inter-population) and temporal (varying weather conditions, seasons) variability to maximize the model's ability to generalize across different environments.

---

## 🏛️ Collaborating Institutions

* **INIBIOMA** (Instituto de Investigaciones en Biodiversidad y Medioambiente, CONICET-UNCo, Argentina)

* **CITECCA** (Centro Interdisciplinario de Telecomunicaciones, Electrónica, Computación y Ciencia Aplicada, UNRN, Argentina)

* **APN** (Administración de Parques Nacionales, Argentina)

