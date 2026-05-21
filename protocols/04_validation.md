# Protocol 04: Evaluation & Performance Validation

This protocol outlines the procedure for validating your custom model's performance against a "Gold Standard"—a dataset of expert-verified annotations that the model has never encountered before.

## 🎯 Objective
To quantify your model’s reliability by calculating standard metrics (**Precision, Recall, and F1-Score**) and determining an operational confidence threshold for field applications.

---

## 💻 Step 1: Selecting the Independent Test Set
Performance validation is only valid if performed on data distinct from the training set.

* **Representativeness:** Select recordings that span different monitoring sites, times of day, and environmental conditions (e.g., wind/rain variability).
* **Independence:** Never use files from your training set for evaluation; this leads to biased, artificially high accuracy metrics.
* **Gold Standard Curation:** Expert-labeled signals must strictly follow the "Gold Standard" rules (evident signals only, as defined in Protocol 01).

---

## 🛠️ Step 2: Temporal Normalization (The Consistency Principle)

BirdNET evaluation relies on calculating the temporal overlap between your expert annotations and the model's predictions. Expert labels can be of any length (e.g., 0.5s or 5s); the critical requirement is that both datasets share the exact same temporal reference system.

**The Golden Rule of Bilateral Consistency:**
If the time references in your **Gold Standard** do not match the structure of the **BirdNET Output**, the evaluation tool may generate incorrect overlap calculations and misleading False Positives/Negatives.

1. **Alignment:** Ensure both tables use compatible relative time references (typically `File Offset (s)`, time relative to the start of each file) instead of absolute time.
2. **Symmetry:** If you create a `Corrected_End_Time` for your Gold Standard, you must create an identical column in your BirdNET Output file using the same logic.

---

## 📊 Step 3: Preparing the Datasets

You must format both your Raven table (*Gold Standard*) and your analysis results (*BirdNET Output*) to be temporally comparable (using Excel, R, etc.):

1. **Required Columns:** Ensure both files include:
   * `Begin File`: Filename of the `.wav`.
   * `File Offset (s)`: Start time relative to the file start.
   * `Delta Time (s)`: Duration of the selection.
   * `Duration` (File Duration): Total duration of the audio file. **Important Note:** Raven Pro does *not* export this automatically. You must manually create this column and populate it with the total duration of your files (e.g., if your recordings are 60 seconds long, enter "60" for every row).

2. **Calculate End Time:** If temporal inconsistencies are detected, create a custom end-time column (e.g., `Corrected_End_Time`) in both files using the same calculation logic.
   * **Formula:** `Corrected_End_Time = [File Offset (s)] + [Delta Time (s)]`

3. **Naming Caution:** Never name this column `End Time`. Raven Pro reserves this label for absolute time; if you reopen the table in Raven, it will overwrite your calculated values with the absolute time.

| Begin File   | File Offset (s) | Delta Time (s) | Corrected_End_Time | Duration |
| :----------- | :-------------- | :------------- | :----------------- | :------- |
| Audio_01.wav | 0.0694          | 2.8796         | 2.949              | 60       |
| Audio_02.wav | 5.1178          | 14.7841        | 19.901             | 60       |

---

## ⚙️ Step 4: BirdNET-Analyzer Configuration (Evaluation Tab)

Navigate to the **"Evaluation"** tab in the BirdNET-Analyzer GUI:

* **Annotations:** Load your aligned "Gold Standard" table.
* **Predictions:** Load your aligned "BirdNET Output" file.
* **Column Mapping:** 
  * Start Time -> `File Offset (s)`
  * End Time -> `Corrected_End_Time`
  * Recording -> `Begin File`
  * Duration -> `Duration` (Ensure this column is present in your CSV; if your files are 60s, populate the entire column with "60").
* **Minimum Overlap:** Use a permissive overlap criterion (e.g., 0.0–0.1). Because BirdNET operates with fixed analysis windows (~3 s) while many biological signals are substantially shorter, strict overlap requirements may artificially inflate false negatives.
---

## 📈 Step 5: Metrics and Interpretation
Click **"Calculate Metrics"**. BirdNET will compare segments and provide:

* **Precision:** How many of the detections made by the model were actually correct?
* **Recall:** How many of the actual calls present in the audio did the model successfully find?
* **F1-Score:** The harmonic mean of Precision and Recall.
* **Score-Threshold Analysis:** BirdNET provides a curve showing how model performance changes with different confidence scores. 

> **Note:** You can manually determine an appropriate **Confidence Threshold** (e.g., 0.8) by analyzing the precision-recall and score-threshold relationships, depending on whether the application prioritizes sensitivity or minimizing false positives.

