# DX+ DAQ

**DX+ Data Acquisition** (DX+ DAQ) sets up devices, configures per-stream processing in a table, and records, views, and transmits the data. Open it from **Start → APEX DX+ → DX+ Data Acquisition**.

A typical session:

1. [Add a device](devices/README.md) with **Add Device** in the [Ribbon](general/ribbon.md).
2. Name the streams and set their processing in the [table](general/table-operations.md): [Range Limits](general/table-operations.md#range-limits), [Raw Units](processors/raw-units.md), [Filtering](processors/filtering.md), [Conversion](processors/conversion.md), [Spectral](processors/spectral.md), and [Statistics](processors/statistics.md).
3. Choose where the data goes in the [Outputs](outputs/README.md) pane: [Viewer](outputs/viewer.md), [Store](outputs/sqlite.md), and [Transmit](outputs/transmit.md).
4. Click **Submit Setup**, then start acquiring.
5. Save the setup as a `.dxt` file to reuse it later.
