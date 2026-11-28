# Loading Data Stores & Playback

**DX+ Data Viewer** connects to recorded telemetry sources dynamically via registered File and Database adapters in **File → Connect**.

---

## Supported File & Database Sources

### Database Adapters (`File → Connect`)

- **`DXDBReader` *(SQLite / `.dxdb` / `.dxdb.index`)***: Opens single `.dxdb` / `.sqlite` recordings or multi-part sharded **`.dxdb.index`** archives seamlessly.
- **`PostgreSQL` Reader**: Connects to centralized enterprise PostgreSQL telemetry databases via server URI/credentials.

### File Adapters (`File → Connect`)

- **`RwxReader` *(APEX `.rwx` / `.pkx`)***: Opens native APEX block-compressed waveform (`.rwx`) and peak (`.pkx`) recordings.
- **`DatxReader` *(Dewesoft / DSPCon `.datx` / `.datx_index`)***: Opens individual `.datx` files or multi-file `.datx_index` grouped test archives.
- **`APEX-H5` *(HDF5 `.h5`)***: Opens APEX HDF5 telemetry recordings.

> [!NOTE]
> **HDF5 Performance Recommendation:** Because `.h5` files do not share SQLite's indexed relational query tables, opening many simultaneous plots from an `.h5` file can slow playback. When possible, record to or convert datasets into **SQLite (`.dxdb`)** or **PostgreSQL** for responsive multi-plot inspection.

---

## Opening a Data Source Step-by-Step

1. Launch **Start → APEX DX+ → DX+ Data Viewer**.
2. Click **File → Connect** and choose the reader adapter matching your file or database.
3. In the **Open Data Store** dialog:
   - Enter the file path or database connection **URI**, or click **`...`** to browse local storage.
   - For PostgreSQL connections, enter host, port (`5432`), username, password, and database name.
4. For databases, configure optional **Data Store Options**:
   - **Load Events**: Loads discrete recorded event intervals (`APEX_DATAPOINT`) and metadata into the Viewer tree and Event Filter dialog (`PhoenixQueryDialog`).
   - **Query Data Store**: Restricts initial loading to a specific **Start** and **End** timestamp range (stored internally in nanosecond Unix epoch UTC).
5. Click **Open**. Loaded records, events, sources, and streams populate the left **Signal Tree**.
6. Repeat **File → Connect** to overlay channels from multiple files or databases on the same page.

### Managing Open Stores

- **`File → Recent Stores`**: Reopen recently inspected files and databases directly.
- **`File → Close`**: Select an active source handle to clear its pages cleanly, stop reader cursors, and release file locks.

---

## Playback, Seek & Time Sync

- **Playback Controls & Slider**: Play forward at real-time or stepped rates, pause, single-step, or drag the playback slider to jump across the recording timeline. Forward micro-steps reuse prefetched row/file spans without redundant reads, while rewinding or jumping outside the active window seeks cleanly.
- **Time Sync (`Plots → Plot Tools → Time Sync`)**: Synchronizes playback timestamps across multiple time-domain charts, spectrograms, and optional synchronized video plots on the active page.
- **Troubleshooting Slow Playback**: Closing unused plots or switching high-density history displays to appropriate window durations improves playback fluidity across large multi-channel recordings.
