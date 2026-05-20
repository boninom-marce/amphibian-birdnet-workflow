# Protocol 03: Acoustic Analysis-Inference

This protocol explains how to apply the custom classifier (`.tflite`) developed in the previous step to process field recordings.
*Note on Versions: The BirdNET-Analyzer interface may show minor changes in button names depending on the version installed (e.g., V2.1 vs V2.4). If labels do not match exactly, look for the equivalent functions described below.*

## 🎯 Objective
To use the trained model to identify the target species in new acoustic data, transforming raw recordings into selection tables compatible with Raven Pro.

---

## 💻 Step 1: BirdNET-Analyzer Configuration
Open the **BirdNET-Analyzer GUI** and navigate to the **"Multiple Files"** tab.

* **Path Selection:**
    * **Input path:** Select the folder containing your field recordings.
    * **Output path:** Select the folder where results will be saved.
* **Loading the Custom Classifier:**
    * Go to the **"Model selection"** section.
    * Depending on your BirdNET-Analyzer version, look for the option associated with loading a “custom classifier” model.
    * Click the selection button (e.g., "Select classifier") and browse for the `.tflite` file generated in Protocol 02.
    * **Important:** Ensure the corresponding labels file (`_Labels.txt`) is in the same folder as the `.tflite` file so the system can load it automatically.

---

## ⚙️ Step 2: Inference Settings
To ensure data is suitable for subsequent scientific validation:

* **Result Type:** Select **"Raven selection table"**. This is essential for visualizing detections over the original audio in Raven Pro.
* **Combine Selection Tables:** Enable this option to consolidate results into a single table, simplifying post-processing.
* **Confidence Threshold:** We recommend an initial low value of **0.1**. 
    * *Reasoning:* It is preferable to capture false positives at this stage and filter them later (e.g., via logistic regression) than to lose real detections due to an overly strict threshold.
* **Threads:** Adjust the number of threads according to your CPU cores to speed up the process. 
* *Tip:* Set the number of threads to **(Total Cores - 1)**. This ensures that at least one core remains free for your operating system and other background tasks, preventing your PC from freezing during the analysis.
---

## 🚀 Step 3: Execution and Results
1. Click **"Analyze"**.
2. **Output:** BirdNET will generate one `.txt` file per analyzed audio. Each row represents an analysis window (~3 seconds) and includes the predicted species label and a confidence score between 0 and 1.

---

## 🔍 Step 4: Visualization and Audit in Raven Pro
Once the analysis is complete, it is recommended to perform a visual inspection to confirm that the model is detecting the expected signals.

1. **Open the original audio:** In Raven Pro, go to **File > Open Sound Files...** (or use `Ctrl + O`) and select the analyzed field recording.
2. **Load the detections:** With the audio window active, go to the menu **File > Open Selection Table...** (or use the shortcut `Ctrl + Shift + O`).
3. **Select the result file:** Locate the `.txt` file that BirdNET generated for that specific audio in your output folder.
4. **Visual Audit:** Raven will overlay the automatic detections onto the spectrogram as selection boxes.
    * Each box will be ~3 seconds long (BirdNET's analysis window).
    * Check if the boxes align with the visual and acoustic signals of your target species.
    * Observe the **Score** column in the selection table; this will give you an initial idea of how "confident" the model is in its predictions.

> **Efficiency Tip:** If you want a faster review, use the **"Selection Review"** function in Raven to automatically jump from one detection to the next.
