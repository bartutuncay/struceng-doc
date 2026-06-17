# Masonry-RC Seismic Hybrid Pipeline - Tools

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

## Load Generator

<u>Pipeline:</u>
```mermaid
flowchart TB

    subgraph "<u>Engineering Inputs</u>"
        E[Input Parameters]
        Ea[Building Class]
        Eb[Soil Class]
        Ec[Members]

        E --> Ea
        E --> Eb
        E --> Ec
    end

    subgraph "<u>Model Definition</u>"
        A[Model]
        D[Structural Parameters]
        B[Mesh]

        A --> D
        A --> B
    end

    subgraph "<u>Processing</u>"
        F[Geometric Segmentation]
        G[Load Generation]

        B --> F
        Ec --> F
        F --> G
        Ea --> G
        Eb --> G
    end
    
    subgraph "<u>Model Output</u>"
        H[Equivalent Lateral Force]
        I[<b>Model with Loads</b>]

        D --> H
        B --> H
        G --> H
        H --> I
    end
```

## Equivalent Lateral Force
*Go to page:*

- [Load Generation](../plugins/elf.md)

## Modal Pushover Analysis
***Reference**: An Implementation of Modal Pushover Analysis for Multistory Buildings in Ansys*