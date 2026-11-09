# NV-center optical and microwave characterization

[← Portfolio](../README.md)

## Objective

Establish fluorescence readout and test whether microwave-dependent optical features survive background, electrical-pickup and repeatability controls. PCB feasibility testing precedes photonic-chip interface validation.

![Optical bench](figures/optical_bench.png)

## Measurement workflow

```mermaid
flowchart TD
    P["Record configuration<br/>sample · optical alignment · RF chain · detector"] --> O["Check PL and background<br/>wafer/no-wafer or ND/coverslip · power dependence"]
    O --> R["Characterize RF path separately<br/>VNA fixture/calibration + antenna configuration"]
    R --> H["Operator checks / alignment baseline<br/>configure detector and RF source"]
    H --> B{"Readout configuration"}
    B -- "QEPro: source reviewed" --> Q["Choose frequency order and real/null mode"]
    Q --> PA["At each frequency: alternate OFF→ON / ON→OFF pairs<br/>acquire spectra and integrate PL"]
    PA --> C["Save raw spectra + pair records<br/>ON/OFF ratio · contrast mean/SEM · fit diagnostics"]
    C --> REP["Compare null, reverse/randomized order<br/>and independent repeats"]
    B -- "APD: supplied result figures" --> A["Compare illuminated REAL with laser-off DARK<br/>check electrical pickup / filtering"]
    A --> REP
    REP --> G{"Reproducible sample-specific feature<br/>beyond matched controls?"}
    G -- "Not established" --> N["Report ODMR unconfirmed<br/>diagnose alignment, drift and pickup"]
    G -- "Future evidence satisfies criteria" --> E["Document validation evidence<br/>before extracting device metrics"]
    PA -. "PL collapse / interruption" .-> STOP["Save completed data<br/>attempt RF OFF"]
```

## Fluorescence baseline

![Measured wafer photoluminescence](figures/wafer_pl.png)

Sample/background and power-dependent PL establish a usable optical signal; PL alone is not ODMR. The supplied figure reports one spectrum per acquisition condition, without replicate error bars.

## PCB feasibility and assembled hardware

[PCB layout, FDTD results, assumptions and selected source](pcb_feasibility/README.md)

![PCB assembly](figures/pcb_assembly.png)

![PCB mounted beneath the objective](figures/pcb_sample_mount.png)

The board marking identifies the g0.10 variant. The g0.12 model is kept separate in the detailed comparison.

![Measured PCB reflection](figures/pcb_wide_s11.png)

The supplied re-soldered PCB trace has its global minimum away from the NV drive target; it is not evidence of successful target-frequency optimization. A quantitative simulation/measurement correlation requires matching board, fixture and calibration records.

## Readout pickup investigation

![Measured RF pickup before and after filtering](figures/pickup_filter_comparison.png)

This is a laser-dark electrical-pickup comparison with unequal sample counts, not a demonstrated ODMR sensitivity improvement. Repeatability and matched optical/RF controls remain the validation criteria. Reproducible ODMR is not established by these plots.
