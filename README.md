# brisko — Automation Workflow Dashboard

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue?style=for-the-badge&logo=github)](https://mrchandrayee.github.io/brisko-automation-dashboard/)
[![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org) [![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org) [![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](./LICENSE)

A responsive, runnable HTML/CSS/JavaScript reconstruction of the supplied 10.57-second screen recording (720 × 1280, 30 fps).

## Run it
1. Extract `brisko-automation-dashboard.zip`.
2. Open `index.html` in Chrome, Edge, Firefox or Safari.
3. No npm install or build step is required.

Optional local server:
```bash
python3 -m http.server 8000
```
Open `http://localhost:8000`.

## Source-video inspection

The recording is titled **Dashboard Animation** and shows a workflow automation product branded **brisko**, inside the **Tallow & Fern** workspace. The theme is a light grey/green dashboard with a nearly black left sidebar and bright lime-green selection accents.

### Main navigation shown
Overview · Scenarios · Runs · Apps · Team · Data · Billing · Learn · Help · Settings

### Overview
The dashboard headline reads: “11 scenarios are running the shop while you plan the day”. Visible metric cards include:
- Operations: 10,298
- Runs: 2,729
- Run success: 68%
- Succeeded: 95.8%
- Days saved: 21

A weekly operations bar chart compares runs and successful runs. The right rail includes operations/data counters, a month-end forecast card and an action to add operations. Lower cards show live runs and upcoming activity.

### Scenarios
The Scenarios page shows:
- 10 scenarios
- 1,897 operations this month
- 2 scenarios failing
- Search and folder/category filters (Orders, Customers, Inventory, Finance)
- Live / Paused / Failing status controls

Visible scenario names include:
1. New order → packing slip
2. Low stock → reorder
3. Review request after delivery
4. Wholesale lead → CRM
5. Morning sales digest
6. Refund → credit note
7. Abandoned cart nudge
8. Support inbox → ticket

### Workflow editor
The selected scenario is **New order → packing slip**. The canvas contains connected app/action nodes, including:
- Storefront
- Router
- Cloud files
- Team chat
- Courier

The right panel shows operations this month, success percentage, next-run information, owner and recent runs. The header includes Live state, event timing and Run now.

### Runs
The Runs page shows daily run counts, runs needing attention, average run time, history filters and a table with:
- Run ID
- Scenario
- Started by
- Status
- Operations
- Data
- Duration
- Time

A separate timeline / live run view appears in the later part of the recording.

## Readable code transcribed from `src/canvas.tsx`

The source preview is visible throughout the recording. The 16-line code block reads as follows (minor punctuation/formatting normalized for legibility):

```tsx
for (const n of order) {
  const body = root.querySelector(`[data-node="${n.id}"] .cv__body`);
  if (connFor(n.app)?.status === 'broken') { shake(body); return; }
  gsap.fromTo(body, { scale: 1 }, {
    keyframes: { scale: [1, 1.14, 0.97, 1], duration: 0.55 },
    setBadges(b) => { ...b, [n.id]: 'ok' });
  // A bead of light runs every wire of this step
  await Promise.all(outsOf(n).map((p) => new Promise((done) => {
    const L = p.getTotalLength(), o = { t: 0 };
    gsap.to(o, { t: 1, duration: 0.5, ease: 'power1.inOut',
      onUpdate: () => {
        const pt = p.getPointAtLength(o.t * L);
        bead.setAttribute('cx', pt.x); bead.setAttribute('cy', pt.y);
      },
      onComplete: done }));
  }));
}
```

The code preview is small; the `setBadges` line is partly obscured/blurred and appears to be an update callback. The snippet is preserved as visible rather than represented as a complete original source file. It indicates that the workflow runner iterates nodes in order, stops if an app connection is broken, briefly scales each node, marks its badge successful, and animates a light bead along outgoing SVG paths using `getTotalLength()` and `getPointAtLength()`.

## Implemented in this project
- Overview dashboard and KPI cards.
- Scenarios gallery with category filtering, search and active/pause toggles.
- Scenario creation modal.
- Click a scenario card to open a visual workflow editor.
- Workflow nodes, connector paths and animated run progression.
- Run now action that animates a bead along the connector, pulses nodes, and marks each step complete.
- Runs history table with status filters and search.
- Apps connection directory, Team, Data, Billing, Learn, Help and Settings screens.
- Responsive layout and collapsible sidebar.

## Files
- `index.html` — application shell
- `styles.css` — UI styling and responsive layouts
- `app.js` — local data, page rendering, interactions and workflow animation
- `README.md` — source inspection, code transcription and run instructions

## Accuracy and limitations
This is a screen-based recreation, not the original brisko repository. The code preview is readable enough to transcribe the main workflow animation logic, but the source shown is only a small `src/canvas.tsx` excerpt. The remainder of the app is reconstructed from visible UI. Some labels, metrics and records are approximate demo content. There is no real Shopify, Slack, Google Drive, CRM, shipping, email, billing or automation API connected. Scenario runs are simulated in the browser and do not trigger real business operations.

## 👨‍💻 Author

**mrchandrayee** · [GitHub](https://github.com/mrchandrayee)

## 📄 License

[MIT License](./LICENSE)
