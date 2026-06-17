# `SeismicNodes`

Base data class forming the compatibility layer between the [Equivalent Lateral Force](../tools/elf.md) module and [Ansys Mechanical](https://www.ansys.com/products/structures/ansys-mechanical) software.

## Attributes

| ID    | Type              | Description
| --- | --- | ---
| [`pos`](#pos) | *dictionary* | positional information and data
| [`node_classes`](#node_classes) | *dictionary* | semantic information, stored per node
| [`body_classes`](#body_classes) | *dictionary* | semantic information, stored per geometry
| [`loads`](#loads) | *dictionary* | load information

### `pos`
**Fields**

- <u>body_map</u>: Numerical mapping for Ansys Body IDs associated with each node `str --> dict`
- <u>global</u>: Coordinates of all nodes stored in an array: `[node_id, body_id, X, Y, Z]`
- <u>axes</u>: Global coordinate system reference. `hasattr: 'up_axis', 'right_axis'`

### `node_classes`
**Fields**

- <u>alignment</u>: Numerical mapping for identified geometry types. For assignment process see [`segment_nodes`](#segment_nodes):
    - `0: slab`
    - `1: right axis-aligned wall`
    - `2: forward axis-aligned wall`

### `body_classes`

### `loads`

## Methods

### `get_nodes`
Obtains nodes from existing meshes. If no existing meshes are found, initiates mesh generation with contacts aligned using the native Ansys mesh generator with default parameters. Ansys bodies (surfaces, solids) are enumerated and all nodes are stored in an array with attributes *Node ID, Body ID, X, Y and Z coordinates*.

**Note**: all nodes use the global coordinate system.

### `segment_nodes`
Inputs:

- `SeismicNodes`: base *dataclass*
- `up_axis`: *str*, world up direction according to the global coordinate system. Obtained automatically from dropdown menu in GUI
- `right_axis` : *str*, world right-hand-side axis according to the global coordinate system. Most useful for directional analyses. Obtained automatically from dropdown menu in GUI

