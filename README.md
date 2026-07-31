# 🌊 Petrospect AI — OceanGuard AI

**An AI-powered system for marine oil spill detection, drift prediction, and incident reporting.**

Petrospect AI is a graduation research project that combines satellite SAR imagery, physics-based drift modeling, historical incident intelligence, and generative AI reporting into a single decision-support pipeline for marine oil spill response — accessed through **OceanGuard AI**, a full-stack desktop application.


## Overview

Oil spills are difficult to detect quickly, hard to track as they drift, and time-consuming to report through traditional workflows. Petrospect AI addresses this by fusing multiple independent detection and analysis signals into a single, auditable confidence score, then simulating spill drift and auto-generating a structured incident report — all within a desktop interface built for analysts.

## System Architecture

The pipeline integrates five components into a weighted decision system:

| Module | Role |
|---|---|
| **MarineXt** | Transformer-based semantic segmentation of Synthetic Aperture Radar (SAR) imagery to detect candidate spill regions |
| **OpenOil / OpenDrift** | Lagrangian particle-tracking simulation (5,000 particles) for spill drift and trajectory forecasting |
| **CMEMS + ERA5** | Ocean current and atmospheric/weather reanalysis data feeding the drift simulation |
| **Fuzzy Validation Module** | Rule-based validation layer that cross-checks detections against environmental conditions |
| **NLP Historical Database** | Retrieval over 3,500+ historical incident records to contextualize new detections |
| **Mistral-7B** | Generates structured, human-readable incident reports from the fused analysis |

Detections are combined using a weighted ensemble confidence score:

```
C_final = 0.45 · C_CV + 0.20 · C_PG + 0.35 · C_NLP
```

where `C_CV` is the computer-vision (MarineXt) confidence, `C_PG` is the physical/geospatial (drift-model) confidence, and `C_NLP` is the historical/textual-evidence confidence.

A **Majority Veto / Safety Veto** rule (formally defined in the accompanying paper) overrides the ensemble score in specific high-risk or high-uncertainty conditions to prevent both false negatives and false alarms.

## Key Features

- 🛰️ SAR-based spill segmentation using a transformer vision model
- 🌊 Physics-based drift and trajectory forecasting via OpenOil/OpenDrift
- 🧠 Historical case retrieval across 3,500+ documented incidents
- ⚖️ Multi-source weighted confidence fusion with a safety-veto override
- 📝 Automated, LLM-generated incident reports (Mistral-7B)
- 🗺️ Interactive map-based visualisation of detections and predicted particle drift
- 🖥️ Cross-platform desktop delivery via Electron

## Tech Stack

**Frontend / Desktop**
- Vite + React + TypeScript
- Electron (desktop packaging)

**Backend**
- Node.js + Express

**AI / Modeling**
- MarineXt (transformer-based SAR segmentation)
- OpenOil / OpenDrift (Lagrangian particle simulation)
- Mistral-7B (report generation)
- Fuzzy logic validation module
- NLP retrieval over historical incident data

**Data Sources**
- CMEMS (Copernicus Marine Environment Monitoring Service)
- ERA5 (atmospheric/weather reanalysis)

## Getting Started

> Adjust these commands to match the exact scripts in `package.json` if they differ.

### Prerequisites
- Node.js (LTS recommended)
- npm or yarn
- Python 3.x (for OpenOil/OpenDrift and model-serving components, if run locally)

### Installation

```bash
# Clone the repository
git clone https://github.com/noor7599/<repo-name>.git
cd <repo-name>

# Install dependencies
npm install
```

### Running in Development

```bash
# Start the backend (Node.js/Express)
npm run server

# Start the frontend (Vite/React)
npm run dev

# Launch the Electron desktop app
npm run electron:dev
```

### Building for Production

```bash
npm run build
npm run electron:build
```

## Project Structure

```
.
├── src/                # React/TypeScript frontend
├── server/             # Node.js/Express backend
├── electron/           # Electron main + preload processes
├── models/             # AI model integration (MarineXt, Mistral-7B, fuzzy module)
├── data/                # CMEMS/ERA5 data handling, historical incident database
└── docs/                # Graduation book, IEEE paper materials, figures
```

*(Update this tree to match the actual repository layout.)*

## Research

This project underpins an IEEE conference paper accepted at **ITC-Egypt 2026** (Track 4: AI and Machine Learning), to be published on IEEE Xplore, alongside a graduation project book detailing the full system design, methodology, and evaluation.

## Roadmap

- [ ] Expand the historical incident database
- [ ] Extend drift forecasting to additional ocean basins
- [ ] Add automated model retraining pipeline
- [ ] Package public demo build
