[back](../sbemdl.md)

Modules and cards ``IexWznmBui``
===

Schema
---

![](./IexWznmBui.jpg)

<p align="center"><em>Figure 1: Modules and cards schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\+ Module [``[ImeIMModule]``](#1-module-imeimmodule)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJMModule]``](#11-name-and-comment-by-locale-imeijmmodule)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Card [``[ImeIMCard]``](#12-card-imeimcard)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name by locale [``[ImeIJMCardTitle]``](#121-name-by-locale-imeijmcardtitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\- Presetting [``[ImeIMPreset]``](#2-presetting-imeimpreset)

[//]: # (IP structure - END)

Details
---

### 1 Module ``[ImeIMModule]``

[//]: # (IP ImeIMModule.superUse - BEGIN)

Use: grouping entity for cards; relevance: web-based UI navigation screen.

[//]: # (IP ImeIMModule.superUse - END)

[//]: # (IP ImeIMModule.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIMModule.columns - END)

### 1.1 Name and comment by locale ``[ImeIJMModule]``

[//]: # (IP ImeIJMModule.superUse - BEGIN)

Super import: module (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMModule.superUse - END)

[//]: # (IP ImeIJMModule.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIJMModule.columns - END)

### 1.2 Card ``[ImeIMCard]``

[//]: # (IP ImeIMCard.superUse - BEGIN)

Super import: module (1:N)

Use: basic unit for web-based UI, one tab per card; database-backed (tbl, sbs references) with list/record view, else custom content.

[//]: # (IP ImeIMCard.superUse - END)

[//]: # (IP ImeIMCard.columns - BEGIN)

Column|Content|
-|-|
srefRefIxVTbl (string)|reference<br>void: none<br>tbl: table<br>sbs: subset|
srefRefUref (string)|tbl reference - table, sbs reference - subset|
sref (string)|identifier|
Title (string)|name|
Avail (string)|availability rule|
Active (string)|activation rule, typically implicating session-wide presettings|

[//]: # (IP ImeIMCard.columns - END)

### 1.2.1 Name by locale ``[ImeIJMCardTitle]``

[//]: # (IP ImeIJMCardTitle.superUse - BEGIN)

Super import: card (1:N)

Use: self-explanatory. Derived from table name for database-backed cards.

[//]: # (IP ImeIJMCardTitle.superUse - END)

[//]: # (IP ImeIJMCardTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIJMCardTitle.columns - END)

### 2 Presetting ``[ImeIMPreset]``

[//]: # (IP ImeIMPreset.superUse - BEGIN)

Use: the retrieve and update operation can be used to bump up the scope of a record reference presetting from card to session scope.

[//]: # (IP ImeIMPreset.superUse - END)

[//]: # (IP ImeIMPreset.columns - BEGIN)

Column|Content|
-|-|
srefIxWznmVIop (string)|import operation<br>retrupd: retrieve and update|
srefRefIxVTbl (string)|reference<br>void: none<br>tbl: table<br>sbs: subset<br>vec: vector|
srefRefUref (string)|tbl reference - table, sbs reference - subset, vec reference - vector|
srefIxVScope (string)|scope<br>sys: system<br>sess: session<br>car: card<br>pnlrec: record panel<br>pnl: panel|
sref (string)|identifier|
srefIxWznmWArgtype (string)|argument type<br>ix: vector item index<br>ref: record reference<br>refs: set of record references<br>sref: string reference<br>intval: integer value<br>dblval: double value<br>boolval: boolean value<br>txtval: text value|

[//]: # (IP ImeIMPreset.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
