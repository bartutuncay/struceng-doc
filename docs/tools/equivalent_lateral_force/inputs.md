## Inputs

### Geometry, Materials and Connections
Model geometry, cross-sectional and material information is defined by the user as in a standard *Ansys Mechanical* workflow. We provide custom material models and connections for seismic analysis of masonry-reinforced concrete hybrid structures (see [Material Models](../data_classes/materials.md) for further details).

### Building Class
Defined according to the classification in SIA 261. Includes compliance and importance factors; can be selected from existing classes or custom values can be defined.

***TODO: screenshot***

**Default Parameters**

| Class | Compliance Factor \(\alpha_{min}\) | Importance Factor \(\gamma_I\)
| --- | :---: | :---:
| *BWK I* | 0.25 | 1.0
| *BWK II* | 0.25 | 1.2
| *BWK II-s: Educational* | 0.4 | 1.2
| *BWK II-i: Infrastructure* | 0.4 | 1.2
| *BWK III* | 0.4 | 1.5

### Variable Loads
Characteristic values according to SIA 261. Can be selected from existing classes or custom values can be defined.

| Type | Load [\(kN/m^2\)]
| --- | :---:
| Residential | 2
| Office | 3
| Public Areas: with Tables | 3
| Public Areas: Fixed Seating | 4
| Public Areas: Crowded, Sports Venues | 5
| Warehouses | 5
| Parking: \(<3.5t\) | 2
| Parking: \(3.5-16t\) | 5
| Inaccessible Roofs | 0.4

### Ground Acceleration
Defined according to SIA 261:

<img src="/media/seismic_zones_sia_261.png" alt="Seismic Zones" width="500">

| Zone | Typical Acceleration [\(m/s^2\)]
| --- | :---:
| Z1a | 0.6
| Z1b | 0.8
| Z2 | 1.0
| Z3a | 1.3
| Z3b | 1.6

### Soil Class