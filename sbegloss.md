[back](./README.md)

# WhizniumSBE glossary

Expressions and abbreviations which are commonly used in WhizniumSBE models and WhizniumSBE-generated code.

expression|context|description|
---|---|---|
API|API library, accessor app|application programming interface mostly consisting of block (de-)serializers|
application server|engine|HTTP(S) 1.1 compliant web-server / thread as part of the engine; implemented with libmicrohttpd|
block|engine, operation engine, clients, accessor app|(de-)serializable (to/from XML) object used e.g. for preferences and communication|
call|engine|notifications allowing to communicate events inter-job as well as from jobs to stub managers and to the M2M handler threads. Brokerage of triggering and listening calls is handled by the engine's exchange object|
capability|engine|user-extensible functionality to be re-used across projects using a parametrized template, and optionally dedicated code generation at various stages|
card|engine, HMI client|each card is displayed in one browser tab - when database-backed representing a main table or subset, else user-defined|
claim|engine|means to gain exclusive controlling access to a client/server job or parts of its functionality|
client/server job|engine|special type of job, mainly for hardware control, which allows one server "acting" instance and multiple client instances at any given time|
cluster sequence|database|enumerated but unnamed group allowing to bundle records in related tables|
combined engine|engine|one common executable for engine and operation engine functionality|
command|engine|job command line command - as opposed to a job method accessible in M2M communication|
component|project configuration|the components which can be generated for a WhizniumSBE project include database access library, engine, operation engine, combined engine, web-based UI, API library and Java API library|
control|HMI client|smallest HMI feature allowing to view/manipulate one block item|
control complex|HMI client|recognized pattern of control and sub-controls, resulting in a dedicated look-and-feel in the web-based UI|
DDS|engine, M2M client|data distribution service, M2M communication protocol; optional engine thread powered by RTI(R) Connext(TM) DDS software|
dialog|engine, HMI client|optionally wizard-style sub-element to card, typically to manage a complex action / workflow - as opposed to simple view and control functionality handled in panels|
dispatch|engine, operation engine, clients, accessor app|XML message, optionally container for multiple blocks|
dispatch collector|engine|storage container per session or per card which keeps unsent engine-to-app dispatches while there is no request from the app. Updates of dispatch content handled by the engine's exchange object|
DOM|accessor app|document object model; storage element for session state information in analogy to a web-browser's DOM|
engine|engine|main executable responsible for performing all actions in multi-threaded fashion. Manages client sessions and interactions (operation distribution/colleciton) with operation engines|
engine server|operation engine|in this thread, the operation engine listens to invocation dispatches from the engine; implemented with libmicrohttpd|
error|engine|project-specific extension of the SbeException class allowing for localized error messages including string variable placeholders|
exchange object|engine, operation engine|object maintaining and brokering information about the job tree (engine); object maintaining and brokering information about all running operations (operation engine)|
external call|engine|used to feed a call into the job tree from an external source such as a library callback function|
feature check|database, engine|"question to a record": using the WhizniumSBE expression language, the content of individual table fields can be queried (true/false answer). This is e.g. used to conditionally show/hide sub-panels on database-backed cards|
feed|engine, HMI client, accessor app|array data source to e.g. pop-up / list controls containing numeric and string references along with names|
HMI|HMI client|human-machine-interface, as opposed to machine-to-machine-interface, another expression for the web-based UI|
HMI session|engine, HMI client|client session that uses cards, dialogs and panels to interact with the engine|
import/export complex|engine|definition for importing/exporting information to / from a set of tables, conserving the relational dependencies between tables; XML and text-based are supported|
insertion point|engine, operation engine, HMI client, accessor app|comment in source code, short form IP, indicating a spot into which code can be inserted manually|
iteration|project configuration|the process of letting WhizniumSBE generate a new version based on the previous version's source code tree and updated model files|
ix...|database, engine, operation engine|index referring to a vector, e.g. ixXyzaVLocale is the variable used to refer to the vector VecXyzaVLocale|
job|engine|jobs are classes within the engine which are responsible for specific functionality. At run-time, there is one root job object, one session job per session, HMI jobs for each card/panel/dialog/query currently active; user-defined jobs with arbitrary functionality are also possible|
job processor|engine|thread waiting for requests for actions to be performed using the job objects. The number of job processors is set in the preferences file to match the host machine's capabilities|
job tree|engine|the hierarchical arrangement of super jobs and sub-jobs at run-time; super jobs #include their sub-jobs in code|
jump table|database|table allowing to conditionally overwrite table fields in their super table|
\<Job>_blks.cpp|engine|source code file containing the implementation of a job's blocks; separated from the main implementation file for clarity - no manual IP's here|
\<Job>_evals.cpp|engine|source code file containing the implementation of a job's expression evaluation statements (typ. control available/active); separated from the main implementation file for clarity - no manual IP's here|
key list|engine|database-backed, run-time extensible list of identifiers with localized names and comments|
list functionality|database|helper table(s) or table column(s) allowing to perform conditional e.g. insert/remove/shuffle record operations on a super table (query-mode only)|
load function|database|SQL SELECT query with fixed parameters resulting in dedicated prepared statement and C++ method|
locale|database, engine, HMI client|language specification|
M2M session|engine, M2M client|client session (currently DDS or OPC UA) by a machine using direct access to job variables and methods|
machine|project configuration|computer or deployment target with common e.g. compiler flags and library paths; hierarchical structure with parameter inheritance|
main table|database|relevant table, the entries of which make sense without other tables - and which warrant a dedicated card|
method|engine, M2M client|job method - as opposed to a job command line command|
module|HMI client|grouping entity for cards|
node|engine|successfully connected operation engine|
OPC UA|engine, M2M client|OPC Unified Architecture, M2M communication protocol for industrial automation; optional engine thread powered by Matrikon(R) OPC UA FLEX SDK|
operation|engine, operation engine|atomic remote procedure which is executed in the operation engine upon invocation from the engine|
operation engine|operation engine|satellite executable responsible for running operations at the request of the engine|
operation engine client|engine|thread to transfer operation invocation/return dispatches to/from connected nodes; implemented with libcurl|
operation engine server|engine|this thread waits for connections by operation engines; implemented with libmicrohttpd|
operation pack|project configuration, engine, operation engine|grouping entity for operations of related functionality; in a project, operation engine components can be defined comprising a subset of operation packs|
operation processor|engine, operation engine|thread waiting for invocation dispatches for remote procedures to be performed using the operation "run" methods. The number of operation processors is set in the preferences file to match the host machine's capabilities|
panel|engine, HMI client|sub-elements to cards for view and control functionality|
presetting|engine|variables of basic data typrs which can be set/reset and attached to jobs. They can be queried up the job structure, allowing to set a context for entire branches of the job tree|
project|project configuration|topmost entity for a WhizniumSBE project - a project has multiple versions|
query|database, engine|sourced from possibly multiple tables, a query represents a meaningful view to database data; composed within the database by means of INSERT INTO / SELECT SQL queries where possible|
query modifier|database, engine|conditional filter for query|
ref...|database, engine, operation engine|reference to a table record, e.g. refXyzaMUser is the variable used to refer to the table TblXyzaMUser|
release|project configuration|results in a makefile/initialization file set for a compnent, specific to a machine|
result|engine|C++ data structure intended for copy-free sharing of job results. The included result items can be locked by other jobs while they are processing their data|
run-time job/block/dispatch|accessor app|ingredients to an accessor app's DOM|
sensitivity|engine|feature attached to a job or a stage within, specifying to which events it reacts, e.g. to calls with fine-grained masking options|
sequence|accessor app|grouping entity for accessor app states|
squawk|engine, operation engine|localized message visible to a HMI user hinting to a job's state, or to an operation's activity; typically parametrized, e.g. with a stub|
sref...|database, engine, operation engine|identifier (string reference) to a key list key or to a table record, e.g. TblXyzaMFile.srefKMimetype is the variable used to refer to the key list KlstXyzaKMFileMimetype|
stage|engine|state within a job's state machine - as opposed to a accessor app state|
state|accessor app|state within the state machine of an accessor app - as opposed to a job stage|
stub|engine|human-readable representaion of a table record. Can include stubs of referred tables, optionally localized|
stub manager|engine|data structure which serves as a cache for stubs in order to avoid excessive database requests. Managed by the engine's exchange object, including the protrusion of updates|
subset|database|subset of a table for records fulfilling a simple SQL WHERE condition|
\<Database>/\<Table>_vecs.cpp|database|source code file containing the implementation of a table's vectors; separated from the main implementation file for clarity|
tag|HMI client|localized control caption; on top of project-specific user-defined tags, WhizniumSBE maintains a list of 100's of tags as simple as "yes"/"no" to generate the basic HMI fabric|
Title|database, HMI client|human-readable name of a record, typically not indexed - as opposed to sref's which may serve as a searchable table record's identifier|
universal reference|database|used to establish a polymorphic relation between database tables; identification by helper vector|
value list|engine|database-backed, run-time extensible list of localized names|
variable|engine, M2M client|job variable accessible in M2M communication|
vector|database, engine, operation engine|enumerated non-extensible list of identifiers with localized names and comments; can be standalone, attached to a table or to a job. The corresponding (numerical) table columns are typically indexed, allowing for fast WHERE filtering in SELECT queries|
version|project configuration|technically the topmost entity when working with WhizniumSBE, as each version comprises the full project model definition|
wakeup|engine|avoids calling sleep() for a wait period which would block the calling job processor thread. Wakeup's with zero wait period are used to switch threads, e.g. when a long-duration action is triggered by a click in the HMI. Handled by the engine's exchange object|
