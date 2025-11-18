Okay, here’s a clean block you can copy into your README 👇

```markdown
## Smart OCR Translator

### What it is  
Smart OCR Translator is a Python tool that takes **scanned PDFs or images in non-English languages** and converts them into an **English PDF while preserving the original layout** (positions of text, paragraphs, and structure).

---

### What it does  
- Reads a scanned document (PDF/image) in languages like French, Spanish, German, Italian, Portuguese, etc.  
- Runs OCR to extract text + word positions from each page.  
- Automatically detects the source language of the text.  
- Translates the content to English using a neural machine translation model.  
- Draws the translated text back onto the pages, keeping the layout as close as possible to the original.  
- Saves the final result as a new **translated PDF**.

---

### Tech stack / Libraries used  
- **Python**
- **PyMuPDF (`fitz`)** – to load and rasterize PDF pages  
- **pytesseract + Tesseract OCR** – to extract text and bounding boxes from images  
- **Pillow (PIL)** – to draw white boxes and render translated text back on the page  
- **Hugging Face Transformers**  
  - `facebook/m2m100_418M` – multilingual translation model  
  - `papluca/xlm-roberta-base-language-detection` – language detection pipeline  
- **Torch (PyTorch)** – to run the translation model  
- (Optional) **Google Colab** – for running the notebook in the cloud

---

### How it works (high level)  
1. **Load pages**  
   - If input is a PDF, each page is converted to an image using PyMuPDF.  
   - If input is a single image, it is loaded directly.

2. **OCR with bounding boxes**  
   - Tesseract OCR reads the page and returns text with coordinates for each word.  
   - Words are grouped into **lines** based on their vertical positions.

3. **Language detection**  
   - A small sample of the extracted text is passed to a language-detection model.  
   - If the detected language is supported (fr/es/de/it/pt/etc.), it is used as the source language for translation.

4. **Translation**  
   - Each line of text is translated from the source language to English using the M2M100 transformer model.  
   - Long lines are truncated or wrapped to avoid overflow.

5. **Layout-preserving rendering**  
   - For each line, the original text area is optionally covered with a white rectangle.  
   - The translated English text is drawn at the same (x, y, width, height) region using Pillow.  
   - This keeps the document structure visually similar to the original.

6. **Export**  
   - All processed page images are combined into a single PDF file  
   - Output file: `Translated_EN_PreservedLayout.pdf`

---

### Real-time / Practical use cases  
- Translating **scanned reports, forms, or contracts** from European languages to English without losing formatting.  
- Helping **students and researchers** read non-English academic papers while keeping tables, figures, and layout.  
- Supporting **multilingual teams** who receive documents in different languages but prefer an English version.  
- Assisting **immigrants and travelers** in understanding official letters, notices, or printed forms from foreign countries.  

This project shows how OCR, language detection, and neural translation can be combined to build a **layout-aware document translator**.
```
