# Oscilloscope waveform and harmonic analysis

[← Portfolio](../README.md)

## Objective

Assess whether coated-fiber optical channels retain the waveform and harmonic content of magnetic excitation, using a simultaneous Hall-reference channel.

![Measured waveform, FFT and fit dashboard](results/scope_dashboard.png)

The existing dashboard uses one measured simultaneous capture. Optical channels and the Hall-reference voltage are analyzed on the recorded timebase without channel substitution or forced phase inversion.

```mermaid
flowchart LR
    C["Measured scope export"] --> T["Validate timebase<br/>contiguous samples · Nyquist"]
    T --> F["Waveforms and FFT"]
    F --> H["Fit 60 / 120 / 180 Hz"]
    H --> R["Amplitude · raw phase<br/>residual RMS"]
    style R fill:#dcfce7,stroke:#15803d
```

The analysis implementation and raw research captures are retained privately. The dashboard shows an existing measured-data analysis, rather than a publicly reproducible dataset. Voltage-domain analysis does not establish magnetic sensitivity or calibrated physical phase.
