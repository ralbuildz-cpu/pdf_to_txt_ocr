# pdf_to_txt_ocr



I got tired of PDFs that either copy-paste fine or are just scanned images, and needing two different tools to deal with them. This script handles both in one go, and it pulls the images out too.

It runs in your terminal, works on Windows and Mac/Linux, and if you don't give it any arguments it just walks you through picking a file.

## What it does

- Checks a PDF for real text first. If it finds it, it extracts it directly
- If there's no text, it runs OCR on each page with Tesseract
- Pulls every embedded image out to an `images/` folder next to your output
- Writes everything to either Markdown or plain text
- In Markdown mode, it adds the images inline so you can read it right away
- Has a simple file browser that starts in Downloads, lets you arrow around and filter by typing
- Asks before overwriting files

## Install

You need Python 3.7+ and Tesseract OCR installed on your system.

Then install the Python packages:

```
pip install pytesseract pillow PyMuPDF
```

On Windows, install Tesseract from https://github.com/UB-Mannheim/tesseract/wiki and make sure `tesseract.exe` is on your PATH. On Mac: `brew install tesseract`. On Linux: `sudo apt install tesseract-ocr`.

## How to use

The easiest way is interactive:

```
python pdf_to_txt_ocr.py
```

It will:
1. Open a picker to choose a PDF
2. Ask for Markdown or TXT output
3. Suggest a default output name (same as the PDF)
4. Ask if you want to extract images

You can also run it directly:

```
python pdf_to_txt_ocr.py input.pdf output.md --format md
```

or

```
python pdf_to_txt_ocr.py scan.pdf notes.txt --format txt
```

If you pass an input file on the command line, it assumes you want images extracted.

## Output

- Text is saved with page breaks like `--- Page 1 ---`
- Images go to `images/` next to your output file, named `img_p1_1.png`, `img_p2_1.png`, etc.
- Markdown output links the images so you can open the .md file and see everything together
- Text output just lists the image paths at the bottom

## Controls in the picker

- Up/Down: move
- PageUp/PageDown: jump
- Enter: select
- Type letters: filter the list
- q: cancel
- ?: help

## Notes

- OCR defaults to English and 200 DPI. If you need other languages, edit the `lang='eng'` line in the script
- It is slow on big scanned PDFs, that's normal for OCR
- It skips password-protected PDFs unless you unlock them first
- The terminal UI uses raw input mode, so Ctrl-C exits cleanly

That's all it does. Pick a PDF, get text and images back.
