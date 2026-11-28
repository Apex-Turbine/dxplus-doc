# Receivers

**Receivers** are data sources from which DX+ subscribes to streams rather than directly configuring the source. This includes hardware receivers, file-based replay sources, and built-in simulators used for testing and demos.

> [!NOTE]
> Receivers are implemented as Phoenix input components and share their configuration UI with the Phoenix runtime. For the full per-device configuration reference (fields, defaults, behavior), see the Phoenix documentation: [**APEX Phoenix — Inputs**](../../DX+OnlineAnalysis/inputs-and-streams.md).

## APEX RWX Device

Replays data from an APEX `.rwx` file as a live stream into the setup.

## Frequency Sweep Simulator

Generates a configurable swept-sine signal across one or more streams. Useful for verifying frequency-domain processing.

## APEX Data Simulator

Generates simulated APEX-format data streams for testing and demos.

## APEX DS Receiver

Receives channels from an APEX DS (DSNet) source. Enter the **Address** and **Port** of the DS source (Port defaults to **Auto**), or click **Discover** to find it on the network. **Pull Setup** reads the source's channel list.

## DX+Net Receiver

Receives streams published by another DX+ system's [Transmit](../outputs/transmit.md) output.

## Sound Input

Receives audio from a system sound input device (microphone or line-in).

> [!NOTE]
> Datatel is now an [Integrated](integrated.md#datatel) device.

## Dewesoft

Receives streams from Dewesoft DAQ hardware.

## National Instruments

Receives streams from National Instruments DAQ hardware.

## PSI 9016

Receives streams from a PSI 9016 pressure scanner.

---

## Further Reading

For the full configuration reference for each receiver — fields, defaults, and runtime behavior — see the Phoenix Inputs documentation: [**APEX Phoenix — Inputs**](../../DX+OnlineAnalysis/inputs-and-streams.md).
