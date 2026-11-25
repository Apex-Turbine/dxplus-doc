# Installing & Licensing

**APEX DX+** uses the **APEX License Manager (ApexLM / ALM)** for node-locked, floating network, and borrowed offline licensing across Windows and Linux systems.

---

## Windows Installation

![DX+ Installer](images/installer.png)
*DX+ Windows Installer component selection*

1. Run the DX+ installer executable on a 64-bit Windows 10 or Windows 11 workstation (administrator privileges required if installing system-wide services).
2. Choose the **Installation Folder** (by default, core runtimes, plugins, `CrashReporter.exe`, and application executables install into `dx+/bin/`).
3. Select the DX+ packages to install:
   - Core **DX+** runtime, **Devices**, **Processors**, and **Net & Storage** plugins
   - Domain applications (**DX+ DAQ**, **DX+ Online Analysis**, **DX+ Offline Analysis**, **DX+ Data Viewer**, **DX+ Remote Viewer**)
   - Supporting tools and bridges (**DX+ DB Manager**, **DXNet Bridge (OPC UA)**, **DXNet Bridge (PLC)**)
4. Ensure **ApexLM** (the required license manager service and system-tray companion) is selected.
5. Complete the installation. Launch applications from **Start → APEX DX+**.

> [!NOTE]
> Unhandled exceptions in any DX+ desktop application invoke `CrashReporter.exe` to generate a forensic `.rpt` log and minidump for support submission at [https://users.apexturbine.com/](https://users.apexturbine.com/).

---

## Linux Service & Server Deployment

On 64-bit Linux systems, **ApexLM** can run as an unmanaged foreground process or be generated and registered as a **systemd** unit (`apexlm.service` for local/passthrough workstations or `apexlm-server.service` for central floating license servers):

```bash
# Run as root to generate /etc/systemd/system/apexlm.service
sudo python apps/main_cli.py interactive
ApexLM> service install
ApexLM> service start
ApexLM> service status

# Or for the floating License Server service (apexlm-server.service):
sudo python apps/main_server_cli.py interactive
ApexLM> service install
ApexLM> service start
```

| Environment | Local Service Database Path | Server Service Database Path |
| :--- | :--- | :--- |
| **Windows** | `C:\ProgramData\APEX\APEXLM\apexlm.db` *(fallback `%APPDATA%\APEX\APEXLM\apexlm.db`)* | `C:\ProgramData\APEX\APEXLM_Server\apexlm_server.db` *(fallback `%APPDATA%\APEX\APEXLM_Server\apexlm_server.db`)* |
| **Linux** | `/var/lib/apexlm/apexlm.db` *(fallback `~/.local/share/apexlm/apexlm.db`)* | `/var/lib/apexlm-server/apexlm_server.db` *(fallback `~/.local/share/apexlm-server/apexlm_server.db`)* |

> [!TIP]
> On Windows, running `service install`, `service start`, `service stop`, `service restart`, or `service uninstall` inside an **elevated** PowerShell `python apps/main_cli.py interactive` session manages the native `ApexLMService` (and `ApexLMServerService` via `apps/main_server_cli.py interactive`).

---

## Managing Licenses with ApexLM

**ApexLM** runs a background license service plus a **loopback-only embedded Web Admin UI** (no password or session token required; loopback reachability authorizes local administration) and an interactive CLI (`main_cli.py interactive`).

![ApexLM System Tray Menu](images/alm-task-tray-menu.png)
*Right-click the **A** icon in the Windows notification area and open **ApexLM** / **Open Configuration***

![ApexLM Configuration Window](images/alm-window.png)
*ApexLM status, license loading, and active token checkout view*

### Step-by-Step Activation (Workstation / Local License)

1. Ensure the ApexLM service is running.
2. Right-click the **A** icon in the system tray and choose **Open Configuration** (or navigate directly in a local browser to **`http://127.0.0.1:27887/`** for the local service, or **`http://127.0.0.1:27888/`** on a floating license server host; `/api/v1/ui` is also supported).
3. In the **Overview / License** view, upload or browse to your Ed25519-signed **Format Version 2** license file (`.lic` / `.json`), or load it from the CLI:
   ```text
   ApexLM> set mode local
   ApexLM> load file C:\path\to\license.json
   ApexLM> status
   ```
4. Once applied, licensed applications and feature pools immediately become active without restarting the service.

> [!WARNING]
> **Format Version 2 Requirement & Legacy Licensing:** ApexLM requires **Format Version 2** JSON license files signed with Ed25519 (host-bound to uppercase hexadecimal MAC addresses without separators, e.g. `00155D2B5AB4`, or wildcard `*`/`demo` for portable demo keys). Format Version 1 keys and legacy FlexNet (`lmgrd`) license files are **not accepted**; contact APEX support for an updated v2 key if migrating from legacy DX installations.

---

## Operating Modes & Ports

| Mode | Purpose | Bind Address & Port | Notes |
| :--- | :--- | :--- | :--- |
| **`LOCAL`** | Single workstation, offline node-locked license | `127.0.0.1:27884` (`APEXLM_PORT`) | Validates local license file against machine MAC addresses. |
| **`PASSTHROUGH`** | Local proxy forwarding to a remote floating server | `127.0.0.1:27884` $\rightarrow$ `<Server IP>:27885` | Supports **borrowing** counted features & hardware serials offline for **up to 30 days**. |
| **`SERVER`** | Central floating license server | `0.0.0.0:27885` (`APEXLM_SERVER_PORT`)<br>External listen `27886` (`APEXLM_SERVER_LISTEN`) | Rejects direct unproxied app clients; workstation clients connect via `PASSTHROUGH` or `APEXLM_HOST`/`APEXLM_PORT`. Admin UI stays restricted to `127.0.0.1:27888`. |

### Environment Variables

Applications and services read connection settings from system environment variables or a local `.env` / `.env.apexlm` file in the application folder:

- `APEXLM_HOST` *(default `127.0.0.1`)* — hostname or IP of the ApexLM service.
- `APEXLM_PORT` *(default `27884`)* — standard service CurveZMQ port (`27885` for server mode).
- `APEXLM_MANAGEMENT_PORT` / `APEXLM_ADMIN_PORT` *(default `27887`)* — local web admin HTTP port.
- `APEXLM_SERVER_MANAGEMENT_PORT` / `APEXLM_SERVER_ADMIN_PORT` *(default `27888`)* — server web admin HTTP port.
- `APEXLM_TIMEOUT` *(default `5000` ms)* — request timeout.

---

## Application & Feature Tokens Reference

Every DX+ application checks out an **application seat** at startup and maintains a **5-second heartbeat**. If transient network interruptions drop the license connection, running applications automatically reconcile and re-checkout active features and hardware serials when connectivity resumes.

### Application Tokens (`ApexApps.csv` & Runtime Checkouts)

| Application | License Catalog Token | Runtime `appname` / Primary Feature |
| :--- | :--- | :--- |
| **DX+ Suite Bundle** | `DXPLUS` | Master DX+ framework entitlement |
| **DX+ Data Acquisition** | `DX+DAQ` | `"dx+daq"` |
| **DX+ Online Analysis** | `DX+ONLINEANALYSIS` | `"dx+onlineanalysis"` |
| **DX+ Offline Analysis** | `DX+OFFLINEANALYSIS` | `"dx+offlineanalysis"` |
| **DX+ Remote Viewer** | `DX+REMOTEVIEWER` | `"dx+remoteviewer"` |
| **DX+ Data Viewer** | `DX+DATAVIEWER` | `"dx+dataviewer"` |
| **DX+ DB Manager** | `DBMANAGE` | `"dbmanage"` (`DBMANAGE-APP`) |
| **DXNet Bridge (OPC UA)** | `OPCUA` | `"opcua"` (`OPCUA-BRIDGE-APP`) |
| **DXNet Bridge (PLC)** | *(runtime bridge token)* | `"plc"` (`plc-bridge-app`) |
| **Wildcard / Multi-App** | `ANY` | Wildcard entitlement covering all applications |

### `ANALYSIS` Token Pool & Add-On Feature Catalog (`ApexFeatures.csv`)

Processors, sinks, and file/stream modules check out named features when initialized (unless included in the app's base bundle):

| Feature Token | Checkout Model | Token Cost (`ANALYSIS` Pool) | Covered Capabilities |
| :--- | :--- | :--- | :--- |
| `BASIC-PROCESSING` | `COUNTED` | `5` | Core filtering (FIR/IIR), scalar EU conversion, resampling, time align, triggers, statistics |
| `LIMITS-PROCESSING` | `COUNTED` | `3` | Range & modal/frequency limits evaluation (`Freq Limits`) |
| `ROTATINGMACHINERY-PROCESSING` | `COUNTED` | `10` | Spectral FFT/DFT, Order FFT, Order Filter, Tachometer, Rev Resample, Relative Phase |
| `ACOUSTICS-PROCESSING` | `COUNTED` | `10` | Octave Band (`1/N`-octave, Z/A/C weighting) |
| `SIGNAL-MATH-PROCESSING` | `COUNTED` | `10` | Signal Math algebraic expressions across streams |
| `SOLUTIONFIT-PROCESSING` | `COUNTED` | `10` | Mode Fit & Static Fit modal/static comparison against FEA limits |
| `VIRTUAL-MODELS` | `COUNTED` | `10` | 3D Model Viewer & Model Publisher |
| `VIDEO-STREAM` | `COUNTED` | `10` | Synchronized video capture, storage, and playback |
| `AEROMECHANICS-PROCESSING` | `COUNTED` | `15` | Aeromechanics analysis components |
| `DBMS` | `COUNTED` | `30` | Database writer/reader access (`SQLite` `.dxdb` & `PostgreSQL`) |
| `DXNET-TX` | `INCLUDED` | — | `DX+Net Transmitter` output |
| `DXNET-RX` | `ACCRUAL` | — | `DX+Net Receiver` / remote subscription seats |
| `DXNET-CONTROL` | `ACCRUAL` | — | Remote DAQ control |
| `DS-RX` / `CYRES-RX` | `ACCRUAL` | — | Legacy `APEX DS` / `Cyres WebSocket` receivers |
| `IDDS-TX` / `IDDS-RX` | `ACCRUAL` | — | iDDS publishing and receiving |
| `APEX-FILE-STANDARD` | `INCLUDED` | — | `.rwx`, `.pkx`, `.datx`, and `.h5` file readers and writers |
| `APEX-DEVICES` | `ACCRUAL` | — | Physical hardware device access |
| `APEX-SIMULATORS-PREMIUM` | `COUNTED` | — | Advanced simulation sources |

---

## Hardware Serial Validation

Hardware drivers validate chassis/card serial numbers against the **`hardware`** section of your ApexLM license before streaming starts:

- **Supported Vendor Keys**: `pacific`, `hgl`, `mecalc`, `datatel`, `scanivalve`, `dewesoft`, `ni`, `ps9016`, `vti`.
- **Enabled-Stream Scoping**: DX+ collects hardware serial numbers **only from currently enabled channels/streams**. Unconfigured or disabled spare cards installed in a chassis do not require serial entries in your license.
- **Wildcard Hardware Licenses**: Licenses configured with `*` for a vendor authorize any hardware serial from that vendor.
- **Disconnecting Between Runs**: Disconnecting an idle socket does not drop the hardware license reservation until the device setup is reset or closed, preventing seat churn between consecutive test runs.
