# MARLIN development package — v0.1 and v0.2

Marine Adaptive Response and Lifecycle Intervention Network

**Status: proposed engineering architecture plus two runnable, uncalibrated research models. No physical band, collector, detector, live-handling process, or release site is validated by this package. Neither model controls equipment.**

**Current concept: two physical layers.** The v0.1/v0.2 reports preserve the earlier three-band design as historical scenario work. The current two-layer, bloom-triggered bubble screening experiment is in `simulation/v2/run_current.py`; it duty-cycles the outer bubble system while leaving the mechanical guide/collector ready and retains one independently sensed residual-recovery layer. Its trigger is a threshold proxy, not trained ML.

## Start here

- [Engineering specification](docs/ENGINEERING_SPEC.md): all three bands, actual extraction pathways, independent reserve capacity, controls, maintenance, and interfaces.
- [Simulation and evidence](docs/SIMULATION_AND_EVIDENCE.md): equations, workflow, assumptions, sources, exclusions, and parameter ownership.
- [Public-data plan](docs/PUBLIC_DATA_PLAN.md): selected datasets, download sources, intended uses, integration workflow and remaining gaps.
- [Downloaded data report](data/DATA_REPORT.md): actual public data coverage, checks, missing intervals, licences and prepared account-dependent requests.
- [Public-data acquisition report](data/DATA_REPORT.md): provenance and coverage. This GitHub copy includes selected processed forcing tables and metadata; the large raw collection and image archive are not included. Regional data do not resolve channel hydraulics or jellyfish biomass.
- [Boat and evidence gaps](docs/BOAT_AND_EVIDENCE_GAPS.md): supervised unmanned development target, crewed initial trials and what simulation cannot establish alone.
- [Simulation v0.2 design and limits](docs/SIMULATION_V2_PLAN.md): implemented algorithms, scenario results, unimplemented items and validation gaps.
- [Validation plan](docs/VALIDATION_PLAN.md): engineering and ecological gates before any production claim.
- [Qandeel comparison](docs/QANDEEL_COMPARISON.md): fair comparisons and evidence still needed.
- [Design decisions](docs/DESIGN_DECISIONS.md): adopted functions, unresolved choices and what the model failures mean for engineering.
- [Verification record](docs/VERIFICATION_RECORD.md): completed software and report checks, with physical validation still pending.
- [Risk register](risk_register.csv): hazards, proposed controls, residual risk, and required verification.
- [Cost template](cost_template.csv): quantities and quotations to obtain; no invented total budget.
- [Model inputs](config/model.json): every numerical input is illustrative, not ENEC site data.

## What happens to jellyfish at each band?

Each band has a separate path: **guide/intercept → local capture pocket → dedicated wet collector → local receiving module → supervised transport → approved release outside the assessed return path**. A receiving module cannot be counted as successfully released biomass. Storing jellyfish indefinitely is not clearance. An inner-band discharge beside the intake is not an approved release solution.

The middle band is prepared on the early warning and activates on actual leakage, outer-stage faults, or approved maintenance. The inner band is also prepared and has independent residual collection. If a reserve stage cannot handle the primary stage's full load, its degraded capability must be declared.

## Run the v0.1 operations model

Python 3.10+; standard library only. Run from this folder:

```powershell
python simulation/marlin_sim.py --config config/model.json --output outputs --samples 24 --seed 20261010
python -m unittest discover -s simulation -p "test_*.py" -v
python simulation/design_tradeoffs.py
```

If `python` is not on your PATH, use the absolute path to an installed interpreter. Generated files:

- `outputs/report.html`: offline scenario explorer with stage flows, storage and failure indicators.
- `outputs/scenario_summary.csv`: representative outcomes and limitations.
- `outputs/sensitivity.csv`: distributions across synthetic parameter samples, **not field probabilities**.
- `outputs/results.json`: inputs, events, stage counters, conservation checks and time series.
- `outputs/RUN_REPORT.md`: actual run findings and limits.
- `outputs/DESIGN_TRADEOFFS.md`: separately varied reserve and logistics assumptions; no field sizing claim.

This preserved model tracks finite capture queues, three dedicated collectors, local receiving limits, activation delay, shared transport/release capacity, refused maintenance, equipment outages, missing detections, and released biomass returning. It explicitly tracks jellyfish that pass beyond the inner band.

It does **not** compute water flow, pressure drop, net deformation, animal survival, bycatch, AI accuracy from images, boat navigation, or regulatory compliance. Occupancy is a queue-loading proxy, not a hydraulic safety calculation. Equipment electricity omits bubble compressors and transport vessel fuel.

## Run the v0.2 public-forcing and particle model

From this folder, with Python 3.10 or later:

```powershell
python simulation/v2/run.py --suite full --samples 4 --morris-trajectories 4 --output outputs/v2/full
```

The v0.2 run pairs assumed three-band and outer-only cases across scripted faults, sensor errors, current reversals, environmental windows, bubble-effect branches, and finite vessel resources. It writes an offline dashboard, a run report, scenario and uncertainty tables, a Morris screening table, a vessel-capacity sweep, and per-run gap and lifecycle records under `outputs/v2/full/`. These are conditional model outputs, not field-success probabilities or claims about ENEC performance.

The v0.2 model uses weighted 2D cohorts, RK2 advection in regional point-forcing scenarios plus an assumed local flow component, angled-line encounters, finite collection/receiving inventories, simple observations and finite vessel trips. It does **not** solve local hydraulics, bubble fluid mechanics, net deformation, actual AI perception, animal welfare/bycatch, navigation or release approval. Read `outputs/v2/full/RUN_REPORT.md` and the dashboard's assumptions before interpreting any percentages.

## Run the current two-layer, bloom-triggered bubble screening scenarios

From this folder, with Python 3.10 or later:

```powershell
python simulation/v2/run_current.py
```

The runner writes `outputs/v2/current-two-layer/RUN_REPORT.md`, `scenario_summary.csv`, and `results.json`. It compares bubbles off, continuously enabled bubbles, and detector-triggered positive/zero/adverse/optical-interference assumptions across nominal and failure cases. A no-bloom false-alarm case checks wasted activation. The outer guide and collector remain ready; only the bubble circuit is duty-cycled. These are conditional simulations, not field probabilities or evidence that the bubble wall improves capture. The model has no trained ML detector, 3D bubble plume, vertical jellyfish lift, local hydraulic solver, bycatch model, or validated site thresholds.

## Run the depth-resolved bubble-plume screening model

```powershell
python simulation/v3/run_physics.py
```

This version adds cohort depth, surface-to-skirt boom geometry, a reduced-order bubble-plume closure, gas-flow and water-depth sensitivity, and an interactive vertical cross-section at `outputs/v3/two-layer-plume/report.html`. The plume inputs are placeholders awaiting site survey and flume calibration. See `docs/PHYSICS_AUDIT_V3.md` and the generated `RUN_REPORT.md` before interpreting any percentage.

## Read outputs correctly

An apparently low residual percentage is meaningful only alongside unprocessed biomass, receiving occupancy, unresolved welfare flags, fault history, and the finite observation horizon. A stage-count advantage is not evidence of novelty or superiority over Qandeel. Severe scenarios are included to expose limits, not to produce a perfect score.

This package was developed with AI assistance. The team should review, explain and reproduce its assumptions and outputs before submission.

