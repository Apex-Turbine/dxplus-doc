# Features Overview

![APEX DX+ Logo](../images/dxplus-logo-dark.svg)

## Data Acquisition & Sources

- **Integrated Hardware Control**: Configure Mecalc (DECAQ), Scanivalve (DSA/DTS/MPS), Pacific Instruments (6000/6700), HGL Dynamics, and Datatel telemetry systems directly from DX+.
- **Network & Driver Receivers**: Ingest live streams from VTI (including VTI 10xxA), National Instruments, DewesoftNet, PSI 9016, APEX DS (`DSNet`), **DX+Net Transmit/Receive**, Cyres WebSockets, and audio devices.
- **Virtual & Simulated Sources**: Prototype complete setups and plot layouts offline with **Virtual Devices** (`1`–`4,096` channels), **APEX Data Simulator**, **Frequency Sweep Simulator**, or replay recorded **`.rwx`** / **`.datx`** / **`.dxdb`** datasets.

## Real-Time & Post-Test Signal Processing

- **Filtering & Resampling**: Linear-phase **FIR** and **IIR** (Butterworth, Papoulis, Chebyshev, Inv. Chebyshev) filters with Octave/1/3-Octave band selection, plus **Rev Resample** (angular resampling) and **Order Filter**.
- **Spectral & Rotating Machinery**: Unified **FFT / DFT (`FDFT`)**, **Order FFT**, **Tachometer** pulse-to-RPM conversion, **Triggers** (analog/digital hysteresis and debounce), **Relative Phase**, and **Adv. DSP (`Peak`)** spectral peak extraction.
- **Acoustics, Fit & Math**: **Octave Band** analysis (Base 2 / Base 10, Z/A/C weighting), **Frequency Binner**, **Mode Fit** & **Static Fit** modal assurance/frequency alignment, **Signal Math** multi-stream expressions, **Wheatstone Strain Bridge (WSB)**, **EU Calibration / Conversion** (integrate, double-integrate, differentiate), **Statistics**, and **Time Aligner** (offset / IRIG).

## Interactive Visualization

- **Time-Based Plots**: `Scope`, `History` (with automatic `32,768`-point min/max envelope decimation), `Strip`, `Scatter` (Signal Index and Reference modes), and **Graphic** meters (`Gauge`, `Text`, `Thermometer`, `LED`, `Bar`).
- **Frequency-Based Plots**: `Scope`, `Magnitude`, `Envelope`, `Mag+Env`, `Campbell` (Time & Speed), `Zmod` color spectrogram, `Bar`, `Tracking` (Hz or Engine Order), and `Bode` (stacked magnitude + phase).
- **Multi-Modal Views**: Sortable **Table** plot, hardware-accelerated **3D Model Viewer** (VTK FEA modal shape animation), and time-synced **Video Viewer**.
- **Alarm & Limit Monitoring**: Time-domain **Range Limits** and modal/spectral **Frequency Limits** (Warning/Alert thresholds with status indicators and 3-second hold decay).

## Storage, Databases & Industrial Connectivity

- **Databases**: Write and query **SQLite** (`.dxdb` single file or `.dxdb.index` sharded sets) and **PostgreSQL** telemetry stores.
- **Binary & Text Formats**: Read and export **`.rwx`**, **`.pkx`**, **`.datx`** / **`.datx_index`**, **`.h5`** (`APEX-H5`), and multi-rate time-synchronized **`.csv`**.
- **Enterprise Bridges**: Stream live plant and test-stand tags bidirectionally between DX+ and **OPC UA** servers/clients or **Allen-Bradley ControlLogix (`1756-L75` / `1756-L63`)** PLCs over EtherNet/IP (CIP).
