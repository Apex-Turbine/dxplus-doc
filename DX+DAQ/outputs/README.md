# Outputs

The **Outputs** pane controls where the data flowing through your DAQ design is sent. Each output is configured on its own tab, and any combination of outputs can be enabled at the same time.

* [**Viewer**](viewer.md) — selects which streams are forwarded to the DX+ Viewer for live plotting.
* [**Store (SQLite)**](sqlite.md) — records selected streams to a SQLite (`.dxdb`) database on disk.
* [**Transmit**](transmit.md) — publishes selected streams over the network so remote DX+ Viewer instances can subscribe.

> [!NOTE]
> Each tab exposes its own Streams / Inputs tree. Streams are grouped by their source element (e.g. `Frequency Sweep Simulator 1`, `Spectrum`) and can be enabled or disabled individually or by group.

## Common Controls

The bottom toolbar of each tab provides the same set of tree controls:

* **Expand All / Collapse All** (left side) — expand or collapse every group in the tree.
* **Enable Selected / Disable Selected** (right side) — turn the selected streams on or off.
* **Filter** — type to narrow the tree to matching stream names.

The trees start collapsed when a setup is first loaded, and groups for newly added processors (for example a Spectral processor) are added collapsed, to keep the trees short.
