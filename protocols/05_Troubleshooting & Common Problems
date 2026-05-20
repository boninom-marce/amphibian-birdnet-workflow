# Protocol 05: Troubleshooting & Common Problems

This document addresses the most frequent technical hurdles encountered when using the BirdNET-Raven workflow, providing specific solutions to ensure data integrity and reliable results.

---

## 🕒 1. Temporal Alignment Errors (The #1 Problem)
* **Symptom:** Run the Evaluation tool and you obtain unrealistically poor evaluation metrics, or thousands of false positives, even though your manual labels and BirdNET detections look correct on the spectrogram.
* **Cause:** **Absolute vs. Relative Time.** Raven Pro often exports time relative to the beginning of a recording session (absolute time), while BirdNET’s Evaluation tool requires time relative to the beginning of each individual file.
* **Solution:**
    * Always use the `File Offset (s)` column as your "Start Time".
    * Ensure you have a manual `Duration` column in your Gold Standard table (e.g., "60" for 1-minute files). Without this, BirdNET cannot align its 3-second processing windows with your expert labels.

## 📊 2. Raven Overwriting Data
* **Symptom:** You carefully calculated the "corrected end time" in Excel, but when you open the file again in Raven, the values have changed.
* **Cause:** **Reserved Column Names.** If you name your calculated end time column exactly `End Time`, Raven Pro will automatically overwrite it with its own absolute time calculations.
* **Solution:** Use a non-standard name like `Corrected_End_Time` or `Rel_End_Time`. BirdNET allows you to map these custom names in the "Column Mapping" section of the Evaluation tab.

## 🦎 3. Poor Model Performance (Low Recall)
* **Symptom:** Your custom classifier misses very obvious calls that a human can easily see and hear.
* **Cause #1 (Noise Pollution):** You included faint traces of your target species in the `NOISE` folder. This teaches the model that those acoustic features are "noise" and should be ignored.
    * *Solution:* Audit your `NOISE` folder; it must be 100% free of target signals.
* **Cause #2 (Training Ambiguity):** You labeled "doubtful" or very distant signals.
    * *Solution:* Follow the Precautionary Principle: only label signals that are clearly audible and visible on the spectrogram.

## ⚙️ 4. Concept Confusion: Score vs. Probability
* **Symptom:** A user assumes a "Confidence Score" of 0.70 means there is a 70% probability the species is present.
* **Correction:** BirdNET scores are not raw probabilities. A score of 0.70 for an easy-to-detect species might be very reliable, while for a difficult species, it might be mostly noise.
* **Solution:** Always perform the Evaluation stage (Protocol 04) to generate the precision-recall and score-threshold relationships. Use these evaluation outputs to select the threshold that provides the desired balance of Precision and Recall for your specific monitoring site.

## 💻 5. Software & Performance Issues
* **GUI Mismatches:** Labels like custom classifier loading options may change slightly between BirdNET-Analyzer versions. If labels don't match, look for the functional equivalent.
* **Memory Errors:** If Raven Pro becomes slow or crashes with large datasets, use "Paged Sound Windows" to load only small portions of audio into RAM at a time.
* **Clipped Audio:** If your input recordings are "clipped" (amplitude too high), BirdNET will struggle to identify the signal due to spurious harmonics. Check your raw audio files before starting the curation process.

---

## 🚀 Pro-Tip: Best Workflow Practices
To avoid technical pitfalls, always prioritize data quality over quantity:
1. **Apply the "Visual Audit" Rule:** Review your curated folders (as detailed in Protocol 01) before every training session.
2. **Conduct a Pilot Study:** Always perform a "small-scale test" using a **small pilot subset of files**. Run the full pipeline—from training to evaluation—with these few files to ensure your metadata, file paths, and column mappings are perfectly aligned before processing your entire dataset.
