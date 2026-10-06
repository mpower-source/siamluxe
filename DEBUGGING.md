# Debugging Guide

Comprehensive troubleshooting and debugging strategies for the Siam Luxe Command Center.

## Resolved Issues (October 2026)

The two panel issues below are fixed. The notes under "Known Issues" are kept as a record of the original investigation.

- **Risks & Gaps and AI Team panels not displaying** — Root cause was malformed HTML, not the artifact viewer. The `.dl-grid` container and `#panel-documents` were never closed, so `#panel-risks` and `#panel-team` were nested inside the All Documents panel and stayed hidden with it. Fix: added the two missing closing `</div>` tags, and removed the debugging overrides (`.panel.active > *` forcing `display: block`, inline styles set in `showPanel`) that had been added while chasing the bug.
- **Page rendering unstyled** — The opening `<style>` tag was missing from `<head>`. Restored.
- **AI Team chat failing outside the artifact viewer** — The page called the Anthropic API with no credentials. The chat panel now asks for an Anthropic API key at runtime, keeps it in `sessionStorage` (`sl-api-key`) for the browser tab only, and shows the API's error message when a request fails. No key is stored in the repository.

## Known Issues

### Issue 1: Risks & Gaps Panel Not Displaying

**Status**: ✅ Resolved (see above)

**Symptoms**:
- Tab highlights when clicked, indicating JavaScript is responding
- Panel content does not appear (no cards, no text)
- No console errors visible
- Other panels (Overview, Pricing, Drops, Revenue, Docs) work correctly

**HTML Structure** (Line 1646-1684):
```html
<div class="panel" id="panel-risks">
  <div class="panel-header">
    <h2>Risks & Gaps</h2>
  </div>
  <div class="grid-4">
    <!-- 4 cards with risk data -->
  </div>
</div>
```

**CSS Rules Applied**:
```css
.panel { display: none; }
.panel.active { display: block !important; width: 100% !important; }
```

**JavaScript Activation** (showPanel function, line 1762-1787):
- Removes `.active` class from all panels
- Adds `.active` class to target panel
- Sets multiple inline styles for safety

**Test Case 1 — Manual DOM Check**:
```javascript
// In browser console, click "Risks & Gaps" tab, then run:
const risksPanel = document.getElementById('panel-risks');
console.log('Panel exists:', !!risksPanel);
console.log('Has active class:', risksPanel.classList.contains('active'));
console.log('Display style:', getComputedStyle(risksPanel).display);
console.log('Visibility:', getComputedStyle(risksPanel).visibility);
console.log('Opacity:', getComputedStyle(risksPanel).opacity);
console.log('Height:', getComputedStyle(risksPanel).height);

// If display is 'none', the CSS !important rule is not being applied
// If display is 'block' but hidden, check visibility and opacity
```

**Test Case 2 — Check for CSS Override**:
```javascript
// See if any other CSS is overriding .panel.active
const styles = window.getComputedStyle(document.getElementById('panel-risks'));
console.log('All inline styles:', document.getElementById('panel-risks').getAttribute('style'));
console.log('Computed display:', styles.display);
console.log('Computed visibility:', styles.visibility);
console.log('Computed opacity:', styles.opacity);
console.log('Computed position:', styles.position);
console.log('Computed z-index:', styles.zIndex);
```

**Possible Root Causes**:
1. **CSS specificity issue** — Artifact viewer may have wrapper CSS that overrides `.panel.active`
2. **JavaScript not executing** — showPanel() function not being called or panel ID mismatch
3. **Browser rendering constraint** — Artifact viewer may limit CSS display property changes
4. **DOM structure issue** — Panel HTML missing or malformed
5. **Z-index stacking** — Panel exists but is behind other elements

**Debugging Strategy**:
1. Run Test Case 1 to confirm panel exists and .active class is applied
2. Run Test Case 2 to check computed styles vs declared styles
3. If display: block is applied but panel doesn't show, check z-index and parent container styles
4. If display remains none, CSS override is likely — inspect artifact viewer wrapper

### Issue 2: AI Team Panel Not Displaying

**Status**: ✅ Resolved (see above)

**Symptoms**:
- Same as Risks & Gaps panel — tab highlights but no content appears
- No JavaScript errors in console
- Chat functionality may work (if accessed through API directly)
- buildTeamGrid() function exists but output is invisible

**HTML Structure** (Line 1687-1696):
```html
<div class="panel" id="panel-team">
  <div class="panel-header">
    <h2>AI Team</h2>
  </div>
  <div class="team-grid"></div>
</div>
```

**JavaScript Build** (buildTeamGrid function, line 2192-2227):
```javascript
const teamGrid = document.querySelector('.team-grid');
teamGrid.innerHTML = ''; // Clear existing

TEAM.forEach(specialist => {
  const card = document.createElement('div');
  card.className = 'card team-card';
  card.innerHTML = `
    <div class="icon">${specialist.icon}</div>
    <div class="title">${specialist.title}</div>
    ...
  `;
  teamGrid.appendChild(card);
});
```

**Test Case 1 — Verify Team Grid Population**:
```javascript
// Click AI Team tab, then run:
const teamGrid = document.querySelector('.team-grid');
console.log('Team grid exists:', !!teamGrid);
console.log('Number of cards in grid:', teamGrid.children.length);
console.log('First card HTML:', teamGrid.children[0]?.outerHTML);

// Should show 8 cards if buildTeamGrid() executed successfully
```

**Test Case 2 — Check Panel Visibility**:
```javascript
// Same as panel-risks, but for panel-team
const teamPanel = document.getElementById('panel-team');
console.log('Panel exists:', !!teamPanel);
console.log('Has active class:', teamPanel.classList.contains('active'));
console.log('Display:', getComputedStyle(teamPanel).display);
console.log('Inner grid display:', getComputedStyle(teamPanel.querySelector('.team-grid')).display);
```

**Possible Root Causes**:
- Same as Risks & Gaps panel (CSS display issue)
- buildTeamGrid() may not be called on tab click
- Grid layout CSS may have issues on artifact viewer

**Debugging Strategy**:
1. Run Test Case 1 to verify cards are in DOM
2. Run Test Case 2 to check both panel and inner grid visibility
3. If cards exist but hidden, same CSS override issue as panel-risks
4. If no cards exist, buildTeamGrid() is not being called

## Testing Procedures

### Procedure 1: Verify All Panels Load in DOM

```javascript
// Run in console on page load (before clicking any tabs)
const panels = ['panel-overview', 'panel-pricing', 'panel-drops', 'panel-revenue', 'panel-risks', 'panel-team', 'panel-docs'];
panels.forEach(id => {
  const panel = document.getElementById(id);
  console.log(`${id}: exists=${!!panel}, hasContent=${panel?.children.length > 0}`);
});
```

**Expected output**:
```
panel-overview: exists=true, hasContent=true
panel-pricing: exists=true, hasContent=true
panel-drops: exists=true, hasContent=true
panel-revenue: exists=true, hasContent=true
panel-risks: exists=true, hasContent=true
panel-team: exists=true, hasContent=true
panel-docs: exists=true, hasContent=true
```

### Procedure 2: Test Tab Click Handler

```javascript
// Manually click "Risks & Gaps" tab, then check:
const risksTab = document.querySelector('[onclick*="risks"]'); // or inspect to find exact selector
console.log('Risks tab exists:', !!risksTab);
console.log('Tab has click handler:', !!risksTab?.onclick);

// Or manually call showPanel directly:
showPanel('risks');
console.log('After showPanel("risks"):', getComputedStyle(document.getElementById('panel-risks')).display);
```

### Procedure 3: Check CSS Cascade

```javascript
// Get all CSS rules affecting .panel
const stylesheet = document.styleSheets[0]; // Main embedded stylesheet
const rules = stylesheet.cssRules;
let panelRules = [];
for (let rule of rules) {
  if (rule.selectorText && rule.selectorText.includes('panel')) {
    panelRules.push({
      selector: rule.selectorText,
      display: rule.style.display,
      important: rule.style.cssText.includes('!important')
    });
  }
}
console.log('Panel CSS rules:', panelRules);
```

### Procedure 4: Check Artifact Viewer Wrapper

If using Claude artifact viewer, check for wrapper constraints:

```javascript
// Check parent containers
let parent = document.getElementById('panel-risks').parentElement;
let depth = 0;
while (parent && depth < 10) {
  console.log(`Parent ${depth}:`, parent.tagName, parent.id, parent.className);
  console.log(`  Display: ${getComputedStyle(parent).display}`);
  parent = parent.parentElement;
  depth++;
}

// Look for wrapper divs that might have display: none or overflow: hidden
```

## Common Solutions

### Solution 1: Force Display via Console

If panels exist in DOM but won't display:

```javascript
// Quick test — make Risks panel visible
const risksPanel = document.getElementById('panel-risks');
risksPanel.style.display = 'block';
risksPanel.style.visibility = 'visible';
risksPanel.style.opacity = '1';
risksPanel.style.pointerEvents = 'auto';
risksPanel.classList.add('active');

// If this works, CSS rules need adjustment
```

### Solution 2: Check JavaScript Execution

```javascript
// Verify showPanel function exists
console.log('showPanel function:', typeof showPanel);

// Manually trigger it
if (typeof showPanel === 'function') {
  showPanel('risks');
  console.log('showPanel executed');
} else {
  console.log('showPanel function not found');
}
```

### Solution 3: Rebuild Panel HTML

If panels are corrupted in DOM:

```javascript
// Reload the page to rebuild from HTML
location.reload();

// After reload, check DOM again
```

## Network Debugging

### Check API Calls

For AI Team chat functionality:

```javascript
// Open DevTools > Network tab
// Click on an AI specialist
// Look for POST request to: https://api.anthropic.com/v1/messages
// Check:
// - Request headers (Authorization, Content-Type)
// - Request body (model, messages, max_tokens)
// - Response status (should be 200)
// - Response body (should contain assistant message)
```

### Check sessionStorage

```javascript
// View stored data
console.log('Tasks:', JSON.parse(sessionStorage.getItem('sl-tasks')));
console.log('Drops:', JSON.parse(sessionStorage.getItem('sl-drops')));

// Clear storage if needed
sessionStorage.clear();
location.reload();
```

## Performance Profiling

### Measure Panel Rendering Time

```javascript
// Before clicking tab
console.time('showPanel');
showPanel('risks');
console.timeEnd('showPanel');

// Should complete in < 50ms if CSS display toggle is working
```

### Check Memory Usage

In Chrome DevTools > Memory tab:
1. Take heap snapshot before opening panels
2. Click each panel
3. Take another snapshot
4. Compare to identify memory leaks

## Reproduction Steps

### To Reproduce Issue 1 (Risks & Gaps Not Displaying)

1. Open `http://localhost:8000` in Chrome
2. DevTools > Console (keep open)
3. Click "Risks & Gaps" tab
4. Observe: Tab highlights but panel doesn't appear
5. Run: `console.log(getComputedStyle(document.getElementById('panel-risks')).display);`
6. Expected: `block` (but likely shows `none`)

### To Reproduce Issue 2 (AI Team Not Displaying)

1. Open `http://localhost:8000` in Chrome
2. Click "AI Team" tab
3. Observe: Tab highlights but cards don't appear
4. Run: `console.log(document.querySelector('.team-grid').children.length);`
5. Expected: `8` (if cards were built)

## When to Escalate

If debugging shows:
- ✅ Panel exists in DOM
- ✅ .active class is applied
- ✅ CSS rule `display: block !important` should apply
- ❌ But computed style still shows `display: none`

Then the issue is likely **CSS override at artifact viewer level** and requires architectural changes or migration to local environment for proper testing.

## Next Steps

1. Run all Test Cases in local environment (http://localhost:8000)
2. Document findings in Console output
3. Share results: panel existence, active class state, computed styles
4. Based on findings, determine if issue is:
   - **JavaScript** (showPanel not running) → Fix event handlers
   - **CSS** (rules not applying) → Fix CSS specificity
   - **Artifact Viewer** (wrapper constraining) → Requires local environment
5. Implement fix and re-test all panels
