# PX4 Simulation Integration Survey

Here is the report of the PX4 intergration survey done in (October 14 – November 16, 2025), sponsored by Dronecode Foundation. 

## Documentation Structure

The report is organized across multiple markdown files in the `docs/` directory:

- `index.md` - Main entry point with metadata and includes
- `preperation_survey.md` - Survey design, pilot analysis, and forum analysis
- `results.md` - Survey results and analysis
- `conclusion.md` - Discussion and recommendations
- `survey_content_pilot.md` - Pilot survey appendix
- `survey_content_final.md` - Final survey appendix


# Research report setup

This report has been made with [Quarto](https://quarto.org/).

Install dependencies using [Pixi package manager](https://pixi.sh/latest/):

```bash
pixi install
```

## Usage

### Preview the Report (Live Reload)

```bash
pixi run preview
```

This will open a browser with live preview that updates as you edit the markdown files.

### Render to HTML

```bash
pixi run render
```

Output will be in `_site/index.html`

