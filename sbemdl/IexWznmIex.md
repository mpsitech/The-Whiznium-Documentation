[back](../sbemdl.md)

Import/export complexes ``IexWznmIex``
===

Schema
---

![](./IexWznmIex.jpg)

<p align="center"><em>Figure 1: Import/export complexes schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\+ Import/export complex [``[ImeIMImpexpcplx]``](#1-Importexport-complex-ImeIMImpexpcplx)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name by locale [``[ImeIJMImpexpcplxTitle]``](#11-Name-by-locale-ImeIJMImpexpcplxTitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Import/export [``[ImeIMImpexp]``](#12-Importexport-ImeIMImpexp)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Import/export column [``[ImeIMImpexpcol]``](#121-Importexport-column-ImeIMImpexpcol)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Stub by vector item [``[ImeIJMImpexpcolStub]``](#1211-Stub-by-vector-item-ImeIJMImpexpcolStub)

[//]: # (IP structure - END)

Details
---

### 1 Import/export complex ``[ImeIMImpexpcplx]``

[//]: # (IP ImeIMImpexpcplx.superUse - BEGIN)

Use: create hierarchical pattern for text-/XML-based import/export of data into/from a set of database tables.

[//]: # (IP ImeIMImpexpcplx.superUse - END)

[//]: # (IP ImeIMImpexpcplx.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Short (string)|acronym|
Title (string)|name|
Minversion (string)|minimum compatible version|
Comment (string)|comment|

[//]: # (IP ImeIMImpexpcplx.columns - END)

### 1.1 Name by locale ``[ImeIJMImpexpcplxTitle]``

[//]: # (IP ImeIJMImpexpcplxTitle.superUse - BEGIN)

Super import: import/export complex (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMImpexpcplxTitle.superUse - END)

[//]: # (IP ImeIJMImpexpcplxTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIJMImpexpcplxTitle.columns - END)

### 1.2 Import/export ``[ImeIMImpexp]``

[//]: # (IP ImeIMImpexp.superUse - BEGIN)

Super import: import/export complex (1:N)

Use: one import/export maps to one database table.

[//]: # (IP ImeIMImpexp.superUse - END)

[//]: # (IP ImeIMImpexp.columns - BEGIN)

Column|Content|
-|-|
iref (ubigint)|integer reference|
irefSupRefWznmMImpexp (ubigint)|integer reference to super import/export|
srefRefWznmMTable (string)|table|
sref (string)|identifier|
rtrSrefsWznmMImpexpcol (string)|retr, retrupd, retrins, rmv import operations - import/export columns by which to retrieve the record|
srefsIxWIop (string)|import operations<br>ins: insert<br>retr: retrieve<br>retrupd: retrieve and update<br>retrins: retrieve, else insert<br>retrupdins: retrieve and update, else insert<br>rmv: remove<br>cust: custom|
Comment (string)|comment|

[//]: # (IP ImeIMImpexp.columns - END)

### 1.2.1 Import/export column ``[ImeIMImpexpcol]``

[//]: # (IP ImeIMImpexpcol.superUse - BEGIN)

Super import: import/export (1:N)

Use: one import/export column maps to one table column with the exception of the iop and iarg types.

[//]: # (IP ImeIMImpexpcol.superUse - END)

[//]: # (IP ImeIMImpexpcol.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>iop: import/export operation<br>idiref: identifying integer reference<br>iref: int ref to import/export item<br>tbl: dual field in table<br>tsref: string ref to table<br>thsref: hierarchical string ref to table<br>thint: textual hint for table ref<br>vsref: string ref to vector item<br>ftm: formatted time stamp/date/time<br>iarg: argument for custom import|
srefsIxWOccurrence (string)|occurrence<br>fil: import/export file<br>tbl: base table|
srefRefWznmMTablecol (string)|table column|
sref (string)|identifier|
Short (string)|acronym|
irefRefWznmMImpexp (ubigint)|sup, sub conversion types - integer reference to corresponding import/export|
srefIxVConvtype (string)|conversion type<br>void: not applicable<br>previmp: find in previous import<br>cust: custom<br>custsql: custom SQL query<br>rst: find in recordset<br>imppp: previous import post-proc.<br>custsqlpp: custom SQL post-proc.<br>ixsref: vector item index vs. string ref<br>incr: increment<br>invftm: invert formatted time<br>sup: reference to super imp./exp.<br>sub: first in sub imp./exp.<br>preset: presetting|
Defval (string)|default value|
srefRefWznmMPreset (string)|preset conversion type - presetting|
srefRefWznmMStub (string)|stub for export|
srefRefWznmMVectoritem (string)|default vector item|

[//]: # (IP ImeIMImpexpcol.columns - END)

### 1.2.1.1 Stub by vector item ``[ImeIJMImpexpcolStub]``

[//]: # (IP ImeIJMImpexpcolStub.superUse - BEGIN)

Super import: import/export column (1:N)

Use: stub distinction for export of universal references

[//]: # (IP ImeIJMImpexpcolStub.superUse - END)

[//]: # (IP ImeIJMImpexpcolStub.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMVectoritem (string)|reference vector vector item|
srefRefWznmMStub (string)|stub|

[//]: # (IP ImeIJMImpexpcolStub.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
