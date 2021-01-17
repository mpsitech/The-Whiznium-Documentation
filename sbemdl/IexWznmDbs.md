[back](../sbemdl.md)

Database structure ``IexWznmDbs``
===

Schema
---

![](./IexWznmDbs.jpg)

<p align="center"><em>Figure 1: Database structure schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\- Relations cluster [``[ImeICRelation]``](#1-relations-cluster-imeicrelation)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Relation [``[ImeIMRelation]``](#2-relation-imeimrelation)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMRelationTitle]``](#21-names-imeiamrelationtitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\- Stub [``[ImeIMStub]``](#3-stub-imeimstub)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Table [``[ImeIMTable]``](#4-table-imeimtable)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Load functions [``[ImeIAMTableLoadfct]``](#41-load-functions-imeiamtableloadfct)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMTableTitle]``](#42-names-imeiamtabletitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Feature check [``[ImeIMCheck]``](#43-feature-check-imeimcheck)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Subset [``[ImeIMSubset]``](#44-subset-imeimsubset)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMSubsetTitle]``](#441-names-imeiamsubsettitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Relations to other subsets [``[ImeIRMSubsetMSubset]``](#442-relations-to-other-subsets-imeirmsubsetmsubset)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Table column [``[ImeIMTablecol]``](#45-table-column-imeimtablecol)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMTablecolTitle]``](#451-names-imeiamtablecoltitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector [``[ImeIMVector2]``](#46-vector-imeimvector2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMVectorTitle2]``](#461-names-imeiamvectortitle2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector item [``[ImeIMVectoritem2]``](#462-vector-item-imeimvectoritem2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJMVectoritem2]``](#4621-name-and-comment-by-locale-imeijmvectoritem2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Main table filters [``[ImeIRMTableMVector2]``](#463-main-table-filters-imeirmtablemvector2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector [``[ImeIMVector1]``](#5-vector-imeimvector1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Names [``[ImeIAMVectorTitle1]``](#51-names-imeiamvectortitle1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Vector item [``[ImeIMVectoritem1]``](#52-vector-item-imeimvectoritem1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJMVectoritem1]``](#521-name-and-comment-by-locale-imeijmvectoritem1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Defining tables [``[ImeIRMTableMVector1]``](#53-defining-tables-imeirmtablemvector1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\- Inter-stub dependencies [``[ImeIRMStubMStub]``](#6-inter-stub-dependencies-imeirmstubmstub)

[//]: # (IP structure - END)

Details
---

### 1 Relations cluster ``[ImeICRelation]``

[//]: # (IP ImeICRelation.superUse - BEGIN)

Use: group relations (currently not in use).

[//]: # (IP ImeICRelation.superUse - END)

[//]: # (IP ImeICRelation.columns - BEGIN)

Column|Content|
-|-|
iref (ubigint)|integer reference|

[//]: # (IP ImeICRelation.columns - END)

### 2 Relation ``[ImeIMRelation]``

[//]: # (IP ImeIMRelation.superUse - BEGIN)

Use: establish relations between database tables.

[//]: # (IP ImeIMRelation.superUse - END)

[//]: # (IP ImeIMRelation.columns - BEGIN)

Column|Content|
-|-|
iref (ubigint)|integer reference|
srefIxVBasetype (string)|type<br>grp: owning user group 1:n<br>own: owner 1:n<br>_11: 1:1<br>_1n: 1:n<br>_1npref: pref sub to 1:n<br>_1nsub1n: 1:n sub to 1:n<br>mn: m:n<br>mnsubmn: m:n sub to m:n<br>mnpref: pref sub to m:n<br>drv: univ derivate<br>drvsub: fixed sub to univ derivate<br>drvusub: univ sub to univ derivate<br>inc: inclusion<br>j: jump table 1:n<br>jpref: pref sub to jump table 1:n<br>clust: cluster 1:n<br>aux: aux 1:n<br>auxpref: pref aux to aux 1:n<br>h1n: hierarchical 1:n<br>u1n: universal 1:n<br>u1nsub: 1:n sub to universal 1:n<br>u1nsubpref: pref sub to universal 1:n<br>u1nsubinc: inclusion sub to univ 1:n<br>u1nsub11: 1:1 sub to universal 1:n<br>umn: universal m:n<br>um1n: any main table 1:n<br>a1n: attribute 1:n<br>au1n: attr universal 1:n<br>au1nsub: spec sub to attr univ 1:n<br>as1n: attr string ref 1:n<br>asmn: attr string refs m:n<br>lu1n: list fct univ 1:n<br>lu1nsub: sub to list fct univ 1:n<br>lu1nlsub: list fct sub to lu1n<br>l1nop: operator sub to l1n/lu1n<br>l1noppr: partner sub 1:n to l1nop<br>l1n: list fct 1:n<br>lmn: list fct m:n<br>lmnop: operator sub to lmn<br>lmnoppr: partner sub 1:n to lmnop|
irefRefWznmCRelation (ubigint)|integer reference to relations cluster|
irefSupRefWznmMRelation (ubigint)|super relation|
srefSupIxVSubrole (string)|role in super relation<br>void: none<br>from1n: from table<br>to1n: to table<br>submn: T table<br>pref: preferred<br>frompref: preferred in from table<br>topref: preferred in to table<br>r1n: rel table<br>mn1n: m:n rel table<br>mod: modifier<br>sub: 1:n sub<br>subl: 1:n sub with list fct<br>subinc: inclusion sub<br>sub11: 1:1 sub<br>sub1n: S table<br>pr1: partner 1<br>pr2: partner 2<br>op: list operator<br>toum1n: to any main table<br>spec: specification|
srefFrRefWznmMTable (string)|from table|
srefFrsRefWznmMSubset (string)|from subset|
srefToRefWznmMTable (string)|to table|
srefTosRefWznmMSubset (string)|to subset|
srefRefWznmMTable (string)|table|
Prefix (string)|prefix|
srefsKOption (string)|options<br>self: self-reference<br>preffrom: preferred in from table<br>prefto: preferred in to table<br>enumfrom: enum by from table<br>enumto: enum by to table<br>pref: preferred in to table<br>enum: enumerated<br>ins: insert operation<br>rmv: remove operation<br>ina: insert after operation<br>swp: swap operation<br>affil: affiliation determining|

[//]: # (IP ImeIMRelation.columns - END)

### 2.1 Names ``[ImeIAMRelationTitle]``

[//]: # (IP ImeIAMRelationTitle.superUse - BEGIN)

Super import: relation (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMRelationTitle.superUse - END)

[//]: # (IP ImeIAMRelationTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>fromsngshort: from singular short form<br>fromsngfull: from singular full title<br>tosngshort: to singular short form<br>tosngfull: to singular full title<br>fromplshort: from plural short form<br>fromplfull: from plural full title<br>toplshort: to plural short form<br>toplfull: to plural full title|
srefX2RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIAMRelationTitle.columns - END)

### 3 Stub ``[ImeIMStub]``

[//]: # (IP ImeIMStub.superUse - BEGIN)

Use: human-readable or shorthand representation of a table record.

[//]: # (IP ImeIMStub.superUse - END)

[//]: # (IP ImeIMStub.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>tco: single table column<br>cust: custom implementation|
srefRefWznmMTable (string)|table|
srefRefWznmMSubset (string)|subset|
sref (string)|identifier|
Hierarch (bool)|hierarchical|
srefRefWznmMTablecol (string)|single table column type - table column|
Localized (bool)|localized|
Example (string)|example|

[//]: # (IP ImeIMStub.columns - END)

### 4 Table ``[ImeIMTable]``

[//]: # (IP ImeIMTable.superUse - BEGIN)

Use: database tables excluding query tables.

[//]: # (IP ImeIMTable.superUse - END)

[//]: # (IP ImeIMTable.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>main: main<br>aux: auxiliary<br>rel: m:n<br>jump: jump<br>clust: cluster<br>list: list<br>opr: list operator<br>sub1n: sub 1:n for 1:n<br>submn: sub 1:n for m:n|
srefRefIxVTbl (string)|reference<br>void: none<br>rel: relation|
irefRefUref (ubigint)|rel type - integer reference to relation|
sref (string)|identifier|
Short (string)|acronym|
unqSrefsWznmMTablecol (string)|table columns for uniqueness rule|
Comment (string)|comment|

[//]: # (IP ImeIMTable.columns - END)

### 4.1 Load functions ``[ImeIAMTableLoadfct]``

[//]: # (IP ImeIAMTableLoadfct.superUse - BEGIN)

Super import: table (1:N)

Use: single table SQL SELECT statements frequently used in the engine / operation engine, resulting in dedicated prepared statements and C++ methods.

[//]: # (IP ImeIAMTableLoadfct.superUse - END)

[//]: # (IP ImeIAMTableLoadfct.columns - BEGIN)

Column|Content|
-|-|
srefIxVLoadtype (string)|load type<br>confirm: check presence<br>count: record count<br>ref: single ref<br>refs: set of refs<br>rec: single record<br>rst: record set<br>string: single string value<br>uint: single uint value<br>hrefsup: set of refs hier. up<br>hrefsdown: set of refs hier. down<br>hrstup: record set hier. up<br>hrstdown: record set hier. down|
Fctname (string)|function name|
ldSrefWznmMTablecol (string)|string, uint load types - table column to load|
lbySrefsWznmMTablecol (string)|table columns for SQL WHERE clause|
ordSrefsWznmMTablecol (string)|table columns for SQL ORDER BY clause ; ascending by default, descending with .desc postfix|
srefIxVLimtype (string)|limitation type<br>void: none<br>first: single record<br>limofs: limit/offset parameters|

[//]: # (IP ImeIAMTableLoadfct.columns - END)

### 4.2 Names ``[ImeIAMTableTitle]``

[//]: # (IP ImeIAMTableTitle.superUse - BEGIN)

Super import: table (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMTableTitle.superUse - END)

[//]: # (IP ImeIAMTableTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>sngshort: singular short form<br>sngfull: singular full title<br>plfull: plural full title|
srefX2RefWznmMLocale (string)|locale|
srefIxWznmVGender (string)|gender<br>m: male<br>f: female<br>n: neuter|
Title (string)|name|

[//]: # (IP ImeIAMTableTitle.columns - END)

### 4.3 Feature check ``[ImeIMCheck]``

[//]: # (IP ImeIMCheck.superUse - BEGIN)

Super import: table (1:N)

Use: query record for certain characteristics in C++ code (boolean result).

[//]: # (IP ImeIMCheck.superUse - END)

[//]: # (IP ImeIMCheck.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>eq: table column equals<br>incl: table column includes<br>leaf: leaf of hierarchical table<br>sbs: part of subsets<br>cust: custom check|
srefRefWznmMTablecol (string)|table column|
sref (string)|identifier|
Comment (string)|comment|

[//]: # (IP ImeIMCheck.columns - END)

### 4.4 Subset ``[ImeIMSubset]``

[//]: # (IP ImeIMSubset.superUse - BEGIN)

Super import: table (1:N)

Use: make certain table columns, relations and web-based UI elements available for table records fulfilling certain conditions.

[//]: # (IP ImeIMSubset.superUse - END)

[//]: # (IP ImeIMSubset.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Short (string)|acronym|
Cond (string)|condition rule|
Comment (string)|comment|

[//]: # (IP ImeIMSubset.columns - END)

### 4.4.1 Names ``[ImeIAMSubsetTitle]``

[//]: # (IP ImeIAMSubsetTitle.superUse - BEGIN)

Super import: subset (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMSubsetTitle.superUse - END)

[//]: # (IP ImeIAMSubsetTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>sngshort: singular short form<br>sngfull: singular full title<br>plfull: plural full title|
srefX2RefWznmMLocale (string)|locale|
srefIxWznmVGender (string)|gender<br>m: male<br>f: female<br>n: neuter|
Title (string)|name|

[//]: # (IP ImeIAMSubsetTitle.columns - END)

### 4.4.2 Relations to other subsets ``[ImeIRMSubsetMSubset]``

[//]: # (IP ImeIRMSubsetMSubset.superUse - BEGIN)

Super import: subset (1:N)

Use: give set theory hints to avoid queries which include record duplicates.

[//]: # (IP ImeIRMSubsetMSubset.superUse - END)

[//]: # (IP ImeIRMSubsetMSubset.columns - BEGIN)

Column|Content|
-|-|
srefBsbRefWznmMSubset (string)|"B" subset|
srefIxVReltype (string)|relation type<br>ainb: a includes b<br>bina: b includes a<br>compl: complement<br>disj: disjointedness<br>xsec: intersection|

[//]: # (IP ImeIRMSubsetMSubset.columns - END)

### 4.5 Table column ``[ImeIMTablecol]``

[//]: # (IP ImeIMTablecol.superUse - BEGIN)

Super import: table (1:N)

Use: self-explanatory.

[//]: # (IP ImeIMTablecol.superUse - END)

[//]: # (IP ImeIMTablecol.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>idref: identifying reference<br>idsref: identidying string reference<br>klref: key list reference<br>tblref: table reference<br>tblsref: table string reference<br>vecref: vector reference<br>uvsref: universal vector string reference<br>grp: owning user group reference<br>own: owner reference<br>enum: enumerator<br>lvl: level in hierarchy<br>intval: integer value<br>dblval: double value<br>boolval: boolean value<br>txtval: text value<br>timeval: time value<br>expr: code expression|
srefRefWznmMSubset (string)|subset applicable to|
irefRefWznmMRelation (ubigint)|tblref, tblsref, grp, own, enum, lvl types - relation|
srefFctIxVTbl (string)|functionality<br>void: none<br>tbl: table<br>vec: vector|
srefFctUref (string)|tbl functionality - table, vec functionality - vector|
sref (string)|identifier|
Short (string)|acronym|
srefIxVSubtype (string)|subtype<br>void: none<br>_[type:klref]_<br>klrefopt: optional<br>klrefsng: single<br>klrefmult: multi<br>_[type:tblref]_<br>trefspec: specific table<br>trefuniv: universal table<br>trefmin: minor reference<br>trefclu: cluster table<br>_[type:tblsref]_<br>tsrefsng: single<br>tsrefmult: multi<br>_[type:vecref]_<br>vreflin: linear vector index<br>vrefand: AND mask for mc vector<br>_[type:enum]_<br>enauto: automatic increment<br>enspec: specific numbering<br>_[type:intval]_<br>tinyint: integer / byte (8bit)<br>utinyint: unsigned integer / byte (8bit)<br>smallint: integer (16bit)<br>usmallint: unsigned integer (16bit)<br>int: integer (32bit)<br>uint: unsigned integer (32bit)<br>bigint: integer (64bit)<br>ubigint: unsigned integer (64bit)<br>_[type:txtval]_<br>txt5: max. 5 characters<br>txt10: max. 10 characters<br>txt30: max. 30 characters<br>txt50: max. 50 characters<br>txt100: max. 100 characters<br>txt192: max. 192 characters<br>txtlong: text field (unlimited)<br>txtbase64: Base64 encoded binary (unlimited)<br>_[type:timeval]_<br>tmdate: date<br>tmtime: time<br>tmstamp: time stamp<br>tmustamp: time stamp with usecs|
srefIxVAxisfct (string)|axis functionality<br>void: not applicable<br>pt: point<br>spt: starting point<br>ept: end point|
srefsKOption (string)|options<br>idx: indexed|
Principal (bool)|principal|
Eponymous (bool)|eponymous for record|

[//]: # (IP ImeIMTablecol.columns - END)

### 4.5.1 Names ``[ImeIAMTablecolTitle]``

[//]: # (IP ImeIAMTablecolTitle.superUse - BEGIN)

Super import: table column (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMTablecolTitle.superUse - END)

[//]: # (IP ImeIAMTablecolTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>short: short form<br>full: full title|
srefX2RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIAMTablecolTitle.columns - END)

### 4.6 Vector ``[ImeIMVector2]``

[//]: # (IP ImeIMVector2.superUse - BEGIN)

Super import: table (1:N)

Use: table-specific vector, key list of value list.

[//]: # (IP ImeIMVector2.superUse - END)

[//]: # (IP ImeIMVector2.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>lin: linear<br>or: multiple-choice<br>klst: key list<br>vlst: value list|
sref (string)|identifier|
osrefWznmKTaggrp (string)|source tag group<br>access: VecXxxxWAccess item<br>adrtype: address type<br>ctdet: contact detail<br>ctry: country<br>error: VecXxxxVError item<br>expstate: VecXxxxVExpstate item<br>iexsge: import/export complex job stage<br>iop: VecXxxxVIop item<br>lat: VecXxxxVLat item<br>lop: VecXxxxVLop item<br>mimetype: MIME type<br>no: no thing<br>none: none<br>oolop: VecXxxxVOolop item<br>prs: default person<br>prstit: person title<br>qrystate: VecXxxxVQrystate item<br>recaccess: VecXxxxVRecaccess item<br>reqitmode: VecXxxxVReqitmode item<br>sex: sex<br>start: login card<br>stdalr: standard alert message<br>stdiex: standard import/export complex title<br>stdrel: standard relation title<br>stdtbl: standard table title<br>stdtco: standard table column title<br>stdvec: standard vector title<br>userlevel: VecXxxxVUserlevel item<br>usrste: user state<br>wkday: weekday|
srefsKOption (string)|options<br>noloc: non-localized<br>notit: no titles<br>cmt: comments<br>apdfed: append to feed<br>filfed: fill feed|

[//]: # (IP ImeIMVector2.columns - END)

### 4.6.1 Names ``[ImeIAMVectorTitle2]``

[//]: # (IP ImeIAMVectorTitle2.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMVectorTitle2.superUse - END)

[//]: # (IP ImeIAMVectorTitle2.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>short: short form<br>full: full title|
srefX2RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIAMVectorTitle2.columns - END)

### 4.6.2 Vector item ``[ImeIMVectoritem2]``

[//]: # (IP ImeIMVectoritem2.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIMVectoritem2.superUse - END)

[//]: # (IP ImeIMVectoritem2.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Avail (string)|availability rule|
Implied (string)|rule for implied|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIMVectoritem2.columns - END)

### 4.6.2.1 Name and comment by locale ``[ImeIJMVectoritem2]``

[//]: # (IP ImeIJMVectoritem2.superUse - BEGIN)

Super import: vector item (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMVectoritem2.superUse - END)

[//]: # (IP ImeIJMVectoritem2.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIJMVectoritem2.columns - END)

### 4.6.3 Main table filters ``[ImeIRMTableMVector2]``

[//]: # (IP ImeIRMTableMVector2.superUse - BEGIN)

Super import: vector (1:N)

Use: key lists only - main tables to the records of which the key list's keys refer.

[//]: # (IP ImeIRMTableMVector2.superUse - END)

[//]: # (IP ImeIRMTableMVector2.columns - BEGIN)

Column|Content|
-|-|
srefRefWznmMTable (string)|table|
srefRefWznmMSubset (string)|subset|

[//]: # (IP ImeIRMTableMVector2.columns - END)

### 5 Vector ``[ImeIMVector1]``

[//]: # (IP ImeIMVector1.superUse - BEGIN)

Use: database-specific vector.

[//]: # (IP ImeIMVector1.superUse - END)

[//]: # (IP ImeIMVector1.columns - BEGIN)

Column|Content|
-|-|
srefIxVBasetype (string)|type<br>lin: linear<br>or: multiple-choice<br>klst: key list<br>vlst: value list|
sref (string)|identifier|
osrefWznmKTaggrp (string)|source tag group<br>access: VecXxxxWAccess item<br>adrtype: address type<br>ctdet: contact detail<br>ctry: country<br>error: VecXxxxVError item<br>expstate: VecXxxxVExpstate item<br>iexsge: import/export complex job stage<br>iop: VecXxxxVIop item<br>lat: VecXxxxVLat item<br>lop: VecXxxxVLop item<br>mimetype: MIME type<br>no: no thing<br>none: none<br>oolop: VecXxxxVOolop item<br>prs: default person<br>prstit: person title<br>qrystate: VecXxxxVQrystate item<br>recaccess: VecXxxxVRecaccess item<br>reqitmode: VecXxxxVReqitmode item<br>sex: sex<br>start: login card<br>stdalr: standard alert message<br>stdiex: standard import/export complex title<br>stdrel: standard relation title<br>stdtbl: standard table title<br>stdtco: standard table column title<br>stdvec: standard vector title<br>userlevel: VecXxxxVUserlevel item<br>usrste: user state<br>wkday: weekday|
srefsKOption (string)|options<br>noloc: non-localized<br>notit: no titles<br>cmt: comments<br>apdfed: append to feed<br>filfed: fill feed|

[//]: # (IP ImeIMVector1.columns - END)

### 5.1 Names ``[ImeIAMVectorTitle1]``

[//]: # (IP ImeIAMVectorTitle1.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIAMVectorTitle1.superUse - END)

[//]: # (IP ImeIAMVectorTitle1.columns - BEGIN)

Column|Content|
-|-|
srefX1IxVType (string)|type<br>short: short form<br>full: full title|
srefX2RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIAMVectorTitle1.columns - END)

### 5.2 Vector item ``[ImeIMVectoritem1]``

[//]: # (IP ImeIMVectoritem1.superUse - BEGIN)

Super import: vector (1:N)

Use: self-explanatory.

[//]: # (IP ImeIMVectoritem1.superUse - END)

[//]: # (IP ImeIMVectoritem1.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Avail (string)|availability rule|
Implied (string)|rule for implied|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIMVectoritem1.columns - END)

### 5.2.1 Name and comment by locale ``[ImeIJMVectoritem1]``

[//]: # (IP ImeIJMVectoritem1.superUse - BEGIN)

Super import: vector item (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMVectoritem1.superUse - END)

[//]: # (IP ImeIJMVectoritem1.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|
Comment (string)|Comment|

[//]: # (IP ImeIJMVectoritem1.columns - END)

### 5.3 Defining tables ``[ImeIRMTableMVector1]``

[//]: # (IP ImeIRMTableMVector1.superUse - BEGIN)

Super import: vector (1:N)

Use: key lists only - tables which use this key list, resulting in editing functionality in the table's card.

[//]: # (IP ImeIRMTableMVector1.superUse - END)

[//]: # (IP ImeIRMTableMVector1.columns - BEGIN)

Column|Content|
-|-|
srefRefWznmMTable (string)|table|
srefRefWznmMSubset (string)|subset|

[//]: # (IP ImeIRMTableMVector1.columns - END)

### 6 Inter-stub dependencies ``[ImeIRMStubMStub]``

[//]: # (IP ImeIRMStubMStub.superUse - BEGIN)

Use: establish hierarchy for automated stub updates.

[//]: # (IP ImeIRMStubMStub.superUse - END)

[//]: # (IP ImeIRMStubMStub.columns - BEGIN)

Column|Content|
-|-|
srefSupRefWznmMStub (string)|super stub|
srefSubRefWznmMStub (string)|sub-stub (containing super stub)|

[//]: # (IP ImeIRMStubMStub.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
