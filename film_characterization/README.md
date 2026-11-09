# Polarization-resolved film characterization

[← Portfolio](../README.md)

## Objective

Determine whether a magnetic-composite coating produces a useful optical response beyond quartz background, and assess the wavelength/loss tradeoff before integrated-device design.

![Actual bench](figures/film_bench.png)

## Acquisition workflow

```mermaid
flowchart TD
    O["Operator: align optics, set QWP,<br/>confirm sample and instrument configuration"] --> R["Create run folder<br/>save configuration + command arguments"]
    R --> I["Identify instruments · set detector wavelength<br/>home analyzer · prepare coil supply"]
    I --> Z["0 V reference<br/>measure residual field + scan analyzer"]
    Z --> F["Next field target<br/>measured-field feedback + stability check"]
    F --> A["Next analyzer angle<br/>move + settle"]
    A --> P["Read repeated optical-power samples<br/>then field + supply voltage/current"]
    P --> L["Append and flush data row<br/>raw power, mean/std, actual angle, field, V/I"]
    L --> N{"More angles?"}
    N -- Yes --> A
    N -- No --> FIT["Fit Malus curve<br/>visibility · polarization angle · fit residual"]
    FIT --> T{"More field targets / repeats?"}
    T -- Yes --> F
    T -- No --> B["Optional return-to-0 V scan<br/>check residual field against initial reference"]
    B --> S["Attempt ramp to 0 V / output OFF<br/>close instruments and export workbook"]
    I -. Exception .-> S
    F -. Exception .-> S
    P -. Exception .-> S
    style R fill:#dbeafe,stroke:#2563eb
    style L fill:#dcfce7,stroke:#15803d
    style FIT fill:#dcfce7,stroke:#15803d
```

## Measured response and design implications

![Film versus quartz control](figures/film_quartz_control.png)

At 1550 nm, the quoted substrate-subtracted slope is unresolved within uncertainty. This supports further controls and wavelength selection rather than a claim of validated chip sensitivity.

![Measured spectral response](figures/spectral_film_results.png)

The wavelength dependence informs material and readout selection. The absorption panel is an inferred upper bound under thickness/background assumptions, not an independent direct measurement of the optical constant.

![Measured bench and proposed polarization change](figures/polarization_noise_comparison.png)

The current-bench noise is labeled measured; the PBS improvement is estimated. It is not presented as a measured before/after improvement.

[Instrument-control source](../instrument_control/README.md)
