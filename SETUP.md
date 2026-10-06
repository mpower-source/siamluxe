# Local Development Setup

Complete instructions for running the Siam Luxe Command Center locally with Claude Code.

## Prerequisites

- Modern browser (Chrome, Firefox, Safari, Edge)
- Python 3.6+ (for local HTTP server)
- Git (optional, for version control)
- Text editor (VS Code, Sublime, etc.)

## Installation

### 1. Clone or Download the Repository

If using Git:
```bash
git clone <github-repo-url>
cd siam-luxe-command-center
```

Or download the files directly and extract to a local folder.

### 2. Verify File Structure

Ensure these files are present:
```
siam-luxe-command-center/
├── index.html                    # Main application
├── README.md                      # Project overview
├── ARCHITECTURE.md                # Technical documentation
├── PANELS.md                      # Panel reference
├── AI_TEAM.md                     # AI specialists
├── SETUP.md                       # This file
└── DEBUGGING.md                   # Troubleshooting
```

## Running Locally

### Option 1: Python HTTP Server (Recommended for Claude Code)

```bash
# Navigate to the project directory
cd siam-luxe-command-center

# Start the HTTP server
python3 -m http.server 8000

# Output should show:
# Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Then open in browser:
- `http://localhost:8000`

### Option 2: Node HTTP Server

If you prefer Node:
```bash
npm install -g http-server
http-server . -p 8000
```

### Option 3: Using Claude Code with Local Server

From Claude Code terminal:
```bash
python3 -m http.server 8000
```

Then use Claude Code's browser tools to inspect `http://localhost:8000`

## Browser Developer Tools Setup

### Chrome DevTools
1. Open `http://localhost:8000` in Chrome
2. Press `Ctrl+Shift+I` (Windows/Linux) or `Cmd+Option+I` (Mac)
3. Go to **Elements** tab to inspect `.panel-risks` and `.panel-team`
4. Go to **Console** to check for JavaScript errors
5. Go to **Network** to verify API calls and resource loads

### Inspecting Panel Rendering

To debug the non-displaying panels:

1. **Open Console** and run:
```javascript
// Check if panels exist in DOM
console.log('Risks panel:', document.getElementById('panel-risks'));
console.log('Team panel:', document.getElementById('panel-team'));

// Check active classes
console.log('Risks active:', document.getElementById('panel-risks')?.classList.contains('active'));
console.log('Team active:', document.getElementById('panel-team')?.classList.contains('active'));

// Check computed styles
const risksPanel = document.getElementById('panel-risks');
if (risksPanel) {
  console.log('Display:', getComputedStyle(risksPanel).display);
  console.log('Visibility:', getComputedStyle(risksPanel).visibility);
  console.log('Opacity:', getComputedStyle(risksPanel).opacity);
}
```

2. **Inspect the panel HTML** in Elements tab:
   - Look for `<div class="panel active" id="panel-risks">`
   - Check if inline styles are being applied
   - Verify CSS classes are present

3. **Check for console errors**:
   - Look for red error messages
   - Check network tab for failed API calls
   - Look for CSS parsing issues

## Testing the AI Team Chat

1. Click on any AI specialist card
2. Check the console for fetch request to Anthropic API
3. Verify response is received (should see JSON in Console > Network > Preview)
4. Confirm chat message appears in the chat panel

If chat is not working:
- Check that API calls are reaching `https://api.anthropic.com/v1/messages`
- Verify the Anthropic API key is properly configured
- Check for CORS errors in the console

## Troubleshooting Common Issues

### Page Loads But Panels Don't Display
- See DEBUGGING.md for panel rendering troubleshooting
- Check browser console for JavaScript errors
- Verify CSS display rules in Elements inspector

### Chat Not Working
- Check Network tab for failed API calls
- Verify Anthropic API endpoint is accessible
- Look for authentication/header errors in Console

### Styling Issues
- Clear browser cache: `Ctrl+Shift+Delete` (or `Cmd+Shift+Delete` on Mac)
- Hard refresh page: `Ctrl+F5` (or `Cmd+Shift+R` on Mac)
- Check for CSS conflicts in Elements inspector

### Page Freezes or Crashes
- Check Console for infinite loops or errors
- Reduce sessionStorage data by clearing via DevTools > Application > Session Storage > Delete
- Restart the server: Stop `http.server` and restart

## Local Testing Checklist

- [ ] Server running at `http://localhost:8000`
- [ ] Page loads without errors
- [ ] Overview panel displays (default tab)
- [ ] All 7 tabs are clickable (Overview, Pricing, Drops, Revenue, Risks, Team, Docs)
- [ ] Pricing panel shows 7 products
- [ ] Drops panel shows 12 drop names
- [ ] Revenue Model shows 6-month chart
- [ ] Docs panel shows 5 downloadable files
- [ ] Risks panel displays 4 cards (currently debugging)
- [ ] AI Team panel displays 8 specialist cards (currently debugging)
- [ ] Click a specialist to open chat
- [ ] Type a message in chat and receive response

## Performance Notes

- **Page Load**: Should be instant (single HTML file, ~3.6 MB)
- **Memory Usage**: ~5-10 MB depending on browser
- **Chat Latency**: Depends on network and Anthropic API response time (typically 1-3 seconds)
- **Storage**: sessionStorage only (cleared on browser close)

## Next Steps

Once the application is running locally:
1. Use browser DevTools to identify the panel rendering issue
2. Reference DEBUGGING.md for specific test cases
3. Make changes to `index.html` and refresh browser to test
4. Document any fixes and commit to Git

For detailed architecture and design, see `ARCHITECTURE.md`.
