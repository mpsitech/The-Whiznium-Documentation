[back](../sbemdl.md)

Global features ``IexWznmGbl``
===

Schema
---

![](./IexWznmGbl.jpg)

<p align="center"><em>Figure 1: Global features schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\+ Block [``[ImeIMBlock]``](#1-block-imeimblock)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Items [``[ImeIAMBlockItem]``](#11-items-imeiamblockitem)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Default value by release [``[ImeIJAMBlockItem]``](#111-default-value-by-release-imeijamblockitem)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Items cluster [``[ImeICAMBlockItem]``](#12-items-cluster-imeicamblockitem)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Capability [``[ImeIMCapability]``](#2-capability-imeimcapability)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Parameters [``[ImeIAMCapabilityPar]``](#21-parameters-imeiamcapabilitypar)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Error [``[ImeIMError]``](#3-error-imeimerror)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Text by locale [``[ImeIJMErrorTitle]``](#31-text-by-locale-imeijmerrortitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector [``[ImeIMVector]``](#4-vector-imeimvector)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMVectorTitle]``](#41-names-imeiamvectortitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector item [``[ImeIMVectoritem]``](#42-vector-item-imeimvectoritem)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJMVectoritem]``](#421-name-and-comment-by-locale-imeijmvectoritem)

[//]: # (IP structure - END)

Details
---

### 1 Block ``[ImeIMBlock]``

[//]: # (IP ImeIMBlock.superUse - BEGIN)

Use: define global XML settings blocks for preferences file.

[//]: # (IP ImeIMBlock.superUse - END)

[//]: # (IP ImeIMBlock.columns - BEGIN)

Column|Content|
-|-|
srefsReaIxWznmWScope (string)|read scope<br>app: app<br>cmbeng: combined engine<br>eng: main engine<br>openg: operation engine|
srefsWriIxWznmWScope (string)|write scope<br>app: app<br>cmbeng: combined engine<br>eng: main engine<br>openg: operation engine|
sref (string)|identifier|
Comment (string)|comment|

[//]: # (IP ImeIMBlock.columns - END)

### 1.1 Items ``[ImeIAMBlockItem]``

[//]: # (IP ImeIAMBlockItem.superUse - BEGIN)

Super import: block (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMBlockItem.superUse - END)

[//]: # (IP ImeIAMBlockItem.columns - BEGIN)

Column|Content|
-|-|
irefRefWznmCAMBlockItem (ubigint)|integer reference to items cluster|
srefIxVBasetype (string)|type<br>var: standard variable<br>conpar: control parameter<br>contit: control title<br>feed: feed<br>rst: record set of query table<br>sub: sub-block|
sref (string)|identifier|
srefIxWznmVVartype (string)|variable data type<br>void: not applicable<br>boolean: boolean<br>tinyint: integer / byte (8bit)<br>utinyint: unsigned integer / byte (8bit)<br>smallint: integer (16bit)<br>usmallint: unsigned integer (16bit)<br>int: integer (32bit)<br>uint: unsigned integer (32bit)<br>bigint: integer (64bit)<br>ubigint: unsigned integer (64bit)<br>float: float<br>double: double<br>string: string<br>booleanvec: boolean vector<br>utinyintvec: unsigned int / byte 8bit vector<br>usmallintvec: unsigned int 16bit vector<br>intvec: integer 32bit vector<br>uintvec: unsigned int 32bit vector<br>ubigintvec: unsigned int 64bit vector<br>floatvec: float vector<br>doublevec: double vector<br>floatmat: float matrix<br>doublemat: double matrix<br>stringvec: string vector<br>vecsref: vector entry string reference<br>scrref: scrambled reference|
Defval (string)|default value|
Comment (string)|comment|

[//]: # (IP ImeIAMBlockItem.columns - END)

### 1.1.1 Default value by release ``[ImeIJAMBlockItem]``

[//]: # (IP ImeIJAMBlockItem.superUse - BEGIN)

Super import: items (1:N)

Use: customize default for specific releases.

[//]: # (IP ImeIJAMBlockItem.superUse - END)

[//]: # (IP ImeIJAMBlockItem.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMRelease (string)|release|
Defval (string)|default value|

[//]: # (IP ImeIJAMBlockItem.columns - END)

### 1.2 TblWznmCAMBlockItem ``[ImeICAMBlockItem]``

[//]: # (IP ImeICAMBlockItem.superUse - BEGIN)

Super import: block (1:N)

Use: group items.

[//]: # (IP ImeICAMBlockItem.superUse - END)

[//]: # (IP ImeICAMBlockItem.columns - BEGIN)

Column|Content|
-|-|
iref (ubigint)|integer reference|

[//]: # (IP ImeICAMBlockItem.columns - END)

### 2 Capability ``[ImeIMCapability]``

[//]: # (IP ImeIMCapability.superUse - BEGIN)

Use: instantiate capabilities, such as managed file archive or access rights management from template.

[//]: # (IP ImeIMCapability.superUse - END)

[//]: # (IP ImeIMCapability.columns - BEGIN)

Column|Content|
-|-|
srefTplRefWznmMCapability (string)|template|
sref (string)|identifier|
Title (string)|name|

[//]: # (IP ImeIMCapability.columns - END)

### 2.1 Parameters ``[ImeIAMCapabilityPar]``

[//]: # (IP ImeIAMCapabilityPar.superUse - BEGIN)

Super import: capability (1:N)

Use: parametrize capability.

[//]: # (IP ImeIAMCapabilityPar.superUse - END)

[//]: # (IP ImeIAMCapabilityPar.columns - BEGIN)

Column|Content|
-|-|
x1SrefKKey (string)|key|
Val (string)|value|

[//]: # (IP ImeIAMCapabilityPar.columns - END)

### 3 Error ``[ImeIMError]``

[//]: # (IP ImeIMError.superUse - BEGIN)

Use: add items to the error vector for use with the version's C++ exception.

[//]: # (IP ImeIMError.superUse - END)

[//]: # (IP ImeIMError.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Title (string)|text|

[//]: # (IP ImeIMError.columns - END)

### 3.1 Text by locale ``[ImeIJMErrorTitle]``

[//]: # (IP ImeIJMErrorTitle.superUse - BEGIN)

Super import: error (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMErrorTitle.superUse - END)

[//]: # (IP ImeIJMErrorTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|text|

[//]: # (IP ImeIJMErrorTitle.columns - END)

### 4 Vector ``[ImeIMVector]``

[//]: # (IP ImeIMVector.superUse - BEGIN)

Use: specify vectors with global scope.

[//]: # (IP ImeIMVector.superUse - END)

[//]: # (IP ImeIMVector.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>lin: linear<br>or: multiple-choice|
sref (string)|identifier|
osrefWznmKTaggrp (string)|source tag group<br>access: VecXxxxWAccess item<br>adrtype: address type<br>ctdet: contact detail<br>ctry: country<br>error: VecXxxxVError item<br>expstate: VecXxxxVExpstate item<br>iexsge: import/export complex job stage<br>iop: VecXxxxVIop item<br>lat: VecXxxxVLat item<br>lop: VecXxxxVLop item<br>mimetype: MIME type<br>no: no thing<br>none: none<br>oolop: VecXxxxVOolop item<br>prs: default person<br>prstit: person title<br>qrystate: VecXxxxVQrystate item<br>recaccess: VecXxxxVRecaccess item<br>reqitmode: VecXxxxVReqitmode item<br>sex: sex<br>start: login card<br>stdalr: standard alert message<br>stdiex: standard import/export complex title<br>stdrel: standard relation title<br>stdtbl: standard table title<br>stdtco: standard table column title<br>stdvec: standard vector title<br>userlevel: VecXxxxVUserlevel item<br>usrste: user state<br>wkday: weekday|
srefsKOption (string)|options<br>noloc: non-localized<br>notit: no titles<br>cmt: comments<br>apdfed: append to feed<br>filfed: fill feed|

[//]: # (IP ImeIMVector.columns - END)

### 4.1 Names ``[ImeIAMVectorTitle]``

[//]: # (IP ImeIAMVectorTitle.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMVectorTitle.superUse - END)

[//]: # (IP ImeIAMVectorTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>short: short form<br>full: full title|
srefX2RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIAMVectorTitle.columns - END)

### 4.2 Vector item ``[ImeIMVectoritem]``

[//]: # (IP ImeIMVectoritem.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIMVectoritem.superUse - END)

[//]: # (IP ImeIMVectoritem.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Avail (string)|availability rule|
Implied (string)|rule for implied|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIMVectoritem.columns - END)

### 4.2.1 Name and comment by locale ``[ImeIJMVectoritem]``

[//]: # (IP ImeIJMVectoritem.superUse - BEGIN)

Super import: vector item (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMVectoritem.superUse - END)

[//]: # (IP ImeIJMVectoritem.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIJMVectoritem.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
