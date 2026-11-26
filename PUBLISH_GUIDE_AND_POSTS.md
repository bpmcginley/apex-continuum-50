# Apex-Continuum-50 v2 publishing guide

- Repository https://github.com/bpmcginley/apex-continuum-50
- Release and downloads https://github.com/bpmcginley/apex-continuum-50/releases/tag/v2.0.0
- Run the checksum verification command below from the repository root.

    sha256sum -c SHA256SUMS_OPEN_RELEASE.txt

## Zenodo DOI

Open [Zenodo GitHub settings](https://zenodo.org/account/settings/github/) with the linked GitHub account. Click **Sync now**, then toggle **bpmcginley/apex-continuum-50** on. The integration archives release events received after it is enabled. For a release already published before linking, [create a Zenodo upload](https://zenodo.org/uploads/new) using the v2.0.0 source ZIP and the GitHub release URL. Record a DOI after publication.

## Preprint submission

Use the [engrXiv submission portal](https://engrxiv.org/about/submissions) or [OSF Preprints](https://osf.io/preprints/) and choose **Add a Preprint**. Upload **Apex_Continuum_50_v2_Scientific_PoC_Paper_FINAL.pdf**. Use CC-BY-4.0 for the paper and cite the repository and tagged release as supporting material.

## Show HN

**Title**

Show HN: Open-source 50 MW thermal-to-sCO2 storage design with solver evidence

**Body**

I’m releasing Apex-Continuum-50 v2, a computational proof of concept for multi-day thermal storage. It pairs a zero-salt magnesia-spinel brick store with a dry-cooled sCO₂ reheat Brayton cycle. The repo includes the paper, CAD, CalculiX stress fields, an OpenFOAM checkpoint, and the CoolProp cycle results.

Two decisions came directly from the component audit. We retained full Inconel 740H after the modeled summer LTR terminal reached 262.76 °C, and changed the header baffle taper after the original design produced 25.35 kPa of loss in OpenFOAM. The rectified case measured 6.22 kPa and 6.92% maximum port deviation. The candidate RIB_F8 pin-ribs also lost their credit after the CFD comparison.

The system model gives 50.00 MW net AC and 52.36% AC round-trip efficiency at 20 °C ISO, with $65.50M in modeled block CAPEX. I’d welcome a critique of the evidence and the proposed hardware validation, especially the 740H bond coupons and header flow rig.

Repo: https://github.com/bpmcginley/apex-continuum-50
Paper, brief and CAD downloads: https://github.com/bpmcginley/apex-continuum-50/releases/tag/v2.0.0

## Reddit · r/energy

**Title**

Open-source thermal storage study: 24 h and 100 h LCOS for a modeled 50 MW plant

**Body**

I’ve published Apex-Continuum-50 v2, a computational design that couples magnesia-spinel brick storage to a dry-cooled sCO₂ reheat Brayton cycle. The model gives 50.00 MW net AC, 52.36% AC RTE, and $82.48/$98.50 per MWh LCOS for 24/100 h at ISO. At 42 °C it gives 45.08 MW, 48.49% AC RTE, and $89.86/$107.05 per MWh. The $65.50M block estimate retains full Inconel 740H and credits $0 in duplex savings.

The paper separates the modeled economics from measured numerical component results and lists the hardware tests still open. I’d be interested in feedback on the cost basis or comparison conditions for other long-duration storage technologies.

Repo: https://github.com/bpmcginley/apex-continuum-50
Release: https://github.com/bpmcginley/apex-continuum-50/releases/tag/v2.0.0

## Reddit · r/engineering

**Title**

Open-source FEA and CFD evidence for a 50 MW thermal-to-sCO2 storage design

**Body**

I published the paper, CAD, and selected solver files for Apex-Continuum-50 v2. The 48,548-element CalculiX 740H unit cell reached 112.60 MPa peak bond-node von Mises under the elastic surge load. Thickened SS316L failed its project screen at 117.53 MPa. The rectified header reached 6.22 kPa loss and 6.92% maximum port deviation in OpenFOAM, and RIB_F8 was excluded after a 14.25% friction increase with a small decrease in Nu.

I’d welcome technical review of the elastic assumptions, CFD interpretation, or how to size a cold-flow rig and PCHE module test. The repo lists the outstanding coupon, scaling, header, vendor and patent review gates.

Repo: https://github.com/bpmcginley/apex-continuum-50
Paper and CAD: https://github.com/bpmcginley/apex-continuum-50/releases/tag/v2.0.0

## Lab and university outreach

**Subject**

Open computational baseline for thermal-to-sCO₂ storage — coupon or flow-rig collaboration

**Body**

Hi [Name],

I’m sharing Apex-Continuum-50 v2, an open computational proof of concept for a 50 MW dry-cooled thermal-to-sCO₂ storage plant. It integrates magnesia-spinel refractory storage, etched Inconel 740H recuperators, and a commercially geared synchronous generator.

The release includes a seven-page paper, CAD, a 48,548-element CalculiX surge case, an OpenFOAM header checkpoint and reductions, and the 192-interval CoolProp closure. The paper reports solver outputs and modeled system performance in separate categories.

Would your group be interested in reviewing one of the open validation tasks? The immediate candidates are 740H diffusion-bond creep and fatigue coupons, module-level PCHE heat-transfer scaling, and a cold-flow header rig to assess port distribution.

Repository: https://github.com/bpmcginley/apex-continuum-50
Paper, brief, and CAD downloads: https://github.com/bpmcginley/apex-continuum-50/releases/tag/v2.0.0

Best,
Bruce McGinley
