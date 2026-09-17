# WP-CAD-2D
WP CAD 2D
# UNISEFE CAD 2D

**Version:** 0.0.1 Alpha
**CAD Engine:** UNISEFE CAD 2D v0.0.6 Alpha
**Platform:** WordPress
**Type:** Browser-based 2D CAD
**Interface:** HTML + SVG + JavaScript
**License:** MIT

---

## Overview

**UNISEFE CAD 2D** is a lightweight browser-based 2D CAD application packaged as a WordPress plugin.

The CAD engine remains self-contained and is loaded by WordPress without restructuring the original application.

The WordPress layer acts only as a lightweight container around the CAD environment.

The goal is to keep the CAD independent from the active WordPress theme and reusable across different websites.

The CAD interface includes its own toolbar, drawing area, properties panel, state system and geometric calculation logic.

---

# Main Features

## 2D Drawing

The current CAD engine includes tools for:

* Line
* Dashed line
* Dash-dot line
* Circle
* Arc
* Text

The drawing area uses a native SVG surface.

Entities remain vector objects instead of raster graphics.

---

# Dimensioning

The CAD includes native dimension tools for:

* Linear dimensions
* Angular dimensions
* Progressive aligned dimensions

Dimension values are calculated directly from geometric relations.

The number of displayed decimal places can be configured from the properties panel.

---

# Editing Tools

Available editing commands include:

* Select
* Undo
* Move
* Copy
* Trim
* Extend
* Fillet
* Mirror
* Rotate
* Delete

The CAD supports selection of drawing entities directly inside the SVG workspace.

---

# View Controls

The drawing environment includes:

* Fit drawing to view
* Zoom
* Pan
* Cursor-centered zoom
* Dynamic viewport calculation

The visible CAD space is recalculated according to the current viewport center and zoom scale.

---

# Snap System

The CAD includes several geometric snap modes.

Currently available:

* Grid / numeric snap
* Midpoint
* Quadrant
* Intersection
* Perpendicular
* Tangent

Snap calculations use geometric relationships rather than only visual proximity.

---

# Geometric Relations

The engine contains native mathematical relations for several geometric operations.

Examples include:

* Distance between two points
* Midpoint calculation
* Segment projection
* Perpendicular projection
* Line-line intersection
* Line-circle intersection
* Circle-circle intersection
* Tangent points
* Rotation
* Mirror transformation
* Arc geometry
* Fillet geometry

Several of these relations are stored as persistent RIKI chains inside the CAD space.

---

# Native Curves

Circles and arcs are represented as native geometric entities.

The CAD does not require converting a circle into a polygon only for visualization.

SVG native geometry is used for rendering.

---

# RIKI Space

The CAD contains an internal **RIKI Space**.

The Space stores persistent named values and geometric relationships used by the application.

Examples include:

```text
SPACE
CAD
TOOL
SNAP
VIEW_X
VIEW_Y
VIEW_SCALE
TEXT_SIZE
LINE_COLOR
LINE_WIDTH
POINT
DIMENSION
```

Each RIKI value can contain:

```text
NAME
VALUE
BIT
```

The current CAD also contains permanent geometric chains such as:

```text
DIST
DX
DY
MID_X
MID_Y
INT_X
INT_Y
PERP_X
PERP_Y
ROT_X
ROT_Y
MIR_X
MIR_Y
```

The objective is to maintain geometric relationships inside one persistent state instead of creating independent calculation engines for each command.

---

# Δ / BIT State

The CAD exposes the RIKI validation concept directly in the interface.

Example:

```text
POINT · Δ 0 · BIT 1
```

The general concept is:

```text
Δ = 0
BIT = 1
```

when the requested relation is considered closed according to the current calculation state.

The CAD also contains a native `SELF_TEST` state.

---

# Persistent Drawing Region

Drawing entities are stored inside a persistent CAD region:

```html
<riki-region name="DRAWING" permanent="true">
```

Geometric chains are stored separately inside the same RIKI Space:

```html
<riki-region name="CHAINS" permanent="true">
```

This structure is intended to keep state, geometry and mathematical relations inside one logical environment.

---

# User Interface

The CAD interface includes:

* Top CAD toolbar
* White drawing canvas
* Native SVG drawing area
* Coordinates HUD
* Command HUD
* Selection status
* Entity counter
* Sliding properties panel

The interface is designed to remain compact and usable without requiring the WordPress administration interface.

---

# Responsive Interface

The interface includes responsive layouts for:

* Desktop
* Tablet
* Mobile
* Small mobile screens
* Landscape mobile devices

On smaller screens, the properties panel becomes a slide-out panel to preserve drawing space.

---

# Properties Panel

The properties panel currently provides controls for:

## Line

* Color
* Width

## View and Drawing

* Snap
* Midpoint snap
* Quadrant snap
* Intersection snap
* Perpendicular snap
* Tangent snap
* Text size
* Dimension decimals

---

# Project Management

The CAD provides basic project commands:

* Open
* Save
* Print
* Save as PDF through browser printing

The project can therefore remain independent from the WordPress database.

---

# WordPress Integration

The plugin intentionally keeps WordPress integration minimal.

WordPress is used mainly to:

1. Load the CAD application.
2. Display it inside a page.
3. Provide shortcode integration.

The CAD engine itself remains independent.

---

# Installation

Download the plugin ZIP.

In WordPress go to:

```text
Plugins
→ Add New Plugin
→ Upload Plugin
```

Upload:

```text
unisefe-cad-2d-0.0.1-alpha.zip
```

Activate the plugin.

---

# Shortcode

Insert the CAD in any WordPress page using:

```text
[unisefe_cad_2d]
```

An additional alias is available:

```text
[riki_cad_2d]
```

---

# Custom Height

The CAD height can be specified directly in the shortcode.

Example:

```text
[unisefe_cad_2d height="900px"]
```

or:

```text
[unisefe_cad_2d height="85vh"]
```

This makes it possible to adapt the CAD to different WordPress layouts.

---

# Architecture

The plugin follows a deliberately simple architecture.

```text
WordPress
    │
    ▼
Plugin wrapper
    │
    ▼
UNISEFE CAD 2D
    │
    ├── HTML interface
    ├── SVG drawing surface
    ├── CAD commands
    ├── RIKI Space
    ├── Geometric chains
    └── Persistent drawing state
```

The WordPress layer should not duplicate the CAD engine.

---

# Design Principle

The plugin is intentionally designed around a simple principle:

> WordPress hosts the CAD.
> WordPress does not become the CAD.

This keeps the application portable and reduces dependencies between the CAD engine, the WordPress theme and other plugins.

---

# Portability

Because the main CAD application is self-contained, the same engine can potentially be used in:

* WordPress
* Static HTML pages
* GitHub Pages
* Local browser environments
* Web applications
* Other CMS platforms

Only the external wrapper needs to change.

---

# Current Status

**Alpha**

The project is under active development.

Current development areas include:

* CAD command refinement
* Geometric reliability
* Snap system improvements
* Arc handling
* Selection behavior
* Mobile interaction
* RIKI state validation
* Import/export improvements
* Structural CAD integration

The Alpha designation means that commands and internal structures may still change.

---

# Planned Evolution

Possible future modules include:

```text
UNISEFE CAD 2D
        │
        ├── RIKI Section
        ├── RIKI Connection
        ├── Structural calculations
        └── UNISEFE CAD 3D
```

The intention is to preserve a common CAD interface and common RIKI state model across the different applications.

---

# Philosophy

UNISEFE CAD is being developed around a lightweight, transparent and browser-native approach.

Instead of depending on a large external CAD framework, the project attempts to keep geometry, state, interface and mathematical relations directly inspectable.

The aim is not only to draw entities, but to maintain meaningful relationships between them inside a persistent computational space.

---

# Technical Notes

Current technologies include:

```text
HTML5
CSS
JavaScript
SVG
WordPress / PHP wrapper
```

The drawing surface uses native SVG.

No external CAD framework is required by the current application.

---

# Repository Structure

Typical plugin structure:

```text
unisefe-cad-2d/
│
├── unisefe-cad-2d.php
├── app/
│   └── unisefe-cad-2d.html
│
└── README.md
```

The main CAD application remains inside the `app` directory.

---

# Version

```text
UNISEFE CAD 2D
WordPress Plugin 0.0.1 Alpha
CAD Engine 0.0.6 Alpha
```

---

# Author

**ITALFABER / UNISEFE**

Website:

https://italfaber.com/

---

# License

MIT License

The software may be used, studied, modified and redistributed according to the terms of the MIT License.

---

## Experimental Project

UNISEFE CAD 2D is an experimental CAD project under active development.

It should currently be considered an **Alpha software environment**, suitable for testing, experimentation and continued development.
