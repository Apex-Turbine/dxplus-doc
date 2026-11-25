# APEX DX+ Quick Start Guide

> [!NOTE]
> Confirm your workstation meets **[System Requirements](../Release%20Policies/system-requirements.md)** (`x86-64` with **AVX2**) and has an active entitlement in **[APEX License Manager](../License%20Manager/README.md)** ([Quick Start](../License%20Manager/quick-start.md)). Legacy FlexNet (`lmgrd`) licensing ends in **October 2027**.

This guide walks through verifying **APEX License Manager (ApexLM)**, configuring a live **DX+ DAQ** acquisition run, viewing live telemetry in **DX+ Remote Viewer**, running **DX+ Online / Offline Analysis** designs, and inspecting saved runs in **DX+ Data Viewer**.

---

## Step 1: Install & Verify Licensing

1. Run the DX+ installer for Windows or Linux ([System Requirements](introduction/system-requirements.md)).
2. Open the local **APEX License Manager** Web UI at `http://127.0.0.1:27887/` and confirm active seats for `DXPLUS`, `DX+DAQ`, `DX+ONLINEANALYSIS`, `DX+OFFLINEANALYSIS`, `DX+REMOTEVIEWER`, and `DX+DATAVIEWER` ([Installation & Licensing](introduction/installing-and-licensing.md)).

---

## Step 2: Acquire & Record Live Data (`DX+ DAQ`)

1. Launch **DX+ DAQ** ([DX+ DAQ Guide](DX+DAQ/README.md)).
2. Open the **Devices** panel and add a physical hardware device (`Mecalc`, `Scanivalve`, `VTI`, `Datatel`, `NI`, `Pacific`, `HGL`, etc.) or select a **Simulator / Virtual Device** for testing ([Devices Reference](DX+DAQ/devices/README.md)).
3. Configure channel calibration, EU scaling, filtering, FFT, and peak extraction directly in the tabular setup grid ([Table Operations](DX+DAQ/general/table-operations.md)).
4. Enable outputs under **Outputs**:
   - **SQLite / PostgreSQL Store** for `.dxdb` persistent recording ([SQLite Output](DX+DAQ/outputs/sqlite.md)).
   - **DXNet Transmit** (`27026` / ZeroMQ) for live network streaming ([Transmit Output](DX+DAQ/outputs/transmit.md)).
5. Click **Submit** on the ribbon to start streaming and **Record** when ready to capture test data.
   - Hardware-specific walkthroughs: [Datatel Quick Start](introduction/quick-start-datatel.md) · [VTI Quick Start](introduction/quick-start-vti.md).

---

## Step 3: Monitor Live Streams (`DX+ Remote Viewer`)

1. Launch **DX+ Remote Viewer** (or **DXNet-Rx**) ([DX+ Remote Viewer Guide](DX+RemoteViewer/README.md)).
2. Select a discovered `_dxnet._tcp.local` mDNS stream (or enter `<host>:27026`) ([Connecting & Streams](DX+RemoteViewer/connecting-and-streams.md)).
3. Drag signals onto a plot grid to build real-time Scope, FFT, Campbell, Waterfall, Gauge, or Bar displays and track scope limits ([Live Plots](DX+RemoteViewer/live-plots.md)).

---

## Step 4: Build Streaming or Post-Test Pipelines

- **Real-Time Pipelines (`DX+ Online Analysis`)**: Connect live `DX+ Receive`, PLC/OPC-UA bridges, and `Simulator` inputs to DSP processors, triggers, solution fits, and database/stream sinks in a `.dpd` node graph, then click **Submit Design** ([Online Analysis Guide](DX+OnlineAnalysis/README.md)).
- **Post-Test & Batch Analysis (`DX+ Offline Analysis`)**: Attach recorded `.dxdb`, `.h5`, `.rwx`, or `.datx` sources via `Stream Select`, resolve matched test records, and execute interactive or headless CLI batch pipelines ([Offline Analysis Guide](DX+OfflineAnalysis/README.md) · [`DX+OfflineQueryCli`](DX+OfflineAnalysis/offline-query-cli.md)).

---

## Step 5: Inspect & Export Results (`DX+ Data Viewer` & `DB Manager`)

1. Open saved `.dxdb`, `.h5`, `.datx`, `.rwx`, `.pkx`, or PostgreSQL runs in **[DX+ Data Viewer](DX+DataViewer/README.md)** to build synchronized time and frequency plots ([Loading & Playback](DX+DataViewer/loading-and-playback.md)).
2. Use **[DX+ DB Manager](Tools/DB%20Manager/README.md)** (`dx+dbmanager.exe`) to browse test runs, edit ROI events, merge databases, or export multi-rate columnar `.csv`, `.datx`, or `.rwx` files.
