[back](../sbemdl.md)

Initialization data ``IexWznmIni``
===

Schema
---

![](./IexWznmIni.jpg)

<p align="center"><em>Figure 1: Initialization data schema - table columns in light blue are part of the input file, table columns in dark blue are inferred</em></p>

Structure
---

[//]: # (IP structure - BEGIN)

&nbsp;&nbsp;&nbsp;&nbsp;\- Parameters [``[ImeIAVControlPar]``](#1-parameters-imeiavcontrolpar)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Keys [``[ImeIAVKeylistKey1]``](#2-keys-imeiavkeylistkey1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJAVKeylistKey1]``](#21-name-and-comment-by-locale-imeijavkeylistkey1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\- Values [``[ImeIAVValuelistVal]``](#3-values-imeiavvaluelistval)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Capability [``[ImeIMCapability]``](#4-capability-imeimcapability)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Parameters [``[ImeIAMCapabilityPar]``](#41-parameters-imeiamcapabilitypar)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Keys [``[ImeIAVKeylistKey2]``](#42-keys-imeiavkeylistkey2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name and comment by locale [``[ImeIJAVKeylistKey2]``](#421-name-and-comment-by-locale-imeijavkeylistkey2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Tag [``[ImeIMTag2]``](#43-tag-imeimtag2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Text by locale [``[ImeIJMTagTitle2]``](#431-text-by-locale-imeijmtagtitle2)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Concerned elements [``[ImeIRMCapabilityUniversal]``](#44-concerned-elements-imeirmcapabilityuniversal)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\- File [``[ImeIMFile]``](#5-file-imeimfile)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Library [``[ImeIMLibrary]``](#6-library-imeimlibrary)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Makefile entries [``[ImeIAMLibraryMakefile]``](#61-makefile-entries-imeiamlibrarymakefile)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Package lists [``[ImeIAMLibraryPkglist]``](#62-package-lists-imeiamlibrarypkglist)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Locale [``[ImeIMLocale]``](#7-locale-imeimlocale)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Name by locale [``[ImeIJMLocaleTitle]``](#71-name-by-locale-imeijmlocaletitle)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Machine [``[ImeIMMachine]``](#8-machine-imeimmachine)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Makefile entries [``[ImeIAMMachineMakefile]``](#81-makefile-entries-imeiammachinemakefile)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Parameters [``[ImeIAMMachinePar]``](#82-parameters-imeiammachinepar)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ Tag [``[ImeIMTag1]``](#9-tag-imeimtag1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Text by locale [``[ImeIJMTagTitle1]``](#91-text-by-locale-imeijmtagtitle1)
<br>&nbsp;&nbsp;&nbsp;&nbsp;\+ User group [``[ImeIMUsergroup]``](#10-user-group-imeimusergroup)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Feature access rights [``[ImeIAMUsergroupAccess]``](#101-feature-access-rights-imeiamusergroupaccess)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ User [``[ImeIMUser]``](#102-user-imeimuser)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Feature access rights [``[ImeIAMUserAccess]``](#1021-feature-access-rights-imeiamuseraccess)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- State history [``[ImeIJMUserState]``](#1022-state-history-imeijmuserstate)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\+ Person [``[ImeIMPerson]``](#1023-person-imeimperson)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Last name history [``[ImeIJMPersonLastname]``](#10231-last-name-history-imeijmpersonlastname)

[//]: # (IP structure - END)

Details
---

### 1 Parameters ``[ImeIAVControlPar]``

[//]: # (IP ImeIAVControlPar.superUse - BEGIN)

Use: manual customization e.g. of UI table column widths. Typically trained in a dedicated user session.

[//]: # (IP ImeIAVControlPar.superUse - END)

[//]: # (IP ImeIAVControlPar.columns - BEGIN)

Column|Content|
-|-|
srefIxWznmVControl (string)|control<br>PnlWznmUsgList.TcoGrp<br>...<br>PnlWznmSteATrig.TcoCnd|
Par (string)|parameter|
Val (string)|value|

[//]: # (IP ImeIAVControlPar.columns - END)

### 2 Keys ``[ImeIAVKeylistKey1]``

[//]: # (IP ImeIAVKeylistKey1.superUse - BEGIN)

Use: populate non-record specific key lists.

[//]: # (IP ImeIAVKeylistKey1.superUse - END)

[//]: # (IP ImeIAVKeylistKey1.columns - BEGIN)

Column|Content|
-|-|
srefKlsIxWznmVKeylist (string)|key list<br>KlstWznmKAMCapabilityParKey: key<br>KlstWznmKAMControlParKey: key<br>KlstWznmKAMControlParVal: value<br>KlstWznmKAMLibraryMakefileTag: tag<br>KlstWznmKAMMachineMakefileTag: tag<br>KlstWznmKAMMachineParKey: key<br>KlstWznmKAMPersonDetailType: type<br>KlstWznmKMControlOption: options<br>KlstWznmKMFileContent: content<br>KlstWznmKMFileMimetype: MIME type<br>KlstWznmKMLibraryLictype: license type<br>KlstWznmKMMachinePkgmgr: package manager<br>KlstWznmKMRelationOption: options<br>KlstWznmKMReleaseOption: options<br>KlstWznmKMTablecolOption: options<br>KlstWznmKMVectorOption: options<br>KlstWznmKRMCapabilityUniversalKey: key<br>KlstWznmKRMPersonMProjectFunction: function<br>KlstWznmKTaggrp: tag group<br>KlstKWznmCtpGenjtrCustop: WznmCtpGenjtr custom operations<br>KlstKWznmCtpGenuiCustop: WznmCtpGenui custom operations<br>KlstKWznmCtpWrsrvCustop: WznmCtpWrsrv custom operations<br>KlstKWznmCtpWrstkitCustop: WznmCtpWrstkit custom operations<br>KlstKWznmCtpWrwebCustop: WznmCtpWrweb custom operations|
sref (string)|identifier|
Avail (string)|availability rule|
Implied (string)|rule for implied|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIAVKeylistKey1.columns - END)

### 2.1 Name and comment by locale ``[ImeIJAVKeylistKey1]``

[//]: # (IP ImeIJAVKeylistKey1.superUse - BEGIN)

Super import: keys (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJAVKeylistKey1.superUse - END)

[//]: # (IP ImeIJAVKeylistKey1.columns - BEGIN)

Column|Content|
-|-|
srefX1IxWznmVLocale (string)|locale<br>enus: English (United States)|
Title (string)|Title|
Comment (string)|Comment|

[//]: # (IP ImeIJAVKeylistKey1.columns - END)

### 3 Values ``[ImeIAVValuelistVal]``

[//]: # (IP ImeIAVValuelistVal.superUse - BEGIN)

Use: populate value lists.

[//]: # (IP ImeIAVValuelistVal.superUse - END)

[//]: # (IP ImeIAVValuelistVal.columns - BEGIN)

Column|Content|
-|-|
srefVlsIxWznmVValuelist (string)|value list<br>VlstWznmUMPersonTitle: title|
srefX1IxWznmVLocale (string)|locale<br>enus: English (United States)|
Val (string)|value|

[//]: # (IP ImeIAVValuelistVal.columns - END)

### 4 Capability ``[ImeIMCapability]``

[//]: # (IP ImeIMCapability.superUse - BEGIN)

Use: specify capability templates.

[//]: # (IP ImeIMCapability.superUse - END)

[//]: # (IP ImeIMCapability.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
srefsIxWArtefact (string)|artefact<br>dbs: database structure<br>bui: basic user interface structure<br>iex: import/export structure<br>srvgblcode: server global code<br>srvjobcode: server job code<br>webgblcode: web UI global code<br>webjobcode: web UI job code|
Title (string)|name|

[//]: # (IP ImeIMCapability.columns - END)

### 4.1 Parameters ``[ImeIAMCapabilityPar]``

[//]: # (IP ImeIAMCapabilityPar.superUse - BEGIN)

Super import: capability (1:N)

Use: specify customization parameter default values.

[//]: # (IP ImeIAMCapabilityPar.superUse - END)

[//]: # (IP ImeIAMCapabilityPar.columns - BEGIN)

Column|Content|
-|-|
x1SrefKKey (string)|key|
Val (string)|value|

[//]: # (IP ImeIAMCapabilityPar.columns - END)

### 4.2 Keys ``[ImeIAVKeylistKey2]``

[//]: # (IP ImeIAVKeylistKey2.superUse - BEGIN)

Super import: capability (1:N)

Use: specify customization parameter keys.

[//]: # (IP ImeIAVKeylistKey2.superUse - END)

[//]: # (IP ImeIAVKeylistKey2.columns - BEGIN)

Column|Content|
-|-|
srefKlsIxWznmVKeylist (string)|key list<br>KlstWznmKAMCapabilityParKey: key|
sref (string)|identifier|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIAVKeylistKey2.columns - END)

### 4.2.1 Name and comment by locale ``[ImeIJAVKeylistKey2]``

[//]: # (IP ImeIJAVKeylistKey2.superUse - BEGIN)

Super import: keys (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJAVKeylistKey2.superUse - END)

[//]: # (IP ImeIJAVKeylistKey2.columns - BEGIN)

Column|Content|
-|-|
srefX1IxWznmVLocale (string)|locale<br>enus: English (United States)|
Title (string)|name|
Comment (string)|comment|

[//]: # (IP ImeIJAVKeylistKey2.columns - END)

### 4.3 Tag ``[ImeIMTag2]``

[//]: # (IP ImeIMTag2.superUse - BEGIN)

Super import: capability (1:N)

Use: specify capability-related (optional multi-locale) tags.

[//]: # (IP ImeIMTag2.superUse - END)

[//]: # (IP ImeIMTag2.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Title (string)|text|

[//]: # (IP ImeIMTag2.columns - END)

### 4.3.1 Text by locale ``[ImeIJMTagTitle2]``

[//]: # (IP ImeIJMTagTitle2.superUse - BEGIN)

Super import: tag (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMTagTitle2.superUse - END)

[//]: # (IP ImeIJMTagTitle2.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|text|

[//]: # (IP ImeIJMTagTitle2.columns - END)

### 4.4 Concerned elements ``[ImeIRMCapabilityUniversal]``

[//]: # (IP ImeIRMCapabilityUniversal.superUse - BEGIN)

Super import: capability (1:N)

Use: define expected elements to relate to in instantiations.

[//]: # (IP ImeIRMCapabilityUniversal.superUse - END)

[//]: # (IP ImeIRMCapabilityUniversal.columns - BEGIN)

Column|Content|
-|-|
srefUnvIxWznmVMaintable (string)|main table<br>TblWznmMBlock: block<br>TblWznmMCard: card<br>TblWznmMCheck: feature check<br>TblWznmMImpexp: import/export<br>TblWznmMImpexpcol: import/export column<br>TblWznmMImpexpcplx: import/export complex<br>TblWznmMJob: job<br>TblWznmMModule: module<br>TblWznmMPreset: presetting<br>TblWznmMRelation: relation<br>TblWznmMSquawk: squawk<br>TblWznmMStub: stub<br>TblWznmMSubset: subset<br>TblWznmMTable: table<br>TblWznmMTablecol: table column|
srefKKey (string)|key|

[//]: # (IP ImeIRMCapabilityUniversal.columns - END)

### 5 File ``[ImeIMFile]``

[//]: # (IP ImeIMFile.superUse - BEGIN)

Use: specify file meta-data for the files to be uploaded in the subsequent initialization step.

[//]: # (IP ImeIMFile.superUse - END)

[//]: # (IP ImeIMFile.columns - BEGIN)

Column|Content|
-|-|
osrefKContent (string)|content<br>appstr: accessor app structure data<br>cftpl: code file template<br>custip: custom insertion points<br>lic: license<br>mod: model data|
Filename (string)|file name|
srefKMimetype (string)|MIME type<br>bmp: image/bmp<br>...<br>zip: application/zip|
Comment (string)|comment|

[//]: # (IP ImeIMFile.columns - END)

### 6 Library ``[ImeIMLibrary]``

[//]: # (IP ImeIMLibrary.superUse - BEGIN)

Use: for Makefile generation, specify libraries and their dependencies.

[//]: # (IP ImeIMLibrary.superUse - END)

[//]: # (IP ImeIMLibrary.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Title (string)|name|
Version (string)|version|
srefKLictype (string)|license type<br>apch2: Apache 2.0<br>bsd2: BSD 2-clause<br>bsd3: BSD 3-clause<br>gpl: GNU general public<br>lgpl: GNU lesser general public<br>mit: MIT<br>zlib: zlib/libpng|
depSrefsWznmMLibrary (string)|library|
Comment (string)|comment|

[//]: # (IP ImeIMLibrary.columns - END)

### 6.1 Makefile entries ``[ImeIAMLibraryMakefile]``

[//]: # (IP ImeIAMLibraryMakefile.superUse - BEGIN)

Super import: library (1:N)

Use: specify library-specific Makefile entries.

[//]: # (IP ImeIAMLibraryMakefile.superUse - END)

[//]: # (IP ImeIAMLibraryMakefile.columns - BEGIN)

Column|Content|
-|-|
hsrefX1RefWznmMMachine (string)|machine|
x2SrefKTag (string)|tag<br>incpath: include path<br>libpath: library path<br>libs: link libraries|
Val (string)|value|

[//]: # (IP ImeIAMLibraryMakefile.columns - END)

### 6.2 Package lists ``[ImeIAMLibraryPkglist]``

[//]: # (IP ImeIAMLibraryPkglist.superUse - BEGIN)

Super import: library (1:N)

Use: specify package manager bundles required for library.

[//]: # (IP ImeIAMLibraryPkglist.superUse - END)

[//]: # (IP ImeIAMLibraryPkglist.columns - BEGIN)

Column|Content|
-|-|
hsrefX1RefWznmMMachine (string)|machine|
Pkglist (string)|package list|

[//]: # (IP ImeIAMLibraryPkglist.columns - END)

### 7 Locale ``[ImeIMLocale]``

[//]: # (IP ImeIMLocale.superUse - BEGIN)

Use: define locales.

[//]: # (IP ImeIMLocale.superUse - END)

[//]: # (IP ImeIMLocale.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Title (string)|name|

[//]: # (IP ImeIMLocale.columns - END)

### 7.1 Name by locale ``[ImeIJMLocaleTitle]``

[//]: # (IP ImeIJMLocaleTitle.superUse - BEGIN)

Super import: locale (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMLocaleTitle.superUse - END)

[//]: # (IP ImeIJMLocaleTitle.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|name|

[//]: # (IP ImeIJMLocaleTitle.columns - END)

### 8 Machine ``[ImeIMMachine]``

[//]: # (IP ImeIMMachine.superUse - BEGIN)

Use: define (cross-)compilation and deploy targets with hierarchical attribute inheritance.

[//]: # (IP ImeIMMachine.superUse - END)

[//]: # (IP ImeIMMachine.columns - BEGIN)

Column|Content|
-|-|
hsrefSupRefWznmMMachine (string)|base machine|
sref (string)|identifier|
hsrefCchRefWznmMMachine (string)|cross-compile host|
srefKPkgmgr (string)|package manager<br>apt: advanced package manager<br>bb: BitBake<br>brew: Homebrew<br>yum: yum|
Comment (string)|comment|

[//]: # (IP ImeIMMachine.columns - END)

### 8.1 Makefile entries ``[ImeIAMMachineMakefile]``

[//]: # (IP ImeIAMMachineMakefile.superUse - BEGIN)

Super import: machine (1:N)

Use: specify machine-specific Makefile entries.

[//]: # (IP ImeIAMMachineMakefile.superUse - END)

[//]: # (IP ImeIAMMachineMakefile.columns - BEGIN)

Column|Content|
-|-|
x1SrefKTag (string)|tag<br>cpp: C++ compiler<br>cppflags: C++ compiler flags<br>statlib: static library tool<br>statlibflags: static library tool flags<br>dynlib: dynamic link library tool<br>dynlibflags: dynamic link library tool flags<br>dynlibext: dynamic link library file extension<br>link: linker<br>linkflags: linker flags<br>incpath: include path<br>libpath: library path<br>libs: link libraries|
Val (string)|value|

[//]: # (IP ImeIAMMachineMakefile.columns - END)

### 8.2 Parameters ``[ImeIAMMachinePar]``

[//]: # (IP ImeIAMMachinePar.superUse - BEGIN)

Super import: machine (1:N)

Use: specify machine-specific parameters, mostly paths.

[//]: # (IP ImeIAMMachinePar.superUse - END)

[//]: # (IP ImeIAMMachinePar.columns - BEGIN)

Column|Content|
-|-|
x1SrefKKey (string)|key<br>whizroot: runtime root directory<br>acvroot: archive root directory<br>binroot: binary root directory<br>monroot: monitoring root directory<br>tmproot: temporary data root directory<br>webroot: web server root directory<br>opengsrvport: default operation engine server port<br>engsrvportbase: default enginer server port base<br>appsrvport: default application server port<br>dbsip: database IP address<br>dbsusername: database user name<br>dbspassword: database password<br>marport: MariaDB server port<br>myport: MySQL server port<br>pgport: PostgreSQL server port<br>whizsdkroot: SDK root directory<br>ncore: number of cores, also for runtime<br>sbeconfig: WhizniumSBE core library configuration<br>buildroot: build root directory<br>libroot: library root directory<br>nddshome: DDS home directory<br>sysroot: root file system path<br>tchroot: tool chain executable directory<br>uasdkroot: OPC UA SDK root directory<br>whizdevroot: development root directory<br>reproot: repository root directory<br>fpgaroot: FPGA root directory<br>javaroot: Java root directory<br>mcuroot: MCU root directory|
Val (string)|value|

[//]: # (IP ImeIAMMachinePar.columns - END)

### 9 Tag ``[ImeIMTag1]``

[//]: # (IP ImeIMTag1.superUse - BEGIN)

Use: specify locale-specific tags used across UI and other code generation.

[//]: # (IP ImeIMTag1.superUse - END)

[//]: # (IP ImeIMTag1.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
osrefWznmKTaggrp (string)|group<br>access: VecXxxxWAccess item<br>adrtype: address type<br>ctdet: contact detail<br>ctry: country<br>error: VecXxxxVError item<br>expstate: VecXxxxVExpstate item<br>iexsge: import/export complex job stage<br>iop: VecXxxxVIop item<br>lat: VecXxxxVLat item<br>lop: VecXxxxVLop item<br>mimetype: MIME type<br>no: no thing<br>none: none<br>oolop: VecXxxxVOolop item<br>prs: default person<br>prstit: person title<br>qrystate: VecXxxxVQrystate item<br>recaccess: VecXxxxVRecaccess item<br>reqitmode: VecXxxxVReqitmode item<br>sex: sex<br>start: login card<br>stdalr: standard alert message<br>stdiex: standard import/export complex title<br>stdrel: standard relation title<br>stdtbl: standard table title<br>stdtco: standard table column title<br>stdvec: standard vector title<br>userlevel: VecXxxxVUserlevel item<br>usrste: user state<br>wkday: weekday|
Title (string)|text|

[//]: # (IP ImeIMTag1.columns - END)

### 9.1 Text by locale ``[ImeIJMTagTitle1]``

[//]: # (IP ImeIJMTagTitle1.superUse - BEGIN)

Super import: tag (1:N)

Use: self-explanatory.

[//]: # (IP ImeIJMTagTitle1.superUse - END)

[//]: # (IP ImeIJMTagTitle1.columns - BEGIN)

Column|Content|
-|-|
srefX1RefWznmMLocale (string)|locale|
Title (string)|Title|

[//]: # (IP ImeIJMTagTitle1.columns - END)

### 10 User group ``[ImeIMUsergroup]``

[//]: # (IP ImeIMUsergroup.superUse - BEGIN)

Use: self-explanatory.

[//]: # (IP ImeIMUsergroup.superUse - END)

[//]: # (IP ImeIMUsergroup.columns - BEGIN)

Column|Content|
-|-|
sref (string)|identifier|
Comment (string)|comment|

[//]: # (IP ImeIMUsergroup.columns - END)

### 10.1 Feature access rights ``[ImeIAMUsergroupAccess]``

[//]: # (IP ImeIAMUsergroupAccess.superUse - BEGIN)

Super import: user group (1:N)

Use: define access rights to individual parts of the WhizniumSBE UI.

[//]: # (IP ImeIAMUsergroupAccess.superUse - END)

[//]: # (IP ImeIAMUsergroupAccess.columns - BEGIN)

Column|Content|
-|-|
srefX1IxWznmVFeatgroup (string)|feature group<br>VecWznmVCard: card|
x2FeaSrefUix (string)|feature|
srefsIxWznmWAccess (string)|feature access rights<br>edit: edit<br>exec: execute<br>view: view|

[//]: # (IP ImeIAMUsergroupAccess.columns - END)

### 10.2 User ``[ImeIMUser]``

[//]: # (IP ImeIMUser.superUse - BEGIN)

Super import: user group (1:N)

Use: specify users with login and password.

[//]: # (IP ImeIMUser.superUse - END)

[//]: # (IP ImeIMUser.columns - BEGIN)

Column|Content|
-|-|
sref (string)|login|
srefIxVState (string)|state<br>act: active<br>dsg: designated<br>due: due for expiration<br>exp: expired|
srefIxWznmVLocale (string)|locale<br>enus: English (United States)|
srefIxWznmVUserlevel (string)|user level<br>adm: administrator<br>gadm: user group administrator<br>reg: regular user<br>vtor: visitor|
Password (string)|password|
Fullkey (string)|full key (X.509)|
Comment (string)|comment|

[//]: # (IP ImeIMUser.columns - END)

### 10.2.1 Feature access rights ``[ImeIAMUserAccess]``

[//]: # (IP ImeIAMUserAccess.superUse - BEGIN)

Super import: user (1:N)

Use: define WhizniumSBE UI access rights, potentially overriding those of the user's user group.

[//]: # (IP ImeIAMUserAccess.superUse - END)

[//]: # (IP ImeIAMUserAccess.columns - BEGIN)

Column|Content|
-|-|
srefX1IxWznmVFeatgroup (string)|feature group<br>VecWznmVCard: card|
x2FeaSrefUix (string)|feature|
srefsIxWznmWAccess (string)|feature access rights<br>edit: edit<br>exec: execute<br>view: view|

[//]: # (IP ImeIAMUserAccess.columns - END)

### 10.2.2 State history ``[ImeIJMUserState]``

[//]: # (IP ImeIJMUserState.superUse - BEGIN)

Super import: user (1:N)

Use: manage time-dependency of user access permission.

[//]: # (IP ImeIJMUserState.superUse - END)

[//]: # (IP ImeIJMUserState.columns - BEGIN)

Column|Content|
-|-|
srefIxVState (string)|state<br>act: active<br>dsg: designated<br>due: due for expiration<br>exp: expired|

[//]: # (IP ImeIJMUserState.columns - END)

### 10.2.3 Person ``[ImeIMPerson]``

[//]: # (IP ImeIMPerson.superUse - BEGIN)

Super import: user (1:N)

Use: exclusively used as 1:1 with user. Provide user clear name information.

[//]: # (IP ImeIMPerson.superUse - END)

[//]: # (IP ImeIMPerson.columns - BEGIN)

Column|Content|
-|-|
srefIxVSex (string)|sex<br>f: female<br>m: male|
Title (string)|title<br>dr: Dr.<br>drlong: Doctor<br>fam: Fam.<br>famlong: Family<br>mr: Mr.<br>mrlong: Mister<br>mrs: Mrs.<br>mrslong: Mistress<br>ms: Ms.<br>mslong: Miss<br>prof: Prof.<br>proflong: Professor|
Firstname (string)|first name|
Lastname (string)|last name|

[//]: # (IP ImeIMPerson.columns - END)

### 10.2.3.1 Last name history ``[ImeIJMPersonLastname]``

[//]: # (IP ImeIJMPersonLastname.superUse - BEGIN)

Super import: person (1:N)

Use: allow a person's last name to change with time.

[//]: # (IP ImeIJMPersonLastname.superUse - END)

[//]: # (IP ImeIJMPersonLastname.columns - BEGIN)

Column|Content|
-|-|
Lastname (string)|last name|

[//]: # (IP ImeIJMPersonLastname.columns - END)

<small>Markdown for WhizniumSBE v1.1.3 auto-generated (what else ;-) ) by WhizniumSBE on 1 Jan 2021</small>
