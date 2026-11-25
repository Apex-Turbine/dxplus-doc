# System Requirements

## Operating System

### Windows Desktop Applications & Services (64-bit)

Supported 64-bit Windows versions:

- **Windows 10** (64-bit)
- **Windows 11** (64-bit)

### Linux Services (64-bit)

- **APEX License Manager (`ApexLM` / `apexlm.service` & `apexlm-server.service`)** runs identically on 64-bit Linux distributions with **systemd**, alongside Python/Qt6 Phoenix services and CLI utilities where deployed on Linux hosts.

---

## Hardware Requirements

DX+ applications target 64-bit **x86-64** processors.

> [!IMPORTANT]
> The CPU **must support the AVX2 instruction set** (typically Intel or AMD processors manufactured in 2016 or later). Running on CPUs without AVX2 support is not supported.

### Minimum Hardware

- **Processor**: 64-bit dual-core CPU at 2.0 GHz or faster with **AVX2** support.
- **Memory**: 2,048 MB (2 GB) RAM.
- **Storage**: 120 GB 7,200 RPM hard drive (SSD strongly recommended for multi-channel database recording).
- **Display & Graphics**: OpenGL-capable graphics adapter and monitor at `1280 x 1024` or higher.

### Recommended Baseline Hardware

- **Processor**: 64-bit quad-core (or higher) CPU with **AVX2** support.
- **Memory**: 4,096 MB (4 GB) RAM or higher (8–32 GB recommended for high-channel-count Spectral, Campbell, PostgreSQL, or 3D Model workloads).
- **Storage**: 500 GB NVMe / SATA SSD.
- **Display & Graphics**: Hardware-accelerated desktop **OpenGL** graphics card and `1920 x 1080` (or higher) monitor (required for VTK 3D Model Viewer and smooth 60 Hz spectral waterfall rendering).

---

## Network Ports Reference

Ensure local firewalls permit traffic on the ports required for your deployment:

| Service / Protocol | Default Port | Range / Protocol | Purpose |
| :--- | :--- | :--- | :--- |
| **ApexLM Local Service** | `27884` | TCP / CurveZMQ | Local & Passthrough license checkouts (`APEXLM_PORT`). |
| **ApexLM Floating Server** | `27885` | TCP / CurveZMQ | Network floating license server (`APEXLM_SERVER_PORT`). |
| **ApexLM Server Listen** | `27886` | TCP / CurveZMQ | Floating server external listen port (`APEXLM_SERVER_LISTEN`). |
| **ApexLM Web Admin UI** | `27887` / `27888` | HTTP (`127.0.0.1` only) | Loopback browser admin UI for Local (`27887`) and Server (`27888`). |
| **DX+ DAQ / Online Transmit** | `27026` | TCP / ZeroMQ | Default `Transmit` control port in `DX+Daq` and `DX+AnalysisOnline`. |
| **DXPNet Telemetry Services** | `27126` | `27126` – `27176` (ZeroMQ) | Default DXPNet receiver/bridge ports (`dx+opcua` outbound `27126`, `dx+plc` outbound `27136`). |
| **mDNS Service Discovery** | `5353` | UDP Multicast (`224.0.0.251`) | Automatic LAN discovery (`_dxnet._tcp.local`). |
| **Remote Component Manager** | `27100` | `27100` – `27125` (ZeroMQ) | Remote Phoenix component orchestration. |
| **DSNet Protocol** | `10995` | `10990` – `10999` (TCP) | Legacy APEX DS hardware streaming (`DS Receiver`). |
| **OPC UA** | `4840` / `4850` | `opc.tcp` | Default external OPC UA port (`4840`) and `DXNet Bridge (OPC UA)` Mirror Server (`4850`). |
| **EtherNet/IP (CIP)** | `44818` | TCP & UDP | Allen-Bradley ControlLogix PLC communication and `dx+plc --test-server`. |
| **PostgreSQL** | `5432` | TCP | Enterprise database storage and query connections. |
