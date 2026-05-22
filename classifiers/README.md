# Custom Classifiers

This directory contains trained `.tflite` models used for automated detection of specific amphibian species.

## Structure
Each subfolder corresponds to a unique species and contains the necessary files for BirdNET-Analyzer:
- `[ModelName].tflite`: The trained neural network model.
- `[ModelName]_Labels.txt`: The corresponding label mapping.

## How to use these models
1. **Download:** Clone this repository or download the specific subfolder containing the model you need.
2. **Setup:** Ensure both the `.tflite` file and the `_Labels.txt` file are located in the same directory.
3. **BirdNET-Analyzer:** - Open the BirdNET-Analyzer GUI.
  - Navigate to the **"Custom classifier"** section.
  - Select the folder containing your desired model and label files.
  - Adjust the **"Confidence threshold"**. See Analysis and Validation sections in protocols (refer to our [Analysis Protocol](../protocols/03_analysis.md) [Validation Protocol](../protocols/04_validation.md)).

## Disclaimer
These models are tailored to specific acoustic environments. Performance may vary when applied to recording sites with significantly different ambient noise or biotic composition. Please consult the `examples/` directory to see performance benchmarks for these models.
