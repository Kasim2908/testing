## Stardust Web Client

A static web client for exploring astronomical data using the WorldWide Telescope (WWT) Web Client.

### Repository layout
- **`testing/`**: Deployable static site
  - `index.html`: Main page bootstrapping the WWT web client and custom UI behavior
  - `custom-styles.css`: Additional site styles
  - `favicon.ico`: Site icon
  - `package.json`: Metadata and placeholder scripts (no build step)
  - `vercel.json`: Static hosting configuration for Vercel
  - `README.md`: Component-level notes for the `testing` folder

### How it works
- Loads the WWT SDK and legacy WWT Web Client assets from CDN.
- Uses AngularJS 1.5.x (from CDN) to wire UI controllers already provided by WWT.
- Applies opinionated CSS to simplify the interface and present an "explore" side panel.
- Sets a default view to Mars after load and simplifies the context menu via DOM manipulation.
- Google Analytics is integrated via `gtag.js` in `index.html` (property `G-YWNE29K5CB`).

### Quick start (local)
- Option 1: Open `testing/index.html` directly in a modern browser.
- Option 2: Serve the `testing/` directory with any static server:

```bash
# using Python 3
cd testing
python -m http.server 8080
# then visit http://localhost:8080/
```

```bash
# using Node.js (if you have serve installed)
cd testing
npx serve -p 8080 .
```

Notes:
- The site relies on external CDNs; an active internet connection is required.
- There is no build step. The `package.json` scripts are placeholders for static hosting workflows.

### Deployment
- Vercel: The included `testing/vercel.json` config serves `index.html` for all routes.
  - Connect the repository to Vercel.
  - Set the project root to the `testing/` directory (or configure the framework preset as "Other").
  - Deploy — no build command is required.
- Any static host (GitHub Pages, Netlify, S3, etc.) can serve the `testing/` folder as-is.

### Customization
- Styling: Update `testing/custom-styles.css` to tweak the look-and-feel and UI visibility.
- Default target: In `testing/index.html`, the default view is set via `wwtlib.WWTControl.singleton.gotoTarget3(...)`. Adjust to change the startup body/zoom.
- Analytics: Replace the GA measurement ID in `testing/index.html` if needed.
- Assets: You can host WWT assets yourself, but by default they are loaded from official CDNs.

### Tech stack
- WorldWide Telescope Web Client + WWT SDK (CDN)
- AngularJS 1.5.x (CDN)
- jQuery, Bootstrap, Angular-Strap, jScrollPane (CDN)
- Font Awesome (CDN)

### Troubleshooting
- Blank canvas: Ensure network access to the WWT CDNs.
- Mixed content or CSP issues: Serve over HTTPS and allow the referenced CDNs.
- UI not appearing: Confirm Angular and WWT scripts load without console errors.

### License
MIT
