# Apex-Continuum-50 v2 final zero-trust continuum audit

**The rectified dry model retains a 740H LTR and the 62%/64% F9 taper.** The original duplex cost credit is withdrawn. The 240 °C duplex unit cell clears the elastic stress screen, while the available summer heat balance puts the LTR hot inlet above the handoff’s 240 °C zone basis. RIB_F8 and Desert_Mist receive no performance credit in the dry closure. Reported system performance is a **HEOS-backed model result**. It incorporates pressure and heat-transfer evidence from component CFD and an isothermal elastic FEA screen.

## Resource gate and handoff provenance

| Resource | Verified before the first solve |
|---|---|
| WSL and CPU | 6.18.58.1-microsoft-standard-WSL2, 22 logical CPUs, one-minute load 0.978 |
| Memory | 21,536,010,240 bytes available of 23,084,810,240 bytes WSL RAM |
| Disk | Windows workspace 26,338,406,400 bytes free; WSL scratch 908,864,167,936 bytes free. Both clear 5 GB. |
| Swap and cap | WSL swap used 0 bytes. Each job used systemd `MemoryMax=2500000000` and `MemorySwapMax=0`; the effective memory ceiling was 2,499,997,696 bytes. |
| Engines | CalculiX `ccx`, Gmsh 4.12.1 compiled backend `libgmsh.so.4.12.1` loaded through Python, CoolProp 7.2.0, OpenFOAM v2312 `pimpleFoam` and `scalarTransportFoam`; the thermal job used the bundled `scalarTransport` function object with `pimpleFoam`. |

The initial preflight held because the standalone Gmsh launcher was absent. Solver work began after verifying the installed compiled Gmsh backend used by the existing conformal mesh builder and rerunning the resource gate. The aggregate cap also bounds any individual solver process. Per-run CalculiX peak RSS is recorded in the Gate 1 results. Peak scope memory was CalculiX 486.2 MB, original F9 169.3 MB, rectified F9 167.9 MB, RIB_F8 427.5 MB, HEOS 117.7 MB. [Passing preflight](solver_evidence/preflight.json) · Initial diagnostic (archival record)

The handoff contains W101–W200, ten rows per block. The archived campaign script assigns the Dry efficiency and cost inputs before computing LCOS. Its **$79.90/$96.23 per MWh** ISO figures reproduce from those model inputs. The 8,760-hour results use synthetic seasonal and daily sinusoids, and the Monte Carlo summaries apply distributions to the campaign's assumed system values. Those files provide model context and carry no solver or field-validation credit in the final numbers. Handoff systems (archival record) · Wave ledger (archival record) · Rectifications (archival record) · Dispatch model (archival record) · Monte Carlo summary (archival record)

## Zero-trust claim ledger

| Gate | MODELED handoff claim | MEASURED numerical outcome | Credit carried into Dry |
|---|---|---|---|
| 1 · Zoned metallurgy | Duplex surge SF 2.76 and $6.58M alloy savings | Duplex 112.596476 MPa at 240 °C. The summer heat balance places the hot inlet above that temperature basis. | Retained 740H. $0 duplex savings. |
| 2 · HDR_F9 | 9.42 kPa header loss and 0.8% core-coupled port deviation | Original 25.345299 kPa / 9.316173%. Rectified 6.222383 kPa / 6.917408%. | Rectified loss under the fallback distribution gate. |
| 3 · RIB_F8 | Nu 56.3 and Fanning f 0.0119 | Nu 43.621533958; mean f 0.0116527337, upper-window f 0.0132524507. | Archived Variant B thermal and friction inputs. |

## Gate 1 · CalculiX C3D10 surge and metallurgy

Each conformal cell uses the Variant B **0.95 m LTR** cross-section and local repeat length. The pressure step is **440.25 bar high side / 79 bar low side** with the carried +10% etch screen, two ideal bonded interfaces, and constrained axial/lateral strain. The Duplex input is **E = 190 GPa, ν = 0.30** and the project comparison threshold is **175 MPa at 240 °C**. The supplied thickened 316L geometry uses **3.05 mm rib / 3.20 mm plate, E = 179 GPa**, and the project threshold **115 MPa**. The model uses ν = 0.30 for 316L and 740H. The 740H fallback uses the vendor modulus interpolated to 275 °C. Mesh target sizes were 0.340, 0.270 and 0.220 mm. The two finest meshes had to agree in peak bond-node stress within 5%. The values are extrapolated nodal stresses from the FRD output.

| Material | Isothermal (°C) | C3D10 element count | MEASURED bond-node von Mises across mesh sizes (MPa) | Fine global nodal peak (MPa) | Finest-two drift | Screening limit (MPa) | Disposition |
|---|---:|---|---|---:|---:|---:|---|
| Duplex 2205 | 240 | 15,010 / 26,642 / 48,548 | 97.450095 / 113.911745 / 112.596476 | 131.946534 | 1.1546% | 175 | Passes at 240 °C. Hot zone remains uncertified. |
| Thickened SS316L | 240 | 17,987 / 32,361 / 58,314 | 98.919349 / 114.030954 / 117.531826 | 133.474356 | 3.0701% | 115 | Fails 115 MPa project screen. |
| Retained 740H | 275 | 15,010 / 26,642 / 48,548 | 97.450023 / 113.912003 / 112.596476 | 131.946511 | 1.1549% | — | Mesh screen passes. Retained material. |

Variant B's prior summer LTR hot inlet is **262.768132 °C**. A wall-temperature and dissimilar-bond zone design would be needed to assign a verified amount of the LTR to 2205. The cost model retains full 740H and **$0** of the claimed **$6.58M** alloy saving. The 275 °C 740H result is an elastic load screen. Bond-life allowables, diffusion-bond coupons and thermal gradients remain open. [All mesh results](solver_evidence/gate1.json) · [740H vendor modulus](https://www.specialmetals.com/documents/technical-bulletins/inconel/inconel-alloy-740h.pdf)

## Gate 2 · HDR_F9 original and rectified baffles

Both runs used a **33,408-cell**, 340 mm × 850 mm cylinder, symmetric dual ends, the four specified axial baffle stations, three curved full-span zero-thickness turning sheets, four outlets and the same **20.5 kPa nominal core jump** at design branch flow. The handoff omitted vane drawings and a separate perforation-loss curve for the altered open area. The model uses **3 mm axial bow**, the inherited 65 mm core standoff, the W142 reported 34%/44% loss coefficients and the recorded inverse-square open-area extrapolation to the tested 62%/64% taper. The fixed-density point is the Option A Variant B HTR inlet at **309.050293 kg/s** plant flow and **484.267353 K**. The **450 kg/m²·s** design flux belongs to the LTR cold passages.

| Case | Four open-area zones | MEASURED header-only ΔP (kPa) | MEASURED core-plane ΔP (kPa) | MEASURED assembly ΔP (kPa) | Max mass imbalance | Max port deviation from mean | Max full port spread / mean | Header ΔP window drift |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| Original F9 | 34% / 44% / 44% / 34% | 25.345299 | 21.053916 | 46.413829 | 0.000002913% | 9.316173% | 18.631712% | 0.006243% |
| Rectified F9 | 62% / 64% / 64% / 62% | 6.222383 | 20.968606 | 27.215510 | 0.000002800% | 6.917408% | 13.833737% | 0.023259% |

The first shakedown exposed a shared face pressure at the coupled jump. The audited reruns use separate taps on either side to recover flux-weighted total pressure. Header loss ends **9.286 mm upstream of the core interface** and core drop spans from there to **10 mm downstream**. Timesteps remained below Co 0.8 and both cases ran approximately six residence times. The original taper missed the 11.7 kPa header limit and the 8.90% fallback distribution benchmark. The 62%/64% case meets the loss and mass gates and clears the allowed comparison with HDR_F8. Its port deviation remains above the preferred 2.5%. The handoff's 0.8% core-coupled headline was not reproduced. The assembly includes the additional core resistance. The cycle uses the header-only loss and accounts for PCHE friction in the recuperator network. Original F9 (archival record) · [Rectified F9](solver_evidence/apex-v2-hdrf9-rect/result.json) · [Porous-jump law](https://doc.openfoam.com/2306/tools/processing/boundary-conditions/rtm/derived/wall/porousBafflePressure/)

## Gate 3 · RIB_F8 CFD and rectified reheat RCBC

The four-rank, **105,000-cell** RIB_F8 run reached **5.99799** sampled flow-throughs. It used an unslotted six-pin periodic realization with three stagger phases, **1.500/0.975 mm** alternating chords, **0.620 mm** narrow tail-shank width, **0.682839 mm** gap and the Phase A reference hydraulic diameter. The handoff supplied the chord ratio, minimum feature and pattern. Absolute chords and the exact rounded polygon use the documented reconstruction in the inputs. The calculation held HEOS properties at **29.33207600 MPa, 660.30048852 K, 482.964 kg/m²·s**, **Re = 11473.29314**, **Pr = 0.808864792** and **Prₜ = 0.85**. It used the same fixed-wall periodic scalar energy-balance method as Option A. Geometry and operating point (archival record) · Mesh validation (archival record) · [OpenFOAM scalar transport](https://api.openfoam.com/2312/scalarTransport_8H_source.html)

| Gate 3 observation | Variant B archive | RIB_F8 solver output | RIB_F8 verdict |
|---|---:|---:|---|
| Wall-area film Nu | 43.66 | 43.621533958 | Below control |
| Mean Fanning f | — | 0.0116527337 | Reference comparison uses the upper-sample statistic below. |
| Upper-window Fanning f | 0.01160 | 0.0132524507 | Fail against W109's 8% loss allowance, limit 0.012528. |
| Mean pressure drop per two-pitch repeat | — | 186.849487 Pa | Compare designs by Fanning f or gradient because repeat lengths differ. |
| Latest two-period thermal averaging drift | — | 1.57116% | Pass joint 1- and 2-period diagnostic. |
| Latest two-period hydraulic averaging drift, f / ΔP | — | 4.17937% / 4.17915% | Fail against 2%. |

Relative to the archived control, the thermal mean changes by -0.088104%, and peak-window friction increases 14.245265%. The RIB_F8 mean is **0.593708299×** the Phase A matched film Nu. Peak Courant number was **0.721442**. The upside remains excluded from the audited system closure. [Gate 3 result](solver_evidence/apex-v2-ribf8/result.json) · Scalar time series (archival record) · Friction time series (archival record)

### MODELED system results from 192-interval CoolProp HEOS closure

| Metric | Rectified Dry 20 °C | Rectified Dry 42 °C | 
|---|---:|---:|
| Net AC export (MW) | 50.000000 | 45.075388 |
| Gross AC (MW) | 50.902823 | 46.011615 |
| Mass flow (kg/s) | 307.352611 | 307.352611 |
| Net AC efficiency (%) | 52.833181 | 48.926509 |
| AC round-trip efficiency (%) | 52.357683 | 48.486170 |
| LTR pinch (K) | 10.170230 | 11.884172 |
| HTR pinch (K) | 18.660292 | 20.153371 |
| Hottest LTR fluid terminal (°C) | 229.773237 | 262.760841 |
| Installed block CAPEX ($M) | 65.499570 | 65.499570 |
| Block CAPEX per delivered net kWe ($) | 1309.991402 | 1453.111632 |
| 24h LCOS ($/MWh) | 82.477661 | 89.861597 |
| 100h LCOS ($/MWh) | 98.497460 | 107.051976 |
| Cycle pressure-closure residual (Pa) | 0.02865010 | 0.01904590 |

The retained reheat RCBC fixes Variant B's LTR length and passage area, 0.39 ISO / 0.34 summer recompression splits, and each design's ISO-sized flow for its summer point. It applies the **6.222383 kPa** selected header-only loss, **43.66** conservative film Nu with multiplier **0.594231839**, and the **0.960527957** archived friction upper-bound multiplier. TS_F10 **$8.99/kWhₜₕ and 0.991 charge/thermal factor**, and the **97.86% / $151 per gross kWe** geared generator inputs are modeled. The control hardware carries a **$200,000** allowance. The continuous control, condensation, CHP, grid inertia and mist performance claims remain outside the credited results. Economics use the locked electricity-only convention with 180 cycles/year at 24h, 50 at 100h, $25/MWh charge and an 8.02% capital recovery factor. [Machine-readable HEOS states and cost inputs](solver_evidence/gate3_cycle.json) · [CoolProp HEOS interface](https://coolprop.org/coolprop/LowLevelAPI.html)

### Reconciliation with the shipped Dry claim

| Metric | Shipped model | Rectified solver-backed model | Difference |
|---|---:|---:|---:|
| Block CAPEX ($M) | 58.92 | 65.499570 | 6.579570 |
| ISO AC RTE (%) | 52.44 | 52.357683 | -0.082317 pp |
| Summer net AC (MW) | 45.45 | 45.075388 | -0.374612 |
| ISO 24h LCOS ($/MWh) | 79.90 | 82.477661 | 2.577661 |
| ISO 100h LCOS ($/MWh) | 96.23 | 98.497460 | 2.267460 |
| Summer 24h LCOS ($/MWh) | 86.77 | 89.861597 | 3.091597 |

The installed block estimate uses the Variant B 740H cost basis, replaces the prior $145 drivetrain line with $151 per gross kWe, and adds the control allowance. Per-delivered-kWe CAPEX rises in summer with the same installed dollars. CAPEX reflects the inherited cost model and carries no supplier quote for the rectified header. The handoff provides no separate condenser or mist validation, so the Desert_Mist values remain campaign claims.

## Commands and SHA-256 custody

The archive digests below describe the original run. The public [checksum manifest](SHA256SUMS_OPEN_RELEASE.txt) covers the distributed bytes after path and hostname redaction. The lite release includes the result files linked below. Other archival record names are retained for provenance.

All numerical stages ran sequentially. The scripts and recorded resource-scoped invocations are in the execution logs. The preflight used the WSL venv's Python and OpenFOAM environment.

| Stage | Numerical calls | Execution record |
|---|---|---|
| Preflight | `python -B preflight_resource_check.py` inside the capped systemd scope | [Preflight](solver_evidence/preflight.json) |
| Gate 1 | `python -B phase_b_scripts/apex_v2_fea.py`, Gmsh C API through Python, and `/usr/bin/time -f "CCX_MAX_RSS_KB %M" timeout -k 10s 180s ccx -i bond` | Gate 1 (archival record) |
| Gate 2 | `python -B phase_b_scripts/apex_v2_header.py <case>` with the second run using `--sigma .62 .64 .64 .62`. Each numerical run used `blockMesh`, `createPatch -overwrite`, `topoSet`, `checkMesh -allGeometry -allTopology`, `pimpleFoam`. | Original (archival record) · Rectified (archival record) |
| Gate 3 CFD | `python -B phase_b_scripts/apex_v2_rib.py <case>` with Gmsh generation, `gmshToFoam case.msh`, `createPatch -overwrite`, `checkMesh -allTopology -allGeometry`, `decomposePar`, then `mpirun -np 4 --bind-to none` launching affinity-pinned `pimpleFoam -parallel` ranks on 0, 2, 4 and 6. | RIB_F8 (archival record) |
| Gate 3 HEOS | `python -B phase_b_scripts/apex_v2_cycle.py --headers <original-result> <rectified-result> --rib <rib-result>` | HEOS (archival record) |

| Key artifact | SHA-256 |
|---|---|
| `apex_campaign_v2_lenovo_handoff.zip (attached archive)` | `190882e4b25de9396d1132e07497cd1a36a05a09aad8ad73b3b4880cfe5a6e9b` |
| `apex_v2_lenovo_specs.json` | `4a7d625a669cfc8687b6289ff7a32219ae03a313c905e57b4a653b171e5f374d` |
| `dispatch_8760h.json` | `4e8b8ec041c53fdf1c709efc9b12075867d575f5c33c980872ea0e2ace90c65f` |
| `mc_10k_v2.json` | `e93fa698f95e2d57c7f659cf293f23032f81efc0ccda3aa775b11471488934f7` |
| `rectifications_blocks_11_to_20.md` | `3d620c1d0e10730ff0dc420ab17b4bbb60c2b67ae1588a9a903b954c568763ef` |
| `v2_harmonized_systems.json` | `bb08474c0a3dcb915cca132a775b94f00e4718a67c29079a448b70efa464d506` |
| `wave_ledger_101_to_200.csv` | `007d01ab9714b658eaa29ee9a551aff185bc653f1e70dfc4e72c293426d9c96f` |
| `gate1.json` | `2fa31e9411845cfc40e38cb903d1fa14eba8e98bb57cfd2df9c887a6dbeebb60` |
| `gate3_cycle.json` | `d233a6da23fbec351ec41e531bd44de4551102c3fd92c049c555b57290e31572` |
| `preflight.json` | `61d0ebe6281d783d0bf8f36d81dd77edf3f42c98ed577b3677d0fb5021b65efc` |

[Public SHA-256 manifest](SHA256SUMS_OPEN_RELEASE.txt)

