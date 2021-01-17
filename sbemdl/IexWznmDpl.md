[back](../sbemdl.md)

Components and releases ``IexWznmDpl``
===

Schema
---

![](./IexWznmDpl.jpg)

<p align="center"><em>Figure 1: Components and releases schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\+ Component [``[ImeIMComponent]``](#1-component-imeimcomponent)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Release [``[ImeIMRelease]``](#11-release-imeimrelease)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Libraries [``[ImeIRMComponentMLibrary]``](#12-libraries-imeirmcomponentmlibrary)

[//]: # (IP structure - END)

Details
---

### 1 Component ``[ImeIMComponent]``

[//]: # (IP ImeIMComponent.superUse - BEGIN)

Use: define artefacts of WhizniumSBE code generation process.

[//]: # (IP ImeIMComponent.superUse - END)

[//]: # (IP ImeIMComponent.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>eng: main engine<br>openg: operation engine<br>cmbeng: combined engine<br>dbs: database access library<br>webapp: web app user interface files<br>api: API library<br>japi: Java API package|
sref (string)|identifier|
Title (string)|title|
Comment (string)|comment|

[//]: # (IP ImeIMComponent.columns - END)

### 1.1 Release ``[ImeIMRelease]``

[//]: # (IP ImeIMRelease.superUse - BEGIN)

Super import: component (1:N)

Use: define component-machine pairs in order to generate corresponding build scripts and makefiles.

[//]: # (IP ImeIMRelease.superUse - END)

[//]: # (IP ImeIMRelease.columns - BEGIN)

Column|Content|
-|-|
hsrefRefWznmMMachine (string)|machine|
sref (string)|identifier|
srefsKOption (string)|options<br>linkstat: link static libraries only<br>dynlib: generate dynamic link library<br>stripdbg: strip debug symbols|
Comment (string)|comment|

[//]: # (IP ImeIMRelease.columns - END)

### 1.2 Libraries ``[ImeIRMComponentMLibrary]``

[//]: # (IP ImeIRMComponentMLibrary.superUse - BEGIN)

Super import: component (1:N)

Use: specifiy external libraries to link to.

[//]: # (IP ImeIRMComponentMLibrary.superUse - END)

[//]: # (IP ImeIRMComponentMLibrary.columns - BEGIN)

Column|Content|
-|-|
srefRefWznmMLibrary (string)|library|

[//]: # (IP ImeIRMComponentMLibrary.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
