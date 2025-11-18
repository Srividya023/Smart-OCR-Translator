## Smart OCR Translator

### What it is

Smart OCR Translator is a Python project that takes **scanned PDFs or images in non-English languages** and converts them into an **English PDF while keeping the original layout** (roughly the same positions and structure).

---

### What it does

* Reads scanned PDFs or images (reports, forms, letters, etc.)
* Uses OCR to extract the text and its position on the page
* Detects the original language of the text
* Translates the text into English
* Writes the translated text back onto the page in the **same regions**
* Exports a new **translated PDF**

---

### Tech used

* **Python**
* **PyMuPDF (`fitz`)** – load and rasterize PDF pages
* **pytesseract + Tesseract OCR** – read text and bounding boxes
* **Pillow (PIL)** – draw white boxes and render translated text
* **Hugging Face Transformers**

  * `facebook/m2m100_418M` – multilingual translation model
  * `papluca/xlm-roberta-base-language-detection` – language detection
* **PyTorch** – backend for the translation model
* (Optional) **Google Colab** – for running the notebook in the cloud

---

### How it works (high level)

1. **Load pages**

   * If input is a PDF, each page is converted to an image.
   * If input is an image, it is loaded directly.

2. **OCR with positions**

   * Tesseract OCR extracts text and bounding boxes for each word.
   * Words are grouped into lines based on their y-coordinates.

3. **Detect language**

   * A sample of the text is passed to a language-detection model.
   * The detected language becomes the translation source language.

4. **Translate text**

   * Each line is translated to English using the M2M100 model.
   * Long lines are handled to avoid overflow in their regions.

5. **Write back with preserved layout**

   * Optionally cover original text with white rectangles.
   * Draw translated text into the same regions using Pillow.

6. **Export output**

   * All processed pages are combined into a new PDF:
     `Translated_EN_PreservedLayout.pdf`

---

### Real-time / practical use cases

* Translating **scanned official letters, contracts, or forms** into English without losing structure
* Helping **students and researchers** read non-English PDFs while keeping tables and figures aligned
* Supporting **teams working with international documents** (e.g., reports from different countries)
* Assisting **immigrants or travelers** to understand printed documents in a foreign language
