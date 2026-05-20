# Examples: Case Studies

This directory provides example datasets to test and validate custom classifiers. Each subdirectory contains key components of the workflow for a specific species.

## Dataset Structure
Each species folder contains:
- **`raw_audio.wav`**: A 10-minute acoustic sample.
- **`gold_standard_labels.csv`**: Expert annotations (the "Gold Standard").
- **`birdnet_output.txt`**: Raw output from BirdNET-Analyzer.
- **`evaluation_results.csv`**: Performance metrics derived from the comparison between the output and the gold standard.
- **`screenshots/`**: Visual references of the acoustic signals and detection windows.

## How to use
You can use these files to reproduce, inspect, and validate the workflow described in this repository. Load the corresponding custom classifier from the `classifiers/` directory and analyze the provided `raw_audio.wav` file using BirdNET-Analyzer.
