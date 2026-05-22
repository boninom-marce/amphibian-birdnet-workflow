# Protocol 02: Custom Model Training

This protocol describes how to use the **BirdNET-Analyzer GUI** to train a custom classifier for a specific acoustic signal (target-species). The process is based on **Transfer Learning**, which leverages BirdNET's pre-existing acoustic knowledge to recognize new sounds with minimal computational effort.

## 🎯 Objective
To generate a custom model file (`.tflite`) capable of identifying your target species using the expert labels and curated data prepared in **Protocol 01**.

---

## 💻 Step 1: Input and Output Configuration
Open the **BirdNET-Analyzer GUI** and navigate to the **"Train"** tab.

* **Training Data:** Select the root folder organized in Protocol 01 (e.g., `/training_data/`). This folder must contain your subfolders for the `target-species` and the `NOISE` class.
* **Classifier Output:** Choose your destination folder and assign a name to your model (e.g., `TargetSpecies_Detector_V1`). BirdNET will generate the classifier as a `.tflite` model file.
* **Model Save Mode:** Select **"Replace"**. This creates a detector dedicated exclusively to your target species, replacing the default BirdNET global list for maximum efficiency in your project.

---

## ✂️ Step 2: Selection of "Crop Mode"
BirdNET internally operates on ~3-second analysis windows. When training with variable-length clips, you must define how the software handles segment extraction:

* **Center:** Extracts only the 3-second center of the clip.
* **First:** Extracts only the first 3 seconds.
* **Smart:** Analyzes the signal to find the 3-second segment with the highest energy or amplitude peaks.
* **Segments (Recommended for long labels):** Splits the audio file into multiple 3-second segments. If you labeled a 10-second call in the previous step, this mode generates several 3-second training examples from that single label, effectively increasing your dataset size. However, excessive overlap or very long labels may introduce highly redundant training samples.

---

## ⚙️ Step 3: Hyperparameters (Conservative Strategy)
For an initial, reliable model, we recommend a conservative approach using the software's default values. Do not modify advanced parameters (e.g., *Autotune*, *Focal Loss*, or *Upsampling*) unless you have prior experience, as the standard values are optimized for most use cases.

* **Epochs:** The number of times the model iterates over the entire dataset. BirdNET uses **"Early Stopping"**, meaning training will automatically halt when accuracy stops improving, preventing overfitting.
* **Batch Size:** The number of samples processed simultaneously. The default value is optimal for most hardware configurations.
* **Learning Rate:** Controls how quickly the model updates its knowledge. Keep the default setting to ensure stable convergence.

---

## 🚀 Step 4: Execution and Final Files
1. Click **"Start Training"**.
2. **Monitoring:** Once finished, BirdNET will display a Training History Plot. A successful execution generally shows stable convergence of the training metrics over time..
3. **Generated Files:** Your output folder will now contain three essential files that must always be kept together:
   * `TargetSpecies_Model.tflite`: The classifier "brain".
   * `TargetSpecies_Model_Labels.txt`: The list of species labels linked to the model.
   * `TargetSpecies_Model_Params.csv`: The configuration log (crucial for scientific reproducibility).

> **User Note:** This model is now ready to be applied to new field recordings or to proceed to **Protocol 03: Analysis**, where we will apply the detector to your data.
