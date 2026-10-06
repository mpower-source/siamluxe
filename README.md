# Siam Luxe Command Center

A comprehensive dashboard and operational hub for the Siam Luxe luxury fashion brand launch and scaling.

## Overview

The Command Center is a single-page application that consolidates:
- **Real-time metrics** (cash, units, revenue, sell-through rate)
- **Product catalog & pricing** (7 hero pieces with wholesale/retail tracking)
- **Drop management** (12-drop roadmap with performance tracking)
- **Financial modeling** (revenue projections, FX rates, cash flow)
- **Risk & gaps registry** (critical issues, mitigations, phase gates)
- **AI Team** (8 specialized advisors for instant strategic guidance)
- **Reference library** (Master Brain File, Brand Brief, Playbooks, Week 1 Checklist)

## Quick Start

1. Open `index.html` in a modern browser
2. Use the top navigation tabs to switch between panels
3. Click on AI specialists to open live chat conversations
4. All data is stored in browser sessionStorage

## File Structure

```
siam-luxe-command-center/
├── index.html                    # Main application
├── README.md                      # This file
├── ARCHITECTURE.md                # Technical architecture
├── PANELS.md                      # Panel documentation
├── AI_TEAM.md                     # AI specialists reference
├── SETUP.md                       # Local development setup
└── DEBUGGING.md                   # Known issues & troubleshooting
```

## Key Features

### Navigation Tabs
- **Overview** — Key metrics and phase timeline
- **Pricing** — Product catalog with wholesale/retail tracking
- **Drops** — 12-drop roadmap with performance data
- **Revenue Model** — 6-month cash flow projection
- **Risks & Gaps** — Risk register and mitigation checklist
- **AI Team** — 8 specialist advisors
- **Docs** — Reference library with downloadable files

### Panels & Content
See `PANELS.md` for detailed documentation of each panel.

### AI Specialists
See `AI_TEAM.md` for the 8 specialist profiles and their prompt templates.

## Technical Stack

- **Frontend:** Vanilla HTML/CSS/JavaScript (no frameworks)
- **Storage:** sessionStorage (browser session only)
- **API:** Anthropic Messages API (for AI Team chat)
- **Styling:** CSS custom properties (variables), responsive grid layout
- **Data Format:** JavaScript objects (PRODUCTS, DROPS, TEAM, DOC_CONTENT)

## Known Issues

See `DEBUGGING.md` for current issues and workarounds.

## Running Locally with Claude Code

```bash
# Clone and navigate to the directory
cd siam-luxe-command-center

# Start a local server
python3 -m http.server 8000

# Open browser to http://localhost:8000
```

For detailed setup, see `SETUP.md`.

## Project Goals

**Phase 1 (Current):** Curated Thai luxury, DM-based sales, limited drops
**Phase 2:** Build email list, test paid ads, optimize funnel
**Phase 3:** Introduce private label, scale internationally
**Phase 4:** Recognizable brand with consistent suppliers

## Contact & Attribution

Built for Siam Luxe by Claude.
Email: cto@cloudwavconsulting.com
