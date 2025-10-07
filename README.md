# Research Reports with Quarto

This project uses Quarto to generate professional research reports with proper citation management.

## Setup

Install dependencies using pixi:

```bash
pixi install
```

## Usage

### Preview the Report (Live Reload)

```bash
pixi run preview
```

This will open a browser with live preview that updates as you edit the markdown file.

### Render to HTML

```bash
pixi run render
```

Output will be in `_output/docs/px4_survey.html`

### Render to PDF

**First time only:** Install TinyTeX (LaTeX distribution for PDF support)

```bash
pixi run install-latex
```

This downloads ~200MB and only needs to be done once. See `PDF_SETUP.md` for details.

**After TinyTeX is installed:**

```bash
pixi run render-pdf
```

Output will be in `_output/docs/px4_survey.pdf`

### Render to Word

```bash
pixi run render-docx
```

Output will be in `docs/px4_survey.docx`

### Render All Formats

```bash
pixi run render-all
```

## Citations

Citations are managed through BibTeX format in `docs/references.bib`.

### Citation Format

In your markdown files, use:
- `@px4-12345` for inline citations (e.g., "As noted in @px4-12345...")
- `[@px4-12345]` for parenthetical citations (e.g., "This was observed [@px4-12345]")
- `[@px4-12345; @px4-67890]` for multiple citations

Quarto will automatically:
- Format citations according to the style (APA by default)
- Generate a References section at the end
- Create hyperlinks between citations and references

## Project Structure

```
research_reports/
├── _quarto.yml          # Quarto configuration
├── pixi.toml            # Pixi package management
├── styles.css           # Custom CSS for HTML output
├── docs/
│   ├── px4_survey.md   # Main report document
│   └── references.bib  # BibTeX references
└── README.md
```

## Customization

### Change Citation Style

Edit `_quarto.yml` and change the `csl` field to any CSL style from:
https://www.zotero.org/styles

Popular styles:
- APA: `https://www.zotero.org/styles/apa`
- IEEE: `https://www.zotero.org/styles/ieee`
- Nature: `https://www.zotero.org/styles/nature`
- Chicago: `https://www.zotero.org/styles/chicago-author-date`

### Adjust PDF Settings

Edit the `pdf` section in `_quarto.yml` to customize margins, fonts, etc.

### HTML Themes

Change the HTML theme in `_quarto.yml`. Available themes:
- cosmo, flatly, darkly, sketchy, minty, pulse, journal, and more
- See: https://quarto.org/docs/output-formats/html-themes.html

## Benefits of Quarto

✅ **Multiple Output Formats**: HTML, PDF, Word, and more from the same source
✅ **Professional Citations**: Automatic bibliography generation with any citation style
✅ **Live Preview**: See changes instantly as you write
✅ **Academic Quality**: Publication-ready output with proper formatting
✅ **Simpler Setup**: No complex plugin configuration needed
✅ **Cross-platform**: Works on Windows, macOS, and Linux

- Generate a References section at the end
- Create hyperlinks between citations and references

## Project Structure

```
.
├── docs/
│   ├── index.md       # Home page
│   └── test.md        # Test page
├── mkdocs.yml         # MkDocs configuration
├── requirements.txt   # Python dependencies
└── README.md          # This file
```

## Customization

Edit `mkdocs.yml` to customize:
- Site name and description
- Navigation structure
- Theme settings
- Markdown extensions

Add new pages by creating markdown files in the `docs/` directory and updating the `nav` section in `mkdocs.yml`.