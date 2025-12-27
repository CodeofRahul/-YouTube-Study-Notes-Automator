# 🎓 YouTube Study Notes Automator 📚

An automated pipeline for Google Colab that converts YouTube lectures into clean, scannable PDF notes. It uses computer vision to detect slide changes and provides a manual cleanup interface to ensure your final notes are perfect.

---

## 🌟 Key Features

-   **Smart Slide Detection:** Uses Histogram comparison to detect when a teacher changes a slide, ignoring small movements like hand gestures or flickering.
-   **Blank Page Filtering:** Automatically skips solid-colored, "empty," or blurry frames using Laplacian variance detection.
-   **Hindi & Special Character Support:** Robust filename sanitization to handle various languages and emojis in YouTube titles.
-   **Interactive PDF Manager:** A secondary visual tool to "Keep" or "Remove" pages from the generated PDF to eliminate any remaining duplicates.
-   **Optimized for Colab:** Downloads in 480p for high-speed processing without sacrificing text readability.

---

## 🛠️ Usage Workflow

### 1. Preparation
* Open [Google Colab](https://colab.research.google.com/).
* Create a new Notebook.
* The scripts will automatically install necessary dependencies: `yt-dlp`, `opencv-python`, `fpdf`, and `pdf2image`.

### 2. Phase 1: The Extractor (Auto-Generation)
Run the **Extractor Cell** and paste your YouTube link.
-   **What happens:** The script downloads the video, scans for unique frames every 5 seconds, and compiles them into a "Raw" PDF.
-   **Output:** Saved in the `Final_PDF_Notes` folder in your Colab sidebar.



### 3. Phase 2: The Manager (Manual Cleanup)
If your PDF has too many pages or unwanted duplicates, run the **Manager Cell**.
-   **Upload:** Select the PDF generated in Phase 1.
-   **Review:** A gallery of pages will appear with **KEEP (Green)** and **REMOVE (Red)** buttons.
-   **Download:** Click **"DOWNLOAD CLEANED PDF"** to get your final, high-quality study guide.



---

## ⚙️ Configuration & Tuning

You can modify these variables at the top of the script to suit different types of lectures:

| Variable | Default | Description |
| :--- | :--- | :--- |
| `CHECK_EVERY_X_SECONDS` | `5` | Frequency of checks. Increase for slow-paced lectures. |
| `SIMILARITY_THRESHOLD` | `0.92` | Similarity limit. Lower it (e.g., `0.85`) to reduce more duplicates. |
| `BLANK_THRESHOLD` | `5.0` | Sensitivity for empty pages. Higher = more aggressive skipping. |
| `DOWNLOAD_RES` | `480` | Video resolution. 480p is the sweet spot for speed and clarity. |

---

## 📂 Project Structure

```text
/content/
├── Final_PDF_Notes/      # Generated PDFs are stored here
├── Captured_Resources/   # Temporary storage for frames (Auto-cleaned)
└── Cleaned_Notes_...pdf  # The final output from the Manager

---

# ⚠️ Troubleshooting

- Buttons not clicking? If the Keep/Remove buttons don't change color, click Runtime > Restart Session in Colab and run the cell again.

- Session Crashed? Large PDFs (200+ pages) use significant RAM. If it crashes, try processing the video in smaller chunks or lower the DPI setting in the script.

- Filenames: If a video title is completely non-English, the script will default the filename to Study_Notes.pdf to prevent system errors.


Created for efficient learning. Happy Studying!
