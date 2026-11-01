**English** | [Türkçe](README.tr.md)

# Whole-Brain Virtual Twins from Open Connectome Data

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME/REPOSITORY/blob/main/sanal_ikiz_noroinformatik.ipynb)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

> **[DECISION]** Replace `USERNAME/REPOSITORY` in the Colab badge and the links below with your GitHub path, and choose the licence (MIT is suggested for code; see [Licence](#licence)).

This repository contains the complete, reproducible analysis behind the manuscript

**"Are Whole-Brain Virtual Twins Personal? Evidence from Open Connectome Data and a Bibliometric Review including Türkiye"**
*(submitted to the Journal of Computational Bioengineering and Clinical Medicine, JCBCM)*

Everything — data loading, modelling, statistics, every figure and table, and the bibliometric review — runs in **one Jupyter notebook** with step-by-step commentary in Turkish. Every figure is produced in **both English and Turkish** at 300 dpi.

## What the study asks

A *digital twin* should be **personalised**, **updated with data** and **predictive**. We built subject-specific whole-brain models for seven healthy adults and tested these properties directly:

| # | Question | Notebook section |
|---|----------|------------------|
| Q1 | Does a twin built on a person's own diffusion-MRI connectome reproduce and predict that person's resting-state brain activity? | 5–6 |
| Q2 | Is the twin **specific** to that person, i.e. better than a twin built from someone else's connectome? | 7 |
| Q3 | What do **virtual lesions** of each of the 80 cortical regions reveal about network vulnerability? | 8 |
| Review | How large is brain/neuro digital twin research worldwide and in Türkiye? (OpenAlex) | 9 |

## Main results

| Measure | Result |
|---|---|
| Direct structure–function correlation (SC–FC) | r = 0.263 ± 0.042 |
| Virtual twin vs. empirical FC | **r = 0.471 ± 0.115** (better in 7/7 participants, p = 0.016) |
| Prediction of the unseen half of the recording | r = 0.455 (69% of the test–retest ceiling) |
| Shuffled-connectome twin (null model) | r = 0.065 |
| Own twin vs. other participants' twins | Δr = −0.007, permutation p = 0.78 → **not personal** |
| Group-average connectome twin | r = 0.495 |
| Virtual lesion maps: reliability / link to node strength | ρ = 0.85 / ρ = 0.79 |
| OpenAlex brain/neuro digital twin publications (2015–2026) | 1,164 (precision 96%); Türkiye 19th with 12 |

**Take-home message:** mechanistic brain twins capture the *shared* architecture of the human connectome and generalise over time, but personalisation must be **demonstrated, not assumed**. The cross-fit test in Section 7 is a simple way to do this for any twin pipeline.

## Data

- **Primary cohort:** 7 healthy adults from the WU-Minn **Human Connectome Project (HCP)** — structural connectivity and fibre length from diffusion tractography, and resting-state BOLD (1,200 volumes, TR = 0.72 s), parcellated into 80 cortical AAL2 regions.
- **Replication cohort:** 5 participants (used only for the empirical structure–function correlation).
- Both are distributed with the open-source [`neurolib`](https://github.com/neurolib-dev/neurolib) library and are loaded automatically; **no data are stored in this repository**.
- **Bibliometrics:** retrieved live from the [OpenAlex](https://openalex.org) API (results in this repository were accessed on 1 November 2026).

HCP data: *Data were provided by the Human Connectome Project, WU-Minn Consortium (Principal Investigators: David Van Essen and Kamil Ugurbil; 1U54MH091657), funded by the 16 NIH Institutes and Centers that support the NIH Blueprint for Neuroscience Research, and by the McDonnell Center for Systems Neuroscience at Washington University.* Use of HCP data is subject to the HCP Open Access Data Use Terms (see [humanconnectome.org](https://www.humanconnectome.org)).

## Method in brief

Each region is a **Stuart–Landau (Hopf) oscillator** near its bifurcation point (*a* = −0.02), with its intrinsic frequency measured from the participant's own BOLD signal. Regions are coupled through the participant's own structural connectome; a single global coupling *G* is calibrated per participant against empirical functional connectivity (0.04–0.07 Hz). Validation uses functional connectivity dynamics (FCD), temporal cross-validation, a cross-fit specificity test with permutation statistics, control twins (group-average, structure-only, rhythm-only, shuffled network) and split-seed reliability for virtual lesions.

## Quick start

**Google Colab (recommended)** — click the badge above, then *Runtime → Run all*. The first cell installs `neurolib`. A full run takes about **40–50 minutes** on a standard Colab CPU.

**Local**

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
pip install -r requirements.txt
jupyter notebook sanal_ikiz_noroinformatik.ipynb
```

### OpenAlex API key (free)

Section 9 queries OpenAlex. Shared Colab IP addresses often hit the anonymous rate limit (HTTP 429), so a **free** API key is recommended:

1. Create a free account at [openalex.org](https://openalex.org) and copy your key from *Settings → API*.
2. In Colab, open the 🔑 **Secrets** panel, add `OPENALEX_API_KEY`, and enable notebook access.

The key costs nothing; no payment details are required.

## Repository structure

```
├── sanal_ikiz_noroinformatik.ipynb   # complete analysis (Turkish commentary)
├── requirements.txt
├── sekiller/
│   ├── en/                           # 16 figures, English, 300 dpi JPEG
│   └── tr/                           # 16 figures, Turkish, 300 dpi JPEG
├── ciktilar/                         # result tables (CSV) and OpenAlex query results
├── README.md                         # this file (English)
└── README.tr.md                      # Turkish
```

## Reproducibility

- All stochastic steps use fixed seeds; reruns in the same environment give identical numbers.
- Different library versions may change only the last digits; conclusions are unaffected.
- Bibliometric counts depend on the access date; the query strings and the access date are saved with the results.
- Note for others: in probabilistic tractography the connectomes are **fully dense**, so degree-preserving rewiring is impossible — the notebook uses weight shuffling instead. A query containing the word *neural* inflates neuro digital twin counts about sevenfold because it captures "neural network" papers.

## Citation

> **[DECISION]** Add the citation once the article is published.

```bibtex
@article{AUTHOR2026virtualtwins,
  title   = {Are Whole-Brain Virtual Twins Personal? Evidence from Open Connectome Data and a Bibliometric Review including T{\"u}rkiye},
  author  = {AUTHOR, A. and AUTHOR, B.},
  journal = {Journal of Computational Bioengineering and Clinical Medicine},
  year    = {2026},
  note    = {Submitted}
}
```

Please also cite the tools and data: neurolib (Cakan et al., 2023, *Cognitive Computation*), the Human Connectome Project (Van Essen et al., 2013, *NeuroImage*) and OpenAlex (Priem et al., 2022).

## Licence

> **[DECISION]** Suggested: **MIT** for the code (notebook) and **CC BY-NC 4.0** for the figures and tables (the licence used by JCBCM). HCP data are not redistributed here and remain under the HCP Data Use Terms.

## Use of generative AI

An AI assistant (Claude, Anthropic) was used to draft and debug code, produce figures and tables from computed results and draft text. All code, results and references were reviewed and verified by the authors.

## Contact

> **[DECISION]** Name, institution and e-mail of the corresponding author.
