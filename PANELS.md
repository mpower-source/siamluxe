# Panels Reference

Complete documentation of each Command Center panel.

## Overview Panel (default)

**Purpose**: Quick snapshot of business health and phase timeline

### Key Metrics
- **Cash on Hand** — Current capital (manual input)
- **Units Sold** — Cumulative across drops
- **Total Revenue** — Cumulative in THB and USD
- **Avg Sell-Through** — Across all drops with color coding (green ≥80%, amber 50-79%, red <50%)

### Phase Timeline
Shows current position in 4-phase roadmap:
- **Phase 1** (Current): Curated resale, DM-based, limited drops
- **Phase 2**: Email list, paid ads, supplier relationships
- **Phase 3**: Private label intro, international expansion
- **Phase 4**: Recognizable brand, scaled operations

### Recent Tasks
Prioritized task list with priority badges:
- 🔴 Critical (red)
- 🟠 High (amber)
- 🟢 Medium (green)
- ✓ Done (gray)

Tasks include:
- Supplier backup identification (Critical)
- Logistics testing with Kerry + DHL (Critical)
- First 10 buyers as VIPs (High)
- Email list setup with Klaviyo (High)
- Private label roadmap (Medium)

### Reference Docs
Quick access to:
- Master Brain File (full strategic guide)
- Brand Identity Brief (visual/tone standards)
- Instagram Strategy (content pillars, calendar)
- Week 1 Checklist (launch preparation)
- Drop System (repeat drop playbook)

---

## Pricing Panel

**Purpose**: Product catalog, wholesale/retail tracking, margin analysis

### Product Table
7 products with editable unit quantities:
- **The Monaco Dress** (backless, hero, ฿400 WS → ฿1,800 retail)
- **The Asoke Set** (one-shoulder, hero, ฿700 → ฿2,800)
- **The Riviera Dress** (backless, hero, ฿400 → ฿1,800)
- **The Siena Dress** (flow, secondary, ฿400 → ฿1,600)
- **The Soho Set** (lounge, secondary, ฿700 → ฿2,400)
- **Bundle: The Edit** (hero bundle, ฿1,100 → ฿4,200)
- **Bundle: The Weekend** (lifestyle bundle, ฿1,100 → ฿3,800)

### Columns
- **Product Name** (tier badge: hero, secondary, bundle)
- **Category** (dress type, set type, bundle)
- **Tier** (visual indicator)
- **Wholesale Cost** (฿)
- **Retail Price** (฿)
- **Units** (editable, updates summary)
- **Markup** (colored: green ≥5×, amber 4-5×, red <4×)

### Summary Metrics
- **Total Units** — Sum of all products
- **Total Revenue** — Retail value of all units (฿ + USD conversion)

---

## Drops Panel

**Purpose**: Track performance of 12 sequential drops, measure sell-through and margin

### Drop Tracker Table
Columns:
- **Drop Name** (Monaco, Capri, Marrakech, Kyoto, Amalfi, Bali, Santorini, Positano, Tulum, Mykonos, Ibiza, Maldives)
- **Bought** (units purchased from supplier)
- **Sold** (units actually sold)
- **Revenue** (฿)
- **COGS** (cost of goods sold, ฿)
- **Gross Profit** (Revenue - COGS, ฿)
- **Sell-Through %** (Sold ÷ Bought, colored)
- **Revenue USD** (converted at live FX rate)

### Metrics Row
- **Drops Run** — # of drops with sales data
- **Total Units Sold** — Cumulative across all drops
- **Total Revenue** — Cumulative (฿ + USD)
- **Avg Sell-Through** — Weighted average ST%

### FX Converter
Live exchange rate selector (hardcoded at ~36 THB/USD, editable for testing)

### Data Management
- **Clear All** button resets drop data to empty
- All inputs auto-save to sessionStorage
- Color coding: green ≥80% ST, amber 50-79%, red <50%

---

## Revenue Model Panel

**Purpose**: Project cash flow and revenue growth over 6 months

### Inputs (Left Side)
- **Starting Units/Month** — Base volume (default: 5)
- **Monthly Growth %** — Compound growth rate (default: 15%)
- **Avg Retail Price** — Per unit (default: ฿2,000)

### Output Chart (Center)
Bar chart showing 6 months of:
- **Month label** (M1–M6)
- **Revenue (฿)** — Total monthly revenue
- **Revenue (USD)** — FX-converted
- **Net Profit** — After COGS and operating expenses

### Calculation Logic
- **Revenue** = Units × Price × Growth factor
- **COGS** — Avg wholesale cost ฿520/unit
- **OpEx** — ฿130/unit + 5% of revenue + ฿3,400 fixed
- **Net** — Revenue - COGS - OpEx

---

## Risks & Gaps Panel

**Status**: ⚠️ Currently not displaying (artifact viewer issue)

**Purpose**: Comprehensive risk register and mitigation roadmap

### Sections (Grid of 4 Cards)

#### 1. Critical Risks
- Single-supplier dependency (Mitigation: backup at Platinum by Drop 03)
- No logistics infrastructure (Mitigation: Kerry + DHL before public launch)
- Zero social proof at launch (Mitigation: VIP treatment for first 10 buyers)
- Trademark not filed (Mitigation: file USPTO before scale, ~$300)

#### 2. Structural Risks
- DM model doesn't scale (Mitigation: build email list from Day 1)
- No owned customer data (Mitigation: Klaviyo email capture)
- Model is easily replicated (Mitigation: brand/story/relationships as moat)
- Quiet luxury trend peaking (Mitigation: Thai provenance + DM relationship)

#### 3. Strategic Gaps (Brain File §19)
- No fulfillment/logistics plan (Covered in Week 1 Checklist)
- No retention system (Drop System §06: VIP tiers + email)
- No email/SMS marketing (Klaviyo free tier + sequences)
- No paid ads testing (Brain File §30: Phase 3 entry)
- No brand guideline system (✓ Resolved — Brand Identity Brief created)

#### 4. Phase Gate Checklist
Move to next phase ONLY after passing gates for 6+ consecutive weeks:
- **Phase 1 → 2**: 3 sell-outs · 50+ email subscribers · logistics working
- **Phase 2 → 3**: $10K/mo consistent · website live · 3+ influencer collabs
- **Phase 3 → 4**: $25K/mo · ROAS >4× · supplier reordered 10+ times

---

## AI Team Panel

**Status**: ⚠️ Currently not displaying (artifact viewer issue)

**Purpose**: Access to 8 specialized advisors for strategic guidance

### AI Specialists (8 roles)

#### 1. Social Media Manager 📱
- **Role**: Instagram content calendar, Reels, Stories
- **Sample Prompts**:
  - Write 5 caption options for the Monaco Dress (feed post)
  - Plan this week's Instagram Stories schedule
  - Write the Drop 02 reveal caption + 3 story slides
  - Give me 10 Reel concepts for the next 5 drops

#### 2. Brand Copywriter ✍️
- **Role**: Product descriptions, emails, captions, brand voice
- **Sample Prompts**:
  - Write product descriptions for all 5 hero pieces
  - Draft early access email for Drop 03
  - Write About page copy (< 120 words)
  - Rewrite this caption in Siam Luxe voice

#### 3. Creative Director 📷
- **Role**: Photography briefs, shot lists, visual direction, moodboards
- **Sample Prompts**:
  - Write full shoot brief for Drop 02 (poolside, 3 pieces)
  - Give me a 16-shot production list for hotel room shoot
  - Describe exact Lightroom editing preset for Siam Luxe
  - Write moodboard description for Riviera Dress campaign

#### 4. Web & Graphic Designer 🎨
- **Role**: Shopify design, Canva templates, packaging, brand system
- **Sample Prompts**:
  - Design the Linktree page layout and copy
  - Give me exact Canva specs for all Story Highlight covers
  - Write Shopify product page template (sections, copy order)
  - Describe custom hang tag design (front/back, dimensions)

#### 5. DM Sales Specialist 💬
- **Role**: Outreach scripts, objection handling, close sequences
- **Sample Prompts**:
  - Write opening DMs for 3 customer profiles
  - Give me 5 responses for "it's too expensive"
  - Write full DM sequence from contact to post-delivery
  - Draft 10 follow-up DMs for cold leads

#### 6. Influencer & PR Manager 🌟
- **Role**: Influencer outreach, gifting, press kit, PR pitches
- **Sample Prompts**:
  - Write Instagram DM to pitch gifting to Bangkok lifestyle influencer
  - Draft press pitch to Tatler Asia for launch story
  - Write handwritten gift note for Monaco Dress
  - Give me 10-point criteria for evaluating influencer fit

#### 7. Finance & Operations 📊
- **Role**: Cash flow, pricing, tax (US FEIE, Thai VAT), inventory
- **Sample Prompts**:
  - Model cash flow for buying 21 units + Drop 01 + reinvestment
  - What are my US tax obligations for Month 1 earning $3K?
  - Build reorder decision framework (stock vs retire SKU)
  - What operating costs should I track monthly?

#### 8. Brand Strategist 🧭
- **Role**: Competitive positioning, private label roadmap, international expansion
- **Sample Prompts**:
  - How should Siam Luxe defend vs copycats at Platinum?
  - What's the trigger point for private label conversation?
  - Design the 12-month brand calendar with milestones
  - How do we expand to UK market — what changes/stays same?

### Chat Interface
- Each specialist appears in a card with icon, title, role
- Pre-written prompts for quick access
- Custom input field for any question
- Chat panel slides up from bottom
- Full conversation history maintained
- Responses from Claude API (claude-sonnet-4-20250514)

---

## Docs Panel

**Purpose**: Access and download reference documents

### Documents (5 available)

1. **Master Brain File** (CLAUDE.md, ~50KB)
   - Complete strategic playbook
   - Phase roadmap, supplier strategy, pricing logic
   - Content pillars, timeline, metrics

2. **Brand Identity Brief** (BRAND.md, ~30KB)
   - Visual identity system (palette, typography)
   - Brand voice guidelines (tone, language)
   - Logo, packaging, photography standards

3. **Instagram Strategy** (IG.md, ~20KB)
   - Content calendar template
   - 4 content pillars (The Piece, The World, The Source, The Customer)
   - Hashtag strategy, caption formula

4. **Week 1 Checklist** (WK1.md, ~15KB)
   - Day-by-day launch tasks
   - Supplier coordination, logistics setup
   - First buyer onboarding, email capture

5. **Drop System** (DROPS.md, ~25KB)
   - Repeatable drop playbook
   - Timeline (announce → pre-order → ship)
   - Pricing, scarcity messaging, follow-up sequences

### Download Functionality
- Click "Download" button to save .md file locally
- Files are embedded as base64 in HTML
- Auto-names based on document (e.g., `SIAM_LUXE_Master_Brain_File.md`)

---

## Summary

| Panel | Status | Key Feature | Updated |
|-------|--------|-------------|---------|
| Overview | ✅ Working | Metrics + timeline | Real-time |
| Pricing | ✅ Working | Product table | On input |
| Drops | ✅ Working | Performance tracking | On input |
| Revenue | ✅ Working | 6-month projection | On change |
| Risks | ⚠️ Issue | Risk register | Static |
| AI Team | ⚠️ Issue | 8 specialists | Dynamic |
| Docs | ✅ Working | Reference library | Static |

*Note: Risks & Gaps and AI Team panels have a rendering issue with the artifact viewer that is being debugged in Claude Code.*
