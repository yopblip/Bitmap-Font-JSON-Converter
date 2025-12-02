# Bitmap Font (XML / FNT) → JSON Converter

A lightweight browser-based tool for converting **Bitmap Font** files (`.xml` or text `.fnt`) into a clean and structured **JSON format**.

This tool supports both **XML-based** and **ASCII text-based** bitmap fonts and outputs a normalized JSON structure suitable for custom engines, renderers, or asset pipelines.

---

## 🚀 Live Demo

Try it online:

👉 **https://yopblip.github.io/Bitmap-Font-JSON-Converter/**

---

## ✨ Features

- Convert **XML** Bitmap Font files
- Convert **ASCII `.fnt`** Bitmap Font files
- Paste raw XML / `.fnt` text — no file upload required
- Instant JSON preview
- One-click JSON download
- Fully client-side (no backend required)

---

## 🚫 Unsupported Formats

**Binary Bitmap Font (`.fnt` / BMF) is not supported.**

This tool cannot parse **binary `.fnt` files**, because they use a block-based binary structure instead of text. Only the following formats are supported:

- ✔ XML bitmap fonts  
- ✔ ASCII / text bitmap fonts  
- ✘ Binary `.fnt` (BMF)

Attempting to load a binary `.fnt` file will fail.

---

## 📥 Usage

### 1. Upload a file

1. Choose a `.xml`, `.fnt`, or `.txt` file.
2. Click **“Convert uploaded file → Download JSON”**.
3. The JSON will appear in the preview box and download automatically.

### 2. Or paste the content manually

1. Paste the XML or ASCII `.fnt` text into the textarea.
2. Click **“Convert pasted text → Download JSON”**.
3. The JSON will appear in the preview box and download automatically.

---

## 🧩 JSON Output Structure

The converter normalizes all supported formats into a unified JSON structure:

```json
{
  "info": [
    {
      "face": "Font Name",
      "size": 32
    }
  ],
  "common": [
    {
      "lineHeight": 36,
      "base": 28,
      "scaleW": 512,
      "scaleH": 512,
      "pages": 1
    }
  ],
  "pages": [
    {
      "page": {
        "id": 0,
        "file": "font.png"
      }
    }
  ],
  "chars": {
    "count": "89",
    "char": [
      {
        "id": 65,
        "x": 10,
        "y": 20,
        "width": 34,
        "height": 40,
        "xoffset": 1,
        "yoffset": 2,
        "xadvance": 36,
        "page": 0,
        "chnl": 15
      }
    ]
  },
  "kernings": {
    "count": "12",
    "kerning": [
      {
        "first": 65,
        "second": 86,
        "amount": -1
      }
    ]
  }
}
````

### 🔸 Numeric Fields

* Metric-like fields (`x`, `y`, `width`, `height`, `xoffset`, `yoffset`, `xadvance`, `lineHeight`, etc.) are converted to **numbers**.
* `chars.count` and `kernings.count` are kept as **strings**, matching typical bitmap font metadata.

### 🔸 Optional Fields

* **`kernings`** is **optional**.
  It will appear in the JSON output **only if the source file contains kerning pairs**.
  If no kerning information is present, the `kernings` field is omitted entirely.

Example without `kernings`:

```json
{
  "info": [...],
  "common": [...],
  "pages": [...],
  "chars": { ... }
}
```

---

## 🛠 How It Works

1. The tool automatically detects the input type:

   * XML `<font>...</font>`
   * ASCII `.fnt` text

2. Text `.fnt` parsing supports the classic AngelCode-style blocks:

   * `info`
   * `common`
   * `page`
   * `chars` / `char`
   * `kernings` / `kerning`

3. XML parsing is done via [`fast-xml-parser`](https://github.com/NaturalIntelligence/fast-xml-parser) (ESM CDN).

4. The parsed data is normalized into a single `font` object and then mapped into the final JSON format used by this tool.

---

## 🔧 Development

* Single static **HTML** file (`index.html`)
* Plain **vanilla JavaScript**
* **fast-xml-parser** loaded via ES module CDN
* No build step required — just push to GitHub Pages or open `index.html` in a browser

Repository structure:

```text
/
  index.html
  README.md
```

---

## 📄 License

MIT — free to use in any project.
