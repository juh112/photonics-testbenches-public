# Instrument integration

[← Portfolio](../README.md)

The acquisition workflow coordinates field targets, motorized analyzer rotation, repeated optical-power reads and measured-field readbacks. Run configuration, raw samples and fitted results are logged together. The OSA workflow acquires companion spectra rather than synchronous VNA/optical data.

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

| Instrument / role | Integration function |
|---|---|
| Coil supply and Hall reference | Approach field targets and record measured field |
| CONEX analyzer rotation | Move, settle and record angular position |
| PM400 optical power | Acquire repeated samples at each condition |
| AQ6370B optical spectrum analyzer | Configure sweep and retrieve spectral traces |
| Run logging and analysis | Preserve timestamps, settings, readbacks and polarization fits |

Implementation code and equipment configuration are retained privately. The diagram describes the acquisition sequence; it does not imply simultaneous optical/VNA acquisition or independently repeated hardware validation.
