# Functions
For all functions operating with the `SeismicNodes` class, see [SeismicNodes/Methods](../../data_classes/dataclass.md/#methods)

## `define_loads`
Defines loads according to selected parameters, and assigns them to corresponding elements.

**Inputs**

- *Mesh nodes, elements*: inherited from `SeismicNodes` class
- *Variable loads*: from selection, see [Inputs/Variable Loads](inputs/#variable-loads)
- *Safety factors*: inherited from building classes, see [Inputs/Building Class](inputs/#building-class)
- *Snow load*: expected snow load, inherited from SIA 261
- *Elevation*: height of the building ASL, used to reduce snow factor
    - $s_k =[1+(\frac{h_0}{350})^2]\cdot 0.4kN/m^2\geq 0.9 kN/m^2$
- *Accessible roof*: boolean toggle to use floor loading on roofs

**Outputs**

- Updated `SeismicNodes.loads` with characteristic values for each storey and roof component



## `period`