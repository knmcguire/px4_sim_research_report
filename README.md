# research_reports

A simple MkDocs documentation site with Material theme.

## Features

- Built with MkDocs and Material theme
- Two test markdown pages demonstrating documentation capabilities
- Responsive and modern design
- Search functionality
- Easy to extend and customize

## Installation

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Usage

### Build the documentation

```bash
mkdocs build
```

This will generate the static site in the `site/` directory.

### Serve the documentation locally

```bash
mkdocs serve
```

This will start a local development server at `http://127.0.0.1:8000/`

### Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

## Structure

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