# SmartFires – REU Program · Summer 2026
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


---

## 1. Project Overview

**SMART FireS** (Sensors, Machine Learning, and Artificial Intelligence in Real Time Fire Science) is a statewide Montana NSF EPSCoR research initiative. Its vision is to expand jurisdictional research capacity to address knowledge gaps associated with **prescribed fire usage** and to understand prescribed fire's impact on individuals, ecosystems, and communities across Montana.

The project spans multiple thrusts — sensor networks, AI/ML modeling, ecology, and community engagement — carried out collaboratively across six Montana institutions.

---

## 2. BMW Lab Role in SmartFires

The **BMW Lab at MSU** is part of the **AI/ML thrust** within SmartFires. Our work focuses on:

> *(will update shortly)*

Our contributions draw on airborne hyperspectral imagery, satellite multispectral data, and machine learning pipelines to support fire science decision-making.

---

## 3. Understanding Prescribed Fire

Prescribed (or "controlled") fire is the intentional, planned use of fire by land managers to reduce hazardous fuel loads, restore ecosystems, and improve forest health. Before diving into the technical work, you should understand the ecological and policy context. Read through the following link below to more detailed understanding of presribed fire or burns:

| Resource | Description |
|---|---|
| [MT Prescribed Fire Council (DNRC)](https://dnrc.mt.gov/Forestry/MT-Prescribed-Fire-Council/MTPFC) | Montana state-level prescribed fire governance |
| [Fire Adapted Montana](https://fireadaptedmontana.org/prescribed-fire-1) | Community and landscape fire adaptation context |
| [MT Fire Info – Landscape](https://www.mtfireinfo.org/pages/landscape) | Montana statewide fire landscape overview |
| [Helena-Lewis & Clark NF – Prescribed Burning](https://www.fs.usda.gov/r01/helena-lewisclark/fire/prescribed-burning) | Regional USFS prescribed burn program |
| [USFS – Managing Land: Prescribed Fire](https://www.fs.usda.gov/managing-land/prescribed-fire) | National USFS prescribed fire policy |
| [National Forests Foundation – What is Prescribed Fire?](https://www.nationalforests.org/article/what-is-prescribed-fire-and-why-is-it-important-for-forest-health/) | Accessible explainer on forest health rationale |
| [NPS – What is a Prescribed Fire?](https://www.nps.gov/articles/what-is-a-prescribed-fire.htm) | National Park Service overview |



---

## 4. Prior Work & Key Papers

Before starting your summer project, read the following work produced by the BMW Lab. These papers form the technical foundation you will build on.

### Isaq — Band Selection & Hyperspectral Classification

**Paper 1 (IEEE MLSP 2025):**
> Karankot, M. I. et al. — *[Attention and Edge-Aware Band Selection for Efficient Hyperspectral Classification of Burned Vegetation]*
> 🔗 https://ieeexplore.ieee.org/abstract/document/11204320
> Code Repo -- https://github.com/BMW-lab-MSU/SF_Prescibed_Fire_HSI

**Paper 2 (MDPI Remote Sensing, 2026):**
> Whitaker, B. M. et al. — *Hyperspectral Band Selection for Ground Fuel Classification for Prescribed Fires*
> Remote Sensing, Vol. 18, Issue 9, p. 1440. DOI: [10.3390/rs18091440](https://doi.org/10.3390/rs18091440)
> 🔗 https://www.mdpi.com/2072-4292/18/9/1440
> > Code Repo -- https://github.com/BMW-lab-MSU/hyperspectral-feature-selection-prescribed-fires

**Summary of Paper 2:** This study evaluates five dimensionality reduction strategies for hyperspectral imagery (PCA, SSEP, SRPA, DRL-based selection, and K-Means clustering) combined with classical and deep learning classifiers (RF, SVM, KNN, 3D-CNN). It includes evaluation on benchmark datasets (Indian Pines, Pavia University) and a new **real-world VNIR dataset collected after prescribed burns at Lubrecht Experimental Forest, Montana**. The goal is compact, informative spectral band subsets that improve classification while reducing computational cost.

### IGARSS 2026 Fire Burn Mapping (Sentinel-2)
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

**Download link:** *(will update link shortly)*

> **The VNIR binary is ~97 GB.** Do not attempt to load it entirely into RAM. Use tiled/windowed reading via `spectral` or `rasterio`. See the preprocessing notebooks for examples.

The data collection process and sensor specifications are documented in the two papers listed in Section 4.

### 5.2 Satellite Data — Sentinel-2 (Google Earth Engine)

We use **Sentinel-2 multispectral imagery** for fire burn mapping tasks. Access is via **Google Earth Engine (GEE)**.

- **Sign up for GEE:** https://earthengine.google.com/ (requires a Google account; approval may take 1–2 days)
- **Sentinel-2 Surface Reflectance collection:** `COPERNICUS/S2_SR_HARMONIZED`
- **Key bands used:** B2 (Blue), B3 (Green), B4 (Red), B8 (NIR), B11/B12 (SWIR) — useful for NBR, NDVI, burn severity indices
- **GEE Python API (geemap):** https://geemap.org/
- **GEE JavaScript Code Editor:** https://code.earthengine.google.com/

**Satellite data download link:** *(will update link shortly)*

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

>  **Add these to your calendar immediately.**

| Date | Time | Location |
|---|---|---|
| Fri, May 29 | 2:00 – 3:00 PM MST | Cobleigh Hall 630 |
| *(subsequent Fridays — TBD)* | 3:00 – 4:00 PM MST | Cobleigh Hall 630 |

This schedule will be updated here soon.


---

## 10. Contacts

**Preferred mode of communication: Email**

| Name | Role | Email | Location |
|---|---|---|---|
| Dr. Bradley Whitaker | Faculty Advisor | bradley.whitaker1@montana.edu | Cobleigh Hall 630 |
| Mahmad Isaq Karankot | PhD Student / Mentor | mahmadisaq.karankot@student.montana.edu · mahmad.isaq@outlook.com | Cobleigh Hall 640 (BMW Lab) |




---

*README maintained by Mahmad Isaq Karankot · BMW Lab · MSU*
*Last updated: May 2026 · Questions? Email Isaq or open a GitHub issue.*
