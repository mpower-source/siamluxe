# Architecture

## System Design

### Single-Page Application (SPA)

The Command Center is a lightweight SPA with no framework dependencies. It uses:
- **DOM manipulation** via vanilla JavaScript
- **CSS Grid/Flexbox** for responsive layout
- **sessionStorage** for temporary data persistence
- **Anthropic API** for AI chat functionality

### Core Structure

```
HTML Document
├── <head>
│   ├── CSS custom properties (color palette, spacing)
│   ├── Component styles (.panel, .card, .grid-*)
│   └── Layout styles (.main, .nav-bar, .masthead)
├── <body>
│   ├── Masthead (title, phase, date)
│   ├── Navigation tabs
│   ├── Main content area (.main)
│   │   └── Panels (.panel - hidden/shown via CSS class)
│   └── Chat panel (fixed position, hidden by default)
└── <script>
    ├── State (PRODUCTS, DROPS, TEAM, DOC_CONTENT)
    ├── Panel functions (showPanel, buildTeamGrid)
    ├── Data functions (buildProductTable, buildDropTable, etc.)
    └── Chat functions (openChat, sendMessage, etc.)
```

## Panel System

### How Panels Work

1. **HTML Structure**: Each panel is a `<div class="panel" id="panel-{name}">`
2. **CSS Default**: `.panel { display: none; }` (all hidden by default)
3. **Activation**: `.panel.active { display: block !important; }` (shown when active)
4. **JavaScript Trigger**: `showPanel(name)` adds/removes `.active` class

### Active Panels
- Overview (default on page load)
- Pricing
- Drops
- Revenue
- Risks
- Team
- Docs

### Known Issue: Panel Rendering
**Status**: Non-functional panels (Risks & Gaps, AI Team) do not display when clicked
**Symptoms**: Tab highlights but panel content remains invisible
**Root Cause**: Artifact viewer rendering constraints (being debugged with Claude Code)
**Workaround**: None currently; full debugging required in local environment

## State Management

### Data Objects

**PRODUCTS** - Array of 7 hero pieces
```javascript
{ name, category, tier, ws (wholesale), retail, units }
```

**DROPS** - Array of 12 drop names
```javascript
"Drop 01 — Monaco", "Drop 02 — Capri", ...
```

**TEAM** - Array of 8 AI specialists
```javascript
{ id, icon, iconBg, title, role, system (prompt), prompts: [] }
```

**DOC_CONTENT** - Object with 5 reference documents
```javascript
{ brain, brand, instagram, week1, drops }
```

### Session Storage

- `sl-tasks` — Task completion status (JSON array)
- `sl-drops` — Drop performance data (JSON array)
- Data persists only during browser session; clears on page close

## Chat System

### AI Team Integration

Each specialist has:
- **System Prompt** — Role and context for Claude API
- **Suggested Prompts** — Pre-written questions
- **Custom Input** — User can type any question

### Chat Flow

1. User clicks a specialist card or suggested prompt
2. `openChat(id, prompt)` opens chat panel
3. User message sent to Anthropic Messages API
4. Response parsed and displayed in chat
5. Conversation history maintained in `chatHistory` array

### API Details

**Endpoint**: `https://api.anthropic.com/v1/messages`
**Model**: `claude-sonnet-4-20250514`
**Max Tokens**: 1000
**Headers**: Content-Type: application/json

## Component System

### CSS Classes (Utilities)

**Grids**
- `.grid-2` — 2-column responsive grid
- `.grid-3` — 3-column responsive grid
- `.grid-4` — 4-column grid
- `.grid-12` — 1/2 ratio layout

**Cards**
- `.card` — White card with border
- `.card-dark` — Dark background card
- `.card-sand` — Sand-colored card
- `.metric-card` — Centered metric display

**UI Elements**
- `.btn` — Default button
- `.btn-dark` — Dark button
- `.badge-*` — Status badges (critical, high, medium, done)
- `.toast` — Notification toast
- `.divider` — Visual separator

### Theme Variables

Defined in `:root`:
- **Neutral**: `--black`, `--mocha`, `--warm-g`, `--sand`, `--linen`, `--white`
- **Semantic**: `--green`, `--amber`, `--red` (+ backgrounds)
- **Borders**: `--border`
- **Text**: `--body-text`

## Responsive Design

### Breakpoints

- **Mobile** (< 900px): Single column grids
- **Desktop** (≥ 900px): Multi-column grids

### Layout Constraints

- Max width: 1280px
- Padding: 28-40px
- Gap: 12-20px

## Performance Considerations

1. **No Dependencies** — No npm, no build step, instant load
2. **Inline Styles** — CSS embedded in HTML (no external files)
3. **Browser Storage** — sessionStorage only (no server)
4. **API Calls** — Only on user action (chat messages)
5. **DOM Updates** — Minimal, targeted updates (not full page refresh)

## Security & Limitations

1. **API Key Exposure** — None (API calls proxied through artifact viewer or local server)
2. **Data Privacy** — All data client-side only; no server storage
3. **Browser Compatibility** — Modern browsers only (ES6+, CSS Grid)
4. **Session Scope** — Data cleared on browser close

## File Size

- **HTML**: ~3.6 MB (includes embedded data + CSS + JS)
- **Load Time**: Instant (single file)
- **Browser Memory**: ~5-10 MB depending on browser

## Deployment

### As Artifact (claude.ai)
- Hosted directly in Claude artifact viewer
- No server required
- Private link sharing

### As GitHub Pages
```bash
git push origin main
# Enable Pages in repository settings
# Site: https://username.github.io/siam-luxe-command-center
```

### Local Server
```bash
python3 -m http.server 8000
# Open: http://localhost:8000
```

## Debugging Points

See `DEBUGGING.md` for:
- Console errors
- Network issues
- Panel rendering problems
- Browser compatibility notes
