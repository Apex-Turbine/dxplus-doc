# Data Formats

> [!IMPORTANT]
> **End-User Format License Notice:** All APEX-provided file formats, database schemas, and streaming protocols are licensed strictly for internal end-user use with authorized APEX software and cannot be used for commercial means without explicit formal written authorization from APEX. See the **[Software License Agreement](../../Release%20Policies/software-license-agreement.md)**. & Storage Architecture

**APEX DX+** supports open relational databases for fast indexed queries, sharded multi-file archives for high-throughput multi-rate recording, binary telemetry containers for compatibility with legacy and third-party tools, and JSON-based design/setup project files.

---

## Format Summary

| Extension / Store | Type | Read Support | Write Support | Primary Applications |
| :--- | :--- | :--- | :--- | :--- |
| **`.dxdb`** / **`.dxdb.index`** | SQLite Database (single file or sharded index) | Yes | Yes | DX+ DAQ, Online/Offline Analysis, Data Viewer, DB Manager |
| **PostgreSQL** | Enterprise Relational / Timescale-compatible DBMS | Yes | Yes | DX+ Online/Offline Analysis, Data Viewer, DB Manager |
| **`.h5`** (`APEX-H5`) | Hierarchical Data Format 5 container | Yes | Yes | DX+ Online/Offline Analysis, Data Viewer |
| **`.datx`** / **`.datx_index`** | Dewesoft / DSPCon binary container & multi-file index | Yes | Yes | DX+ Online/Offline Analysis, Data Viewer, DB Manager |
| **`.rwx`** | APEX DSAPI raw block-compressed waveform binary | Yes | Yes | DX+ DAQ (replay), Online/Offline Analysis, Data Viewer, DB Manager |
| **`.pkx`** | APEX DSAPI legacy peak binary container | Yes | — | DX+ Data Viewer (via DSAPI reader) |
| **`.dxt`** | DX+ DAQ Tabular Setup file (JSON, `"mode": "table"`) | Yes | Yes | DX+ DAQ |
| **`.dpd`** *(or `.json`)* | DX+ Analysis Graphic Design graph project (JSON) | Yes | Yes | DX+ Online Analysis, DX+ Offline Analysis, `DX+OfflineQueryCli` |
| **`.csv`** | Strict Columnar Time-Series CSV export / Freq Limits | Yes (Limits) | Yes (Export) | DX+ DB Manager (Export), DX+ DAQ / Analysis (Freq Limits) |

---

## 1. SQLite (`.dxdb` / `.dxdb.index`) & PostgreSQL Schema

Both SQLite and PostgreSQL storage drivers share the standard **APEX Phoenix Database Schema**. All timestamps across tables and messages are stored as **64-bit unsigned/signed integers in nanoseconds since Unix epoch (UTC)**.

### Core Tables

| Table | Purpose | Key Columns |
| :--- | :--- | :--- |
| **`DS_INDEX`** | Master recording session registry (1 row per Record / `ds_id`) | `ds_id`, `api_version`, `create_time`, `complete_time`, `graph_json`, `tables_json`, `metadata` |
| **`APEX_DATA`** | Time-series vectors, spectra, and message payloads | `ds_id`, `source_index`, `stream_index`, `starttime`, `endtime`, `delta`, `typecode`, `header`, `data` |
| **`APEX_DATAPOINT`** | Discrete recorded **Event** windows *(physical table name preserved for `.dxdb` compatibility)* | `ds_id`, `starttime`, `endtime`, `event_number`, `event_flags`, `info` |
| **`APEX_ERROR`** | Timestamped runtime error records emitted by sources/processors | `ds_id`, `source_index`, `stream_index`, `timestamp`, `message`, `error_level`, `error_loc` |
| **`APEX_LOG`** | Informational and diagnostic log entries | `ds_id`, `source_index`, `stream_index`, `timestamp`, `message` |
| **`APEX_MODEL_DATA`** | Serialized 3D model / modal analysis payloads | `ds_id`, `source_index`, `stream_index`, `starttime`, `endtime`, `data` |

### Sharded Archives (`.dxdb.index`) & Partitioning

When high-throughput DAQ setups enable file splitting (**Time**, **Size**, or **Event**) or partitioning (**None**, **Sources**, **Streams**):

- Data partitions are written into linked SQLite shard files referenced through `tables_json` (`parts[].location` and optional `parts[].recordNumber`).
- Opening the master **`.dxdb.index`** file in [DX+ Data Viewer](../DX+Viewer/DX+DataViewer/README.md), [DX+ Offline Analysis](../DX+OfflineAnalysis/README.md), or [DX+ DB Manager](../Tools/DB%20Manager/README.md) automatically resolves, attaches, and unions all external shard tables transparently.

> [!NOTE]
> **All Data vs. Events-Only Recording (`eventmode`)**: When **All Data** is checked in DAQ or Online Store settings (`eventmode = false` in JSON), configured streams write continuously while **RECORDING** is active. Disabling **All Data** (`eventmode = true`) or enabling **Event-based file splitting** restricts database writes strictly to active **EVENT REC** intervals.

---

## 2. Binary File Formats (`.h5`, `.datx`, `.rwx`, `.pkx`)

### APEX HDF5 (`.h5`)

- Written and read via **APEX-H5 Output** (`HDF5Output`) and **APEX-H5 Input** (`HDF5Input`) components with configurable **Write Interval (`commit_time`)** and **Event Mode** (`only_data_points` when reading).
- **Performance Advisory**: Multi-channel playback directly from `.h5` files in DX+ Viewer can incur higher latency when many plots are open simultaneously. For interactive multi-plot playback and post-test querying, **SQLite (`.dxdb`)** or **PostgreSQL** is recommended.

### DATX & Multi-Part Index (`.datx` / `.datx_index`)

- Native reader and writer supporting Dewesoft / DSPCon DATX binary files and `.datx_index` grouped file sets (with test keyword headers, events `event_NNNN`, IRIG timestamps, and channel mappings).
- Supports **File Parts** partitioning (**`Single File`**, **`Sample Rate`**, or **`Channels`**) and rollover **Split Conditions** (**`None`**, **`Time`**, **`Size`**, **`Event`**).
- **Rate Constraint**: All streams written into a single `.datx` file must share the **same sample rate** (use `Sample Rate` or `Channels` partitioning when exporting mixed-rate records).

### APEX RWX & PKX (`.rwx` / `.pkx`)

- Legacy/native APEX block-compressed binary waveform (`.rwx`) and peak (`.pkx`) formats accessed via **DSAPI** and `RWXReader`/`RWXWriter`.
- `.rwx` files support playback at real-time or accelerated speeds (`1x`, `10x`, `100x`, `1000x`, `Max`) with optional looping, as well as multi-part export via `DX+ DB Manager` or `RWX File Writer`.
- **Rate Constraint**: Streams combined into a single `.rwx` file must share the same sample rate or have sample rates differing by an exact power of 2.

---

## 3. Configuration & Export Formats (`.dxt`, `.dpd`, `.csv`)

- **`.dxt` (DAQ Tabular Setup)**: JSON setup file (`"mode": "table"`) created and opened exclusively by [DX+ DAQ](../DX+DAQ/README.md). Auto-named `DXP<YYYYMMDD>.dxt` when unsaved. Cannot be opened in DX+ Online/Offline Analysis, and `.dpd` graphs cannot be loaded into DX+ DAQ.
- **`.dpd` / `.json` (Analysis Design Graph)**: Complete Phoenix node-graph topology (`sources`, `connections`, `settings`, `units`, limits) saved and loaded by [DX+ Online Analysis](../DX+OnlineAnalysis/README.md), [DX+ Offline Analysis](../DX+OfflineAnalysis/README.md), and the headless [`DX+OfflineQueryCli`](../DX+OfflineAnalysis/offline-query-cli.md) runner.
- **Strict Columnar CSV (`.csv`)**: Exported by [DX+ DB Manager](../Tools/DB%20Manager/README.md#4-exporting-to-strict-columnar-csv) with selectable primary time columns (`timestamp_irig` default, `timestamp_utc`, or `timestamp_ns`), multi-rate sample-and-hold synchronization or binned downsampled statistics (`Average`, `Min`, `Max`, `Peak-to-Peak`, `RMS`), and `"Source.Stream"` headers. Also used by [DX+ DAQ Freq Limits](../DX+DAQ/general/ribbon.md#freq-limits) CSV limit tables.
