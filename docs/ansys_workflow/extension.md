# Extension Overview

This page displays the architecture of the extension and its components. For a detailed overview of the workflow, go to [**Tools/Equivalent Lateral Force**](../tools/equivalent_lateral_force/elf.md).

- [Architecture](#architecture)
- [Requirements (as Tested)](#requirements-as-tested)
- [ANSYS ACT Data](#ansys-act-data)
- [GUI Functions](#gui-functions)
- [Utility Scripts](#utility-scripts)
    - [`data.py`](#datapy)
    - [`panels.py`](#panelspy)
    - [`analyses.py`](#analysesspy)
    - [`base_class.py`](#base_classpy)
    - [`helpers.py`](#helperspy)
    - [`plotting_utils.py`](#plotting_utilspy)
    - [`visualization.py`](#visualizationpy)
- [Processing Scripts](#processing-scripts)
    - [`connections.py`](#connectionsspy)
    - [`loads.py`](#loadspy)
    - [`masonry_shell_verification.py`](#shell_verificationpy)
    - [`period_utils.py`](#period_utilspy)
    - [`postprocess.py`](#postprocesspy)


## Architecture

The ANSYS ACT is packaged in the following format:

```mermaid
---
config:
  htmlLabels: false
---
flowchart TD
    GUI["`**GUI Functions**
            Analysis
            Loads
            Site
            Get Stories
            Optimize Mesh
            Assign Coordinate Systems
            Connections
            Estimate Period
            SDOF/MDOF Approximation
            Verification
            Plot Results`"]
    click GUI "#gui-functions"

    subgraph "<u>ANSYS ACT Data</u>"
        direction LR
        I[images]
        X[equivalent_lateral_force.xml]
    end
    click X "#equivalent_lateral_forcexml"
    click I "#images"

    subgraph "<u>Utility Scripts</u>"
        A[analyses.py]
        B[base_class.py]
        D[data.py]
        H[helpers.py]
        P[panels.py]
        PL[plotting_utils.py]
        V[visualization.py]
    end
    click A "#analysespy"
    click B "../../data_classes/dataclass"
    click D "#datapy"
    click H "#helperspy"
    click P "#panelspy"
    click PL "#plotting_utilspy"
    click V "../../tools/visualization"

    subgraph "<u>Processing Scripts</u>"
        C[connections.py]
        L[loads.py]
        S[masonry_shell_verification.py]
        PU[period_utils.py]
        PP[postprocess.py]
    end
    click C "../../tools/connections"
    click L "../../tools/loads"
    click S "../../tools/verification"
    click PU "#period_utilspy"
    click PP "#postprocesspy"

        M[main.py]
        click M "#mainpy"

        GUI-->M

        M-->D
        M-->P

        P-->V
        P-->PL

        D-->B
        D-->A

        B<-.->C
        B<-.->PU
        B<-.->L    
```
<u>Note:</u> *most significant function calls and data transfers displayed*

## Requirements *(as Tested)*

- ANSYS Workbench 2026/R1 including:
    - Mechanical
    - Discovery or Spaceclaim *(if modeling directly within Workbench)*
- IronPython 2.7.4 (bundled with ANSYS)

## ANSYS ACT Data

### `equivalent_lateral_force.xml`
Establishes connections between Workbench and the extension and stores GUI elements.

### `images/`
Directory for relevant GUI icons.

## GUI Functions
*For process details, go to page:*

- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/pref.png" style="height: 2em; vertical-align: middle;">
    Analysis
    </a>
- <a href="../../tools/loads.md">
    <img src="../../media/loads.png" style="height: 2em; vertical-align: middle;">
    Loads
    </a>
- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/soil.png" style="height: 2em; vertical-align: middle;">
    Site
    </a>
- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/stories.png" style="height: 2em; vertical-align: middle;">
    Get Stories
    </a>
- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/meshopt.png" style="height: 2em; vertical-align: middle;">
    Optimize Mesh
    </a>
- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/coords.png" style="height: 2em; vertical-align: middle;">
    Assign Coordinate Systems
    </a>
- <a href="../../tools/connections.md">
    <img src="../../media/conn.png" style="height: 2em; vertical-align: middle;">
    Connections
    </a>
- <a href="../../tools/equivalent_lateral_force/elf.md">
    <img src="../../media/period.png" style="height: 2em; vertical-align: middle;">
    Estimate Period
    </a>
- <a href="../../tools/equivalent_lateral_force/sdof_mdof.md">
    <img src="../../media/sdof.png" style="height: 2em; vertical-align: middle;">
    SDOF/MDOF Approximation
    </a>
- <a href="../../tools/verification.md">
    <img src="../../media/plotting.png" style="height: 2em; vertical-align: middle;">
    Verification
    </a>
- <a href="../../tools/visualization.md">
    <img src="../../media/overlay.png" style="height: 2em; vertical-align: middle;">
    Plot Results
    </a>


## `main.py`
Acts as the compatibilty layer between ACT and function scripts. Uses lazy function calls and injects API into distributed scripts.

## Utility Scripts

### `data.py`
Stores default values for calculations, defined according to SIA 260 ([*Inputs*](../tools/equivalent_lateral_force/inputs.md)). Handles I/O with ANSYS simulation objects and state save files for extension parameters.

### `panels.py`
Defines utilities and function calls for drawing function-specific GUI panels and relevant plots. Calls backend functions within relevant sections.

---

### `analyses.py`
Handles *Mechanical: Analysis* objects, computes SDOF and MDOF approximations.

### `base_class,py`
Data class storing geometric simulation data and geometric pre-processing methods. For detailed overview, see [`SeismicNodes`](../data_classes/dataclass.md).

### `helpers.py`
Stores data and math utilities commonly used in other functions.

### `plotting_utils.py`
Includes plotting scripts for drawing spectra, SDOF/MDOF displacement curves and related utilities.

### `visualization.py`
Plotting scripts for single-surface results. For detailed overview, see [**Visualization**](../tools/visualization.md).

### `material_assignment.py`
.

## Processing Scripts

### `connections.py`
Functions for identifying corresponding nodes and generating connections via APDL. For detailed overview, see [**Connections**](../tools/connections.md).

### `loads.py`
Functions for identifying surfaces and applying pre-defined or customized loads in batch. For detailed overview, see [**Loads**](../tools/loads.md).

### `masonry_shell_verification.py`
Functions for processing element-level FE results and evaluating material failure. For detailed overview, see [**Verification**](../tools/verification.md).

### `period_utils.py`


### `postprocess.py`

## To be implemented:
- loading based on equivalent lateral forces
- time-history analysis
- response spectrum analysis
    - lumped-mass simplification
    - direct M/K
- static pushover
- performance-based assessment
- code compliance

*Jump to subsection:*
- [Linear Static Analysis]()
- [Linear Dynamic Analysis]()
- [Nonlinear Static Analysis]()
