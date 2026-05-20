# Protocol 01: Data Curation & Labeling Criteria

The objective of this stage is to create a clean, robust training dataset. We will generate two organized folders: one containing the target species' calls and another containing representative noise, to feed the model.

## 1. Defining the "Gold Standard"
To ensure the model learns efficiently, we follow strict curation rules for every single selection.

* **Evident Signals Only:** Label acoustic events only if they are clearly audible and distinctly visible on the spectrogram.
* **The Golden Rule #1 (Precautionary Principle):** *"If you are not sure it is correct, consider it incorrect."* Labeling faint, highly masked, or ambiguous signals weakens the clear acoustic signature the model is attempting to learn.
* **The Golden Rule #2 (Noise Purity):** The `NOISE` folder (non-event class) must have an absolute absence of the target species' signal. Including even faint traces of the target species in this folder sends contradictory messages to the algorithm, leading to poor model performance.
* **Representativeness:** The training dataset must encompass spatial (inter-population) and temporal (varying weather conditions, seasons) variability to maximize the model's ability to generalize across different environments.

## 2. Linear Workflow: From Spectrogram to Dataset
Follow these steps sequentially to build your dataset:

### Step A: Selection and Labeling
1. Open your audio files in **Raven Pro**.
2. Identify and draw selection boxes around your target species' calls (ensure they are clear and evident).

> **Note on Selection Length:**
> * **Optimal Range:** Aim for selections between **1.5 and 3 seconds** whenever possible.
> * **Handling Shorter Selections (< 1.5s):** Try to avoid very short clips. Since the training pipeline defaults to 3-second windows, it will fill the remaining time with background noise (*padding*). If the signal is too short, the model may struggle to distinguish the target call from the background, potentially reducing performance.
> * **Handling Longer Selections (> 3s):** You can safely label events longer than 3 seconds. The training pipeline will automatically segment these into multiple 3-second chunks. **Crucial Rule:** When using long selections, ensure they do not contain long periods of silence or the presence of non-target species. The selected interval should be dominated by the target signal and should avoid long silent periods or prominent non-target sounds whenever possible.

3. Identify and draw selection boxes around environmental noise events (rain, wind, technical artifacts, other species' calls).
4. Save your Selection Table.

### Step B: Exporting Samples
1. Use your preferred tool (or the provided script) to extract these selections.
2. Export the annotated selections as individual `.wav` clips. BirdNET-Analyzer can handle variable-length segments when using `Crop Mode = Segments`.

### Step C: Folder Organization
Organize your clips into the following structure. This folder path is what you will provide to the BirdNET training module later:

```text
/training_data/
  ├── /Target_Species_Name/  <- Only clear, evident calls
  └── /NOISE/                <- Pure noise (no traces of target species)
```
## 3. Final Verification
Before moving to the next protocol, perform a "Visual Audit":

* **Open your `/Target_Species_Name/` folder:** Do all these clips clearly show the species' signal?
* **Open your `/NOISE/` folder:** Are you 100% sure none of these contain even a faint trace of the target species?

**If you answered YES to both, your dataset is ready for the training stage.**
