# MARLIN

**Marine Adaptive Response and Lifecycle Intervention Network**

MARLIN is a proposed, two-layer jellyfish interception and recovery concept for protecting a coastal power-plant intake. The repository contains the proposal deck, the simulation package, selected public-data records, design documentation, and the current conditional v4 scenario report.

## Start here

- [Proposal deck (PDF)](MARLIN_ENEC_Proposal.pdf) · [editable PowerPoint](MARLIN_ENEC_Proposal.pptx)
- [Project source and documentation](MARLIN/README.md)
- [Latest v4 simulation report](MARLIN/outputs/v4/low-slip/RUN_REPORT.md)
- [Interactive report page](MARLIN/outputs/v4/low-slip/report.html)
- [Downloadable v4 simulation archive](MARLIN_Simulation_v4.zip)

## Reproduce the v4 screening run

From the repository root, with Python 3.10 or newer:

```powershell
python MARLIN/simulation/v4/run_scenarios.py
```

The script writes results under `MARLIN/outputs/v4/low-slip/`. The packaged report is a conditional model result, **not** a prediction of ENEC site performance or proof of 95% capture. It uses uncalibrated contact, geometry, flow, collection, and transport assumptions. Read the physics review and run report before interpreting percentages. The model does not establish animal survival, bycatch outcomes, operational safety, or regulatory approval.

## Repository scope

The repository includes source code, configurations, documentation, selected processed public forcing tables, and the latest v4 outputs. Temporary files, virtual environments, raw image files, and the large raw-data bundle are excluded; download instructions and provenance are documented under `MARLIN/data/` and `MARLIN/docs/`.
