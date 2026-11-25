# Connecting & Discovering Streams

**DX+ Remote Viewer** subscribes directly to live **DX+Net** (ZeroMQ) publishers and compatible stream sources without interrupting acquisition on the transmitting host.

---

## Connecting in DX+ Remote Viewer (`DX+RemoteViewer.exe`)

1. Open **Start → APEX DX+ → DX+ Remote Viewer**.
2. Click **File → Connect** and select the stream adapter (such as **`DX+Net Receiver`**).
3. Choose either **Auto-Discovery** or **Manual Connection**:
   - **Auto-Discovery (`Discover`)**: Click **Discover** to scan your LAN via mDNS (`_dxnet._tcp.local`). Select a discovered transmitter row showing **Service Name**, **Host Name**, **IP Address**, and **Port**. Under **Connect using**, select **Host Name** *(default)* or **IP Address**.
   - **Manual Endpoint**: Enter the transmitting host's **URI / IP Address** and control **Port** directly.
4. Click **Connect**. If event/channel filtering is enabled on the endpoint, select the channels/events to display in the **Query Filter** dialog.
5. Repeat **File → Connect** to monitor multiple transmitters simultaneously, or use **File → Recent Stores** and **File → Close** to manage active sessions.

### Default Port Reference

| Publisher Application | Default Control Port | Notes |
| :--- | :--- | :--- |
| **DX+ DAQ (`Transmit` tab)** | **`27026`** | Configurable in the [DAQ Transmit Output](../DX+DAQ/outputs/transmit.md) tab. |
| **DX+ Online Analysis (`DX+Net Transmitter`)** | **`27026`** *(or auto `-1`)* | Sequential multi-instance transmitters also use **`27126`–`27176`**. |
| **DXNet Bridge (OPC UA)** | **`27126`** | ZeroMQ REP control + PUB streaming (`27127`). |
| **DXNet Bridge (PLC)** | **`27136`** | ZeroMQ REP control + PUB streaming (`27137`). |
| **mDNS Discovery** | **`5353`** (UDP Multicast `224.0.0.251`) | Required for automatic LAN **Discover**; manual IP:Port works across routed subnets/VPNs when multicast is blocked. |

> [!WARNING]
> **Firewall Check:** If **Discover** finds no transmitters or connection times out, verify Windows Firewall / network ACLs permit inbound TCP connections to both the publisher's **Control Port** (`27026` or `27126`–`27176`) and its dynamically announced **PUB data port**, plus UDP `5353` on LAN interfaces if using mDNS discovery.

---

## DXNet-Rx Companion Viewer (Windows & Android)

**DXNet-Rx** (`DXPlus-ViewApp`) provides a touch-friendly, cross-platform dashboard client for phones, tablets, control-room displays, and field laptops:

1. **Connect or Scan LAN**: Click **Connect** (top bar) or **Scan LAN** (`_dxnet._tcp.local`) to rank reachable adapters automatically. Enter a publisher password if authentication is enabled.
2. **Manual / Routed / WebSocket (`ws://`)**: Enter **Host / IP** and **Control Port** (default `27126`; use `10.0.2.2` inside an Android Emulator to reach Windows `localhost`), and optionally toggle **Use WebSocket (`ws://`)**. Saved connections reconnect automatically on startup.
3. **Built-In Demo Rig**: Click **Launch Demo** (or **Demo**) to start an in-process simulated turbine publisher with starter dashboards for training without hardware.
4. **Origin-Collapsed Stream Browser**: Automatically groups raw channels, server FFTs, nested `Statistics` (`Max`, `Min`, `Avg`, `Peak`, `P2P`, `RMS`), and `Modal Limits` beneath shared **Origin Source** groups with quick filter pills (**`All`**, **`Plot`**, **`Alert`**, **`FFT`**, **`Stats`**) and **`Src (N)`** variant selection (including **`SERVER FFT`** vs. local **`ON-DEVICE FFT`** fallback).
5. **Themes & Persistence**: Switch between `DX+ Dark`, `Midnight OLED`, `Slate`, `DX+ Blue`, and `Engineer Light`; pages, layouts, strip buffers, and saved connections persist in `dxnet-rx-workspace.json`.
