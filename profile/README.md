# Landseed PBC

**Earth Credits** — verified ecological condition as a tradeable commodity.

Landseed measures ecosystem health across six scientific dimensions (SEEA EA framework), issues Earth Credits against verified condition, and builds the infrastructure to make ecological truth tradeable at scale.

> **Status (May 2026):** Calculator, Earth Markets, and all portal infrastructure live. Team: Alex Roessner + Greg Curtis.

## Live Products

| Product | URL | What It Does |
|---------|-----|-------------|
| **Landseed Portal** | [landseed.com](https://landseed.com) | NDA-gated asset directory — single entry point for investors, advisors, partners, counsel. |
| **Landseed Calculator** | [landseed.com/calculator](https://landseed.com/calculator) | Scoring engine + interactive globe. 18 remote sensing sources, 35 indicators, 6 SEEA EA dimensions. |
| **Earth Markets** | [earthmarkets.ai](https://earthmarkets.ai) | Prediction markets for ecological outcomes. 54 live markets. |
| **NRD-DAO Atlas** | [landseed.com/nrd-dao](https://landseed.com/nrd-dao) | Three-layer legal architecture for Nature Rights Deeds — 7 templates, 5 jurisdictions. |
| **Earth Dashboard** | [landseed.earth/dashboard](https://landseed.earth/dashboard) | Real-time planetary intelligence — 7 Earth system modules, Three.js globe, multi-model AI. |
| **Pitch Deck** | [landseed.com/deck](https://landseed.com/deck) | Full scrolling deck — thesis, NRD, Earth Credits, measurement, market opportunity. |
| **Platform Walkthrough** | [landseed.earth/walkthrough](https://landseed.earth/walkthrough) | Guided walkthrough with embedded 109-second demo video. |
| **EC-M-1.1 Methodology** | [landseed.com/methodology](https://landseed.com/methodology) | Full Earth Credit specification — 32 indicators, 6 SEEA EA dimensions, 9 ecosystems. |

## Repository Map

### Core Methodology & Writing
| Repo | What It Is |
|------|-----------|
| [knowledge-base](knowledge-base) | **Start here.** Source of truth — EC-M-1.1 methodology, Nature Rights Deed spec, data specs |
| [earth-credit-package](earth-credit-package) | Complete deliverable — methodology + two 18-month financial projections |
| [writing](writing) | Published writing — The Unauditable Market, NURJ conservation paper, Nature Rights Deed v1.2. The intellectual foundation. |

### Live Infrastructure
| Repo | What It Is |
|------|-----------|
| [landseed-portal](landseed-portal) | NDA-gated centralized asset directory. Cloudflare Pages + Functions middleware. |
| [landseed-calculator](landseed-calculator) | **Most mature product.** EC-M-1.1 scoring engine — 18 remote sensing sources, 35 indicators, PGM aggregation, Three.js globe dashboard. |
| [earth-markets](earth-markets) | Prediction markets — Three.js globe, Supabase, Cloudflare Workers. 54 live markets. |
| [nrd-dao-atlas](nrd-dao-atlas) | NRD-DAO Atlas — Three-layer legal architecture visualization. Cloudflare Pages. |
| [landseed-deck](landseed-deck) | Pitch Deck v5 — full scrolling deck. Cloudflare Pages. |
| [landseed-walkthrough](landseed-walkthrough) | Platform walkthrough + 109-second demo video. Cloudflare Pages. |
| [landseed-earth-dash](landseed-earth-dash) | Earth Dashboard frontend — Three.js globe, 7 Earth system modules, multi-model AI. Cloudflare Pages. |
| [landseed-dashboard](landseed-dashboard) | Simulated portfolio — 10-property analysis, financials, risk framework. |
| [methodology-site](methodology-site) | EC-M-1.1 publication site for partners and auditors. Cloudflare Pages. |

### Agents & Automation
| Repo | What It Is |
|------|-----------|
| [captain-landseed](captain-landseed) | Embodied Company Agent (ECA) — 10-stage pipeline, 22 data adapters, 16-persona deliberation council. |
| [landseed-agents](landseed-agents) | Public agent fleet (Verifier / Methodologist / Captain) + operator-only MCP gateway. |
| [Earth-Signals](Earth-Signals) | Structured ecological data products for markets, research, risk, and discovery. |

### Hardware & R&D
| Repo | What It Is |
|------|-----------|
| [earth-pulse-node](earth-pulse-node) | Sensor cluster hardware spec — $2K-$3.8K base node, LoRaWAN + satellite, edge AI. Pre-deployment. |
| [earth-scanner](earth-scanner) | R&D validation — 26 research threads, 10 pressure tests, Monte Carlo simulations. Stress-tests EC-M-1.1. |

### Infrastructure & Routing
| Repo | What It Is |
|------|-----------|
| [landseed-router](landseed-router) | Cloudflare Worker on landseed.earth/* — path-prefix proxy to Pages backends. |
| [landseed-com-router](landseed-com-router) | Cloudflare Worker on landseed.com/* — NDA-gated proxy to confidential Pages. |
| [landseed-enter](landseed-enter) | Password gate for landseed.com — first layer of two-tier auth. |
| [earth-dashboard](earth-dashboard) | Earth Dashboard API Worker (46 endpoints). |

### Brand & Media
| Repo | What It Is |
|------|-----------|
| [assets](assets) | Brand system (Grand Army, Spring 2026) — logos, pitch decks, email signatures |
| [demo-video](demo-video) | 109-second cinematic demo — Remotion v4 + Three.js, every frame is code |

### Legal & Governance
| Repo | What It Is |
|------|-----------|
| [NRD-DAO](NRD-DAO) | Bifurcation of the Nature Rights Deed — lightweight legal anchor + per-property modular DAO. |
| [landseed-onboarding](landseed-onboarding) | Landowner onboarding workflow — Deed and Stewardship Agreement generation. |
| [landseed-registry](landseed-registry) | Public verification ledger of EC-M-1.1 assessments. |

## Architecture

```
Satellite Sources (18)              Earth Scanner (LiDAR, future)
  MODIS, SoilGrids, GBIF,                    |
  NASA POWER, FIRMS, GloFAS,                 |
  CAMS, WDPA, GFW, OSM,                     |
  ORNL DAAC, iNaturalist,                    v
  Ecoregions, Sentinel-2,          Earth Pulse Node (continuous)
  ERA5, CHIRPS, WorldClim                    |
        |                                    v
   Landseed Calculator (Cloudflare Worker — 35 indicators, 6 dimensions)
        |
        v
   EC-M-1.1 Scoring → ECI (Penalized Geometric Mean)
        |
        +---> Earth Credits (Acres x ECI_conservative x Threat Multiplier)
        +---> Earth Markets (prediction markets — earthmarkets.ai)
        +---> Nature Rights Deed (legal instrument — severable property right)
```

## Scoring Formula (EC-M-1.1)

```
ECI = GM(D1', ..., Dn') x (1 - (sigma/mu)^2)

Where:
  Di' = max(Di, 0.05)       floor prevents zero-collapse
  GM = geometric mean        rewards balance across dimensions
  P = (sigma/mu)^2          imbalance penalty

Credits = Verified Acres x ECI_conservative x Threat_Multiplier
```

## Key Numbers

| Metric | Value |
|--------|-------|
| Methodology | EC-M-1.1 |
| Data sources | 18 (17 no-auth + 1 OAuth) |
| Indicators measured | 35 |
| SEEA EA dimensions | 6 |
| Validation biomes | 4 (tropical, temperate, desert, urban) |
| All-in cost per acre/year | $5-$15 (hardware path) |

## Team

- **Alex Roessner** — Co-founder, Co-CEO. Strategy, markets, AI workflows, infrastructure.
- **Greg Curtis** — Co-founder, Co-CEO. Former Deputy General Counsel, Patagonia. Inventor of the Nature Rights Deed.

## Contact

- Email: outreach@landseed.earth

---

*Dual-remote: [GitHub](https://github.com/landseed-pbc) + [Forgejo](https://forge.aroessner.com/Landseed-PBC). Both kept in sync.*
