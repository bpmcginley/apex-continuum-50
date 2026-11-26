# Contributing to Apex-Continuum-50 v2 (Open Hardware & Lab Gates)

Apex-Continuum-50 v2 is released openly so universities, national laboratories, EPC engineers, and independent researchers can move it from a continuum-audited computational PoC to physical hardware.

## Zero-Trust Contribution Standard
Every PR or experimental report must preserve strict separation between:
- **`MEASURED`** (numerical outputs from continuum solvers with traceable inputs),
- **`MODELED`** (parametric cycle, CAD, or technoeconomic projections), and
- **`HARDWARE`** (physical rig and coupon data, with the experimental setup and conditions identified).

## The Five Open Hardware & Qualification Tracks
1. **Track 1 — Inconel 740H Diffusion-Bond Creep & Fatigue Coupons:**
   - Current state: Isothermal elastic CalculiX surge screen (`112.60 MPa` bond-node peak at `275 °C`, `440.25/79 bar`).
   - Needed: Coupled thermal-gradient FEA (`262.76 °C` summer hot inlet), physical 740H diffusion-bond creep/fatigue test data, and (optional upside) dissimilar 2205-to-740H cold-zone transition coupon testing to recover up to `$6.58M` in LTR CAPEX.
2. **Track 2 — PCHE Module Heat-Transfer Scaling:**
   - Current state: Archived Variant B periodic cell `Nu = 43.66` (`0.5942×` analytic).
   - Needed: Benchtop or pilot-loop module-level sCO₂ heat-transfer data verifying thermal scaling across full `0.95 m` etched plates.
3. **Track 3 — Cold-Flow `HDR_F9` Header Rig (`<2.5%` Port Uniformity):**
   - Current state: OpenFOAM `pimpleFoam` rectified `62%/64%` taper measured `6.22 kPa` loss and `6.92%` max port deviation.
   - Needed: 3D-printed or machined scaled cold-flow manifold rig testing secondary vane angles / graded perforations to reach `<2.5%` deviation without exceeding `11.7 kPa`.
4. **Track 4 — Binding OEM Maps & Vendor Quotes:**
   - Current state: Parametric `$65.50M` block CAPEX and `97.86%` / `$151/gross kWe` commercial `3,600 RPM` geared WRSM basis.
   - Needed: Vendor off-design sCO₂ compressor/turbine maps (`20 °C` ISO & `42 °C` summer) and budgetary/binding quotes for etched 740H PCHEs, header fabrication, and `TS_F10` magnesia-spinel bricks (`$8.99/kWh_th`).
5. **Track 5 — Formal IP Freedom-to-Operate (`US11530625B2`):**
   - Needed: Independent patent counsel claim-chart verification of the external forced-convection Kanthal/SiC charging plenum relative to `US11530625B2`.
