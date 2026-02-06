# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Abraham Duran's brand color reference — the canonical source for colors used across social media, client work, and personal design projects. A single-page static site (no build tools, no frameworks) hosted on GitHub Pages at `brand.abrahamduran.com`.

## Architecture

Everything lives in `index.html` — HTML, CSS, and JavaScript are all inline in one file:

- **CSS** (~280 lines): CSS custom properties power a dark/light theme system (`[data-theme="light"]` / default dark). Uses a grid layout for color cards.
- **Color data**: Three JSON blobs embedded in `<script type="application/json">` tags (`#jsonA`, `#jsonB`, `#jsonC`) representing three different color palettes. Palette C ("Paleta de Colores por Colorimetría") uses Spanish field names (`nombre`, `nota`) while palettes A and B use English field names (`name`, `notes`, `role`).
- **JavaScript** (~300 lines): Vanilla JS that parses the JSON palettes, computes derived color values (HSL, WCAG contrast ratios), renders color cards into the DOM, and handles per-section + global search filtering.

## Key Details

- UI language is Spanish.
- Default theme is `light` (set at end of script and in `<body data-theme="light">`).
- No build step, package manager, or test framework. To preview locally, serve the directory with any static file server.
- WCAG AA/AAA contrast checks are computed against black (`#000`) and white (`#FFF`).
- The `shapeItem()` function normalizes both English and Spanish field names from the JSON data into a common internal format.
