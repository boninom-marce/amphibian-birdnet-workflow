# Examples: Case Studies

This directory provides example datasets to test and validate custom classifiers. Each subdirectory contains key components of the workflow for a specific species.

## Dataset Structure
Each species folder contains:
- **`*.wav`**: A set of 10 acoustic samples (~1 minute each) containing representative target vocalizations.
- **`gold_standard_labels.csv`**: Expert annotations (the "Gold Standard").
- **`birdnet_output.txt`**: Raw output from BirdNET-Analyzer.
- **`evaluation_results.csv`**: Performance metrics derived from the comparison between the output and the gold standard.
- **`screenshots/`**: Visual references of the acoustic signals and detection windows.

## How to use
You can use these files to reproduce, inspect, and validate the workflow described in this repository. Load the corresponding custom classifier from the `classifiers/` directory and analyze the provided `.wav` files using BirdNET-Analyzer.
