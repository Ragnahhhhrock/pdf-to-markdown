# PDF → Markdown Converter

Turn PDFs into clean Markdown — headings, tables, lists, images, and OCR for scanned pages. Everything runs **100% in your browser**: files are never uploaded to any server.

## Features

- **Text & structure** — extracts text in correct reading order; detects headings (H1–H4) from font sizes, plus bold/italic runs, bullet lists, and numbered lists
- **Tables** — geometry-based table detection, rendered as Markdown tables
- **Images** — extracts embedded images and inlines them as data URIs (deduplicated, downscaled, capped)
- **Scanned PDFs (OCR)** — pages without a text layer are recognized with Tesseract OCR; supports English, Simplified Chinese, or both
- **Output** — rendered preview and raw Markdown tabs, copy to clipboard, one-click `.md` download
- **Options** — toggle table detection, image extraction, OCR, page separators, and OCR language

## Tech stack

- React + TypeScript + Vite
- Tailwind CSS + shadcn/ui
- [PDF.js](https://mozilla.github.io/pdf.js/) (`pdfjs-dist`) for PDF parsing
- [Tesseract.js](https://tesseract.projectnaptha.com/) for OCR
- [marked](https://marked.js.org/) for Markdown preview

## Getting started

```bash
npm install
npm run dev      # start dev server
npm run build    # production build -> dist/
```

## How it works

1. PDF.js parses each page's text content (with font, size, and position metadata), embedded images, and drawing operators.
2. Text items are clustered into lines; font-size analysis identifies the body size and heading levels.
3. Consecutive multi-column lines that share aligned x-positions are grouped into tables.
4. Pages with fewer than ~30 extractable characters are treated as scanned: the page is rendered to a canvas at 2× scale and recognized with Tesseract OCR.
5. Everything is assembled into Markdown with optional `---` page separators.

## License

MIT

Another [Mal Gordon](https://malgordon.com/) creation
