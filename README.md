# Custom Quarto Reveal.js Template

This repository contains an advanced template for Quarto presentations using Reveal.js. It is designed to integrate interactive charts (Plotly), maps (Folium), and custom styles.

## Quick Start

To preview the presentation in real-time:
```bash
quarto preview template.qmd --no-browser --no-watch-inputs
```

## Environment Configuration (macOS)

On recent versions of macOS, **PEP 668** security prevents the global installation of packages via `pip`. It is essential to use a virtual environment so that Quarto can execute Python code blocks (Jupyter).

### Setting up the Virtual Environment

1.  **Create the environment:**
    ```bash
    python3 -m venv .venv
    ```
2.  **Activate the environment:**
    ```bash
    source .venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install jupyter pyyaml matplotlib numpy folium plotly
    ```

> **Note:** Remember to reactivate the environment using `source .venv/bin/activate` every time you reopen your terminal. Or if you use VSCode and want something automated export the good variable in your rc file `export QUARTO_PYTHON="/Users/tlavigne/Documents/softwares/python_venv/venv/bin/python"`.

---

## Quarto & Reveal.js Tips

### 1. Containers and Divs (The famous `:`)
The number of consecutive colons (`:`) is crucial in Quarto. They are used to delimit blocks (somewhat equivalent to `{}` in LaTeX).
* **Golden Rule:** A child block must always have **more** dots than its parent block (as shown in the example below to ensure proper nesting).
* *Example:*
    ```markdown
    ::: {.columns}
      :::: {.column width="50%"}
        Column content
      ::::
    :::
    ```

### 2. Interactivity vs. Chalkboard
The **Chalkboard** plugin creates a transparent layer over the slides to allow drawing. This layer intercepts mouse events, which blocks interactions with Plotly charts or Folium maps.
* **Solution:** To maintain zoom and hover functionality, interactive code must be encapsulated within **Iframes**.

### 3. Useful Resources
* [Official Reveal.js Documentation](https://quarto.org/docs/presentations/revealjs/)
* [Creating Themes](https://quarto.org/docs/presentations/revealjs/themes.html#creating-themes)

---

## Project Structure

```text
.
├── _quarto.yml          # Global configuration (theme, bibliography, menus)
├── template.qmd         # Source file for the presentation
├── styles.css           # Custom CSS adjustments
├── resources/           # Centralized assets folder
│   ├── images/          # Logos, diagrams, icons
│   ├── csv/             # Data for Python charts
│   ├── bibliography/    # .bib files
│   └── pages_style/     # Specific styles per slide type
└── presentation_built/  # Generated HTML output
```

---

## Troubleshooting

**Keyboard shortcuts (B, C) are not working?**
If you have just clicked on an interactive chart (Plotly/Map), it currently has the "focus." Click once on the white background of the slide or on the sidebar to return focus to Reveal.js; the shortcuts will work again.

**The side background does not cover the full height?**
Check the CSS to ensure the element has a `::before` pseudo-element with `content: "";` and negative overflow values (e.g., `top: -2000px`) to compensate for Reveal.js's automatic vertical centering.