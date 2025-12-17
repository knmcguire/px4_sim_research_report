# PX4 Simulation Integration Survey

Here is the report of the PX4 intergration survey done in (October 14 – November 16, 2025), sponsored by Dronecode Foundation. 

A rendered html version on this report can be found here: <https://www.mcguirerobotics.com/px4_sim_research_report/>

## Documentation Structure

The report is organized across multiple markdown files in the `docs/` directory:

- `index.qmd` - Main entry point with metadata and includes
- `docs/preperation_survey.md` - Survey design, pilot analysis, and forum analysis
- `docs/results.md` - Survey results and analysis
- `docs/conclusion.md` - Discussion and recommendations
- `docs/survey_content_pilot.md` - Pilot survey appendix
- `docs/survey_content_final.md` - Final survey appendix


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


## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). 

Under this license, you are free to:
* **Share** — copy and redistribute the material in any medium or format.
* **Adapt** — remix, transform, and build upon the material for any purpose, even commercially.

**Under the following terms:**
* **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. 

## Citation

If you use this report or the data within it, please cite it as follows:

> McGuire, K. (2025). PX4 Simulation Integration Survey Report. McGuire Robotics AB. Available at: https://www.mcguirerobotics.com/px4_sim_research_report/


For BibTeX users:

```bibtex
@techreport{mcguire2025px4survey,
  author = {McGuire, Kimberly},
  title = {PX4 Simulation Integration Survey Report},
  institution = {McGuire Robotifcs AB},
  year = {2025},
  url = {[https://www.mcguirerobotics.com/px4_sim_research_report/(https://www.mcguirerobotics.com/px4_sim_research_report/}
}
