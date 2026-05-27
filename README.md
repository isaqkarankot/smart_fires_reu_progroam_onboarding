# 🔥 SmartFires – REU Program · Summer 2026
### BMW Lab · Department of Electrical & Computer Engineering · Montana State University

> **SMART FireS** — *Sensors, Machine Learning, and Artificial Intelligence in Real Time Fire Science*
> A Montana NSF EPSCoR partnership among MSU, University of Montana, Salish Kootenai College, Little Big Horn College, Montana Tech, and Flathead Valley Community College.
> 🔗 [Project Home](https://www.mtnsfepscor.org/projects/smart-fires)

Welcome to the BMW Lab's REU onboarding document. Read this top to bottom before your first meeting. It is your single reference for the project background, data, tools, tasks, and contacts for Summer 2026.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [BMW Lab Role in SmartFires](#2-bmw-lab-role-in-smartfires)
3. [Understanding Prescribed Fire](#3-understanding-prescribed-fire)
4. [Prior Work & Key Papers](#4-prior-work--key-papers)
5. [Data](#5-data)
6. [Prerequisites & Required Knowledge](#6-prerequisites--required-knowledge)
7. [Software & Tools Setup](#7-software--tools-setup)
8. [Key Python Libraries](#8-key-python-libraries)
9. [Meetings & Schedule](#9-meetings--schedule)
10. [Contacts](#10-contacts)
11. [Code of Conduct & Best Practices](#11-code-of-conduct--best-practices)

---

## 1. Project Overview

**SMART FireS** (Sensors, Machine Learning, and Artificial Intelligence in Real Time Fire Science) is a statewide Montana NSF EPSCoR research initiative. Its vision is to expand jurisdictional research capacity to address knowledge gaps associated with **prescribed fire usage** and to understand prescribed fire's impact on individuals, ecosystems, and communities across Montana.

The project spans multiple thrusts — sensor networks, AI/ML modeling, ecology, and community engagement — carried out collaboratively across six Montana institutions.

---

## 2. BMW Lab Role in SmartFires

The **BMW Lab at MSU** is part of the **AI/ML thrust** within SmartFires. Our work focuses on:

> *(Add 2–3 sentences describing the specific AI/ML objectives your lab is working on — e.g., hyperspectral image classification, ground fuel mapping, burn severity estimation, etc.)*

Our contributions draw on airborne hyperspectral imagery, satellite multispectral data, and machine learning pipelines to support fire science decision-making.

---

## 3. Understanding Prescribed Fire

Prescribed (or "controlled") fire is the intentional, planned use of fire by land managers to reduce hazardous fuel loads, restore ecosystems, and improve forest health. Before diving into the technical work, you should understand the ecological and policy context. Read through the following:

| Resource | Description |
|---|---|
| [MT Prescribed Fire Council (DNRC)](https://dnrc.mt.gov/Forestry/MT-Prescribed-Fire-Council/MTPFC) | Montana state-level prescribed fire governance |
| [Fire Adapted Montana](https://fireadaptedmontana.org/prescribed-fire-1) | Community and landscape fire adaptation context |
| [MT Fire Info – Landscape](https://www.mtfireinfo.org/pages/landscape) | Montana statewide fire landscape overview |
| [Helena-Lewis & Clark NF – Prescribed Burning](https://www.fs.usda.gov/r01/helena-lewisclark/fire/prescribed-burning) | Regional USFS prescribed burn program |
| [USFS – Managing Land: Prescribed Fire](https://www.fs.usda.gov/managing-land/prescribed-fire) | National USFS prescribed fire policy |
| [National Forests Foundation – What is Prescribed Fire?](https://www.nationalforests.org/article/what-is-prescribed-fire-and-why-is-it-important-for-forest-health/) | Accessible explainer on forest health rationale |
| [NPS – What is a Prescribed Fire?](https://www.nps.gov/articles/what-is-a-prescribed-fire.htm) | National Park Service overview |

**Goal:** After reading these, you should be able to explain *why* prescribed fires are conducted, *who* manages them in Montana, and *what ecological outcomes* they are intended to produce. This context directly motivates the remote sensing work we do.

---

## 4. Prior Work & Key Papers

Before starting your summer project, read the following work produced by the BMW Lab. These papers form the technical foundation you will build on.

### Isaq — Band Selection & Hyperspectral Classification

**Paper 1 (IEEE):**
> Karankot, M. I. et al. — *[Band Selection for Hyperspectral Classification — Prescribed Fire Context]*
> 🔗 https://ieeexplore.ieee.org/abstract/document/11204320

**Paper 2 (MDPI Remote Sensing, 2026):**
> Whitaker, B. M. et al. — *Hyperspectral Band Selection for Ground Fuel Classification for Prescribed Fires*
> Remote Sensing, Vol. 18, Issue 9, p. 1440. DOI: [10.3390/rs18091440](https://doi.org/10.3390/rs18091440)
> 🔗 https://www.mdpi.com/2072-4292/18/9/1440

**Summary of Paper 2:** This study evaluates five dimensionality reduction strategies for hyperspectral imagery (PCA, SSEP, SRPA, DRL-based selection, and K-Means clustering) combined with classical and deep learning classifiers (RF, SVM, KNN, 3D-CNN). It includes evaluation on benchmark datasets (Indian Pines, Pavia University) and a new **real-world VNIR dataset collected after prescribed burns at Lubrecht Experimental Forest, Montana**. The goal is compact, informative spectral band subsets that improve classification while reducing computational cost.

### Isaq — Fire Burn Mapping (Sentinel-2)
> Details and access shared via email. Contact Isaq if you haven't received it.

### Ethan — Thesis Work
> Shared via email. Contact Dr. Whitaker or Isaq if you haven't received it.

### Piper — Synthetic HSI Forest Work
> Shared via email. Contact Dr. Whitaker or Isaq if you haven't received it.

---

## 5. Data

### 5.1 Airborne Hyperspectral Data (Primary Dataset)

Our primary dataset is **VNIR hyperspectral imagery** collected via drone/aircraft at **Lubrecht Experimental Forest, Montana** — a **pre-burn flight**.

| File | Description |
|---|---|
| `vnir.hdr` | Metadata header file (ENVI format — open with a text editor or spectral Python libraries) |
| `VNIR` | Binary hyperspectral datacube (~97 GB) |
| `segmented.png` | Ground truth mask — pixel labels: `1 = tree`, `2 = grass` |

**Download link:** *(Add internal link or shared drive path here)*

> ⚠️ **The VNIR binary is ~97 GB.** Do not attempt to load it entirely into RAM. Use tiled/windowed reading via `spectral` or `rasterio`. See the preprocessing notebooks for examples.

The data collection process and sensor specifications are documented in the two papers listed in Section 4.

### 5.2 Satellite Data — Sentinel-2 (Google Earth Engine)

We use **Sentinel-2 multispectral imagery** for fire burn mapping tasks. Access is via **Google Earth Engine (GEE)**.

- **Sign up for GEE:** https://earthengine.google.com/ (requires a Google account; approval may take 1–2 days)
- **Sentinel-2 Surface Reflectance collection:** `COPERNICUS/S2_SR_HARMONIZED`
- **Key bands used:** B2 (Blue), B3 (Green), B4 (Red), B8 (NIR), B11/B12 (SWIR) — useful for NBR, NDVI, burn severity indices
- **GEE Python API (geemap):** https://geemap.org/
- **GEE JavaScript Code Editor:** https://code.earthengine.google.com/

**Satellite data download link:** *(Add link here once available)*

### 5.3 MTBS — Monitoring Trends in Burn Severity

The **MTBS program** (USGS + USFS) provides national burn severity data derived from Landsat imagery for all fires ≥ 1,000 acres in the western US.

- **MTBS Data Access:** https://www.mtbs.gov/direct-download
- **What we use it for:** Burn severity maps (dNBR), fire perimeter shapefiles, pre/post-fire Landsat composites
- **Data formats:** GeoTIFF (burn severity rasters), Shapefile (perimeters), CSV (fire metadata)
- **Key metadata fields:** `Ig_Date` (ignition date), `BurnBndAc` (acreage), `dNBR` classes (unburned → high severity)

To download for a Montana prescribed burn:
1. Go to https://www.mtbs.gov/viewer/
2. Filter by state = Montana, fire type = Prescribed Fire
3. Download the GeoTIFF + shapefile package for your target event

---

## 6. Prerequisites & Required Knowledge

You don't need to be an expert in everything on day one. Items marked **Required** are expected before you arrive. Items marked **Recommended** should be developed in Weeks 1–2.

### Mathematics (Required)

- **Linear Algebra** — matrix operations, eigendecomposition, dot products (essential for PCA, CNNs)
- **Basic Statistics** — mean, variance, distributions, correlation
- **Basic Calculus** — derivatives, gradients (for understanding model training)
- **Basic Probability** — conditional probability, Bayes' theorem

### Remote Sensing (Recommended)

- What hyperspectral vs. multispectral imagery is (number of bands, spectral resolution)
- What raster vs. vector data are
- Coordinate reference systems (CRS) and map projections
- Basic understanding of spectral indices (NDVI, NBR, dNBR)
- Familiarity with QGIS or ArcGIS is a plus

### Python (Required)

- Writing and running `.py` scripts
- Working with virtual environments (`venv` or `conda`)
- Core libraries: `numpy`, `pandas`, `matplotlib`
- Basic object-oriented programming (classes, methods)
- Reading/writing files: CSV, JSON, GeoJSON

### Machine Learning (Recommended)

- Supervised learning: classification and regression
- Train / validation / test splits; avoiding data leakage
- `scikit-learn` fit/predict/evaluate pattern
- Basic understanding of neural networks (helpful, not required)

### General Tools (Required)

- **Git & GitHub** — cloning repos, committing, branching, pull requests
- **Command line** — navigating directories, running scripts, basic bash
- **Jupyter Notebooks** — running cells, converting to scripts

---

## 7. Software & Tools Setup

Install everything below **before your start date**. Flag any issues to Isaq at least 48 hours in advance.

### 7.1 Core Software

| Tool | Version | Link |
|---|---|---|
| Python | 3.10+ | https://www.python.org/downloads/ |
| Anaconda / Miniconda | Latest | https://docs.conda.io/en/latest/miniconda.html |
| Git | Latest | https://git-scm.com/downloads |
| VS Code *(or PyCharm — your choice)* | Latest | https://code.visualstudio.com/ |
| QGIS | 3.x LTS | https://qgis.org/en/site/forusers/download.html |

### 7.2 Accounts to Set Up

Request access by emailing Isaq **before your start date**:

- [ ] **GitHub** — create an account at https://github.com and share your username with Isaq
- [ ] **Google Earth Engine** — sign up at https://earthengine.google.com/ (takes 1–2 days for approval)
- [ ] **MTBS Data Portal** — https://www.mtbs.gov/ (free, no account needed, but bookmark it)
- [ ] **BMW Lab GitHub Org** — Isaq will add you once your GitHub username is shared
- [ ] **Shared data storage** — *(Google Drive / lab NAS / HPC — Isaq will provide access)*

### 7.3 VS Code Extensions (Recommended)

- Python (Microsoft)
- Pylance
- Jupyter
- GitLens
- Rainbow CSV

---

## 8. Key Python Libraries

These are the core libraries used in BMW Lab work. You will install additional ones as needed while working on your specific project.

| Library | Purpose |
|---|---|
| `numpy` | Numerical computing, array operations |
| `pandas` | Tabular data manipulation |
| `geopandas` | Geospatial vector data (shapefiles, GeoJSON) |
| `rasterio` | Reading and writing raster / satellite imagery |
| `spectral` | Hyperspectral image I/O and analysis (ENVI format) |
| `shapely` | Geometric operations |
| `scikit-learn` | Classical ML models and preprocessing |
| `torch` / `tensorflow` | Deep learning (as applicable to your project) |
| `matplotlib` / `seaborn` | Plotting and visualization |
| `folium` / `plotly` | Interactive maps and dashboards |
| `geemap` | Google Earth Engine + Python integration |
| `requests` | API calls |
| `python-dotenv` | Loading `.env` credential files |

> Install the environment using the `environment.yml` in the repo:
> ```bash
> conda env create -f environment.yml
> conda activate smartfires
> ```

---

## 9. Meetings & Schedule

### Weekly Meeting with Dr. Whitaker — Summer 2026

> ⚠️ **Add these to your calendar immediately.**

| Date | Time | Location |
|---|---|---|
| Fri, May 29 | 3:00 – 4:00 PM MST | Cobleigh Hall 630 |
| *(subsequent Fridays — TBD)* | 3:00 – 4:00 PM MST | Cobleigh Hall 630 |

This schedule will be updated here as dates are confirmed. Check back regularly.

### Standup Format

Come to each meeting ready to share:
1. **Done** — What did you finish since last time?
2. **Doing** — What are you working on now?
3. **Blocked** — What is slowing you down? What do you need?

---

## 10. Contacts

**Preferred mode of communication: Email**

| Name | Role | Email | Location |
|---|---|---|---|
| Dr. Bradley Whitaker | Faculty Advisor | bradley.whitaker1@montana.edu | Cobleigh Hall 630 |
| Mahmad Isaq Karankot | PhD Student / Mentor | mahmadisaq.karankot@student.montana.edu · mahmad.isaq@outlook.com | Cobleigh Hall 640 (BMW Lab) |

> For day-to-day questions, technical help, and data access: **contact Isaq first.**
> For research direction, progress check-ins, and formal matters: **contact Dr. Whitaker.**

---

## 11. Code of Conduct & Best Practices

### Git Workflow

- **Never push directly to `main`.** Create a feature branch, then open a pull request.
- Branch naming: `yourname/short-description` (e.g., `alex/ndvi-preprocessing`)
- Write meaningful commit messages: `Add NDVI calculation to Sentinel-2 pipeline` — not `fix stuff`
- Pull from `main` before starting each work session

### Code Quality

- Write docstrings for every function
- Format code with `black` before committing
- If a notebook exceeds ~200 lines of logic, move that logic into a `.py` module in `src/`
- Add comments explaining *why*, not just *what*

### Data Rules

- **Raw data is read-only.** Never overwrite original files.
- Never commit large data files or credentials to Git (`.env`, binary files, GeoTIFFs)
- Document any new dataset you introduce (source, date downloaded, format)

### Research Integrity

- Report results honestly — failures and negative results are data too
- Cite every dataset and paper you use
- If you're unsure whether something is okay, ask before doing it

### Inclusive Environment

This REU is committed to a respectful, inclusive environment for all participants. Harassment of any kind is not tolerated. If you experience or witness a concern, bring it to Dr. Whitaker or consult [MSU reporting resources](https://www.montana.edu/titleix/).

---

*README maintained by Mahmad Isaq Karankot · BMW Lab · MSU*
*Last updated: May 2026 · Questions? Email Isaq or open a GitHub issue.*
