# Processors

The **Processors** section configures the per-stream processing pipeline applied to incoming device data. Each processor is configured through its own settings dialog and can be applied to one or more selected streams.

* [**Raw Units**](raw-units.md) — assigns the raw engineering units of the incoming signal.
* [**Filtering**](filtering.md) — applies a digital filter (FIR or IIR) to selected streams.
* [**Conversion**](conversion.md) — converts the raw signal into a different unit or representation.
* [**Spectral**](spectral.md) — produces frequency-domain output via FFT or DFT, with optional peak detection.
* [**Statistics**](statistics.md) — calculates statistics such as maximum, minimum, average, and RMS over fixed time intervals.

> [!NOTE]
> Each settings dialog applies the chosen configuration to every stream selected at the time the dialog is opened. Streams that aren't selected are left unchanged.
