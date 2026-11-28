# DX+ Remote Viewer & DXNet-Rx

**DX+ Remote Viewer** (`DX+RemoteViewer.exe`) monitors **live network telemetry streams** broadcast from [DX+ DAQ](../../DX+DAQ/outputs/transmit.md), [DX+ Online Analysis](../../DX+OnlineAnalysis/outputs.md#dxnet-transmitter-dxpnettransmittercomponent), [DXNet Bridge (OPC UA)](../../Services/DXNet%20Bridge%20%28OPCUA%29/README.md), or [DXNet Bridge (PLC)](../../Services/DXNet%20Bridge%20%28PLC%29/README.md) — allowing engineering, control-room, and remote workstations to inspect test data in real time without touching the primary DAQ host.

For lightweight desktop, tablet, and Android field monitoring, the cross-platform **DXNet-Rx** (`DXPlus-ViewApp`) companion viewer connects to the same ZeroMQ (`tcp://`) and WebSocket (`ws://`) publishers with hardware-accelerated dashboards.

Once connected, Remote Viewer uses the same plotting workspace as every DX+ viewer — see [Viewer General](../General/README.md) for the ribbons, plot types, and live limit indicators.

---

## Core Capabilities

- **Zero-Configuration LAN Auto-Discovery (mDNS)**: Automatically discovers active DX+ transmitters on the local subnet via `_dxnet._tcp.local` (UDP `224.0.0.251:5353`), or connects manually over routed subnets and VPNs via `Host/IP : Port`.
- **Event & Stream Filtering**: Filter active channels and discrete event streams on connect via the **Query Filter** dialog.
- **Live Plotting & Limit Alerts**: Plot live streams and watch **Range Limits (`R`)** and **Frequency Limits (`F`)** alerts using the shared [Viewer workspace](../General/workspace-and-ribbons.md).

> [!NOTE]
> `DX+ Remote Viewer` connects **only to live stream publishers**. To inspect previously recorded `.dxdb`, PostgreSQL, `.datx`, `.rwx`, `.pkx`, or `.h5` files, use **[DX+ Data Viewer](../DX+DataViewer/README.md)**.

---

## Licensing

- **DX+ Remote Viewer**: Checks out `DX+REMOTEVIEWER` (`"dx+remoteviewer"`) with a 5-second **ApexLM** heartbeat and stream-receiver entitlements (`DXNET-RX` / `DS-RX`) as required; see [Installing & Licensing](../../introduction/installing-and-licensing.md).

---

## In This Section

- [Connecting & Discovering Streams](connecting-and-streams.md) — LAN mDNS discovery, manual URI/port connection (`27026` vs `27126`–`27176`), firewall tips, and the **DXNet-Rx** companion app.

For plotting once connected, see [Viewer General](../General/README.md): [Workspace & Ribbons](../General/workspace-and-ribbons.md), [Building Plots](../General/building-plots.md), and the [Time-Based](../General/time-based-plots.md) and [Frequency-Based](../General/frequency-based-plots.md) plot references.
