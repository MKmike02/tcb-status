# TCB Status

Public status page for [The Cloud Bakery](https://tcb-cloud.com), hosted on GitHub Pages — deliberately independent of the platform it monitors, so it stays reachable during an outage.

## How it works

- `.github/workflows/health-check.yml` runs every 5 minutes, calls `https://tcb-cloud.com/api/health-check`, and updates `status.json`.
- On a status change, an entry is added to `incidents.json` (opened automatically, resolved automatically when health returns). The `note` field can be edited by hand for a real incident to add actual context — the automation only writes a placeholder ("Automatically detected — investigating.").
- `index.html` is a static page that reads both JSON files client-side. No build step.

## Manually editing an incident

During a real incident, edit the relevant entry in `incidents.json` directly (e.g. via the GitHub web UI) to replace the auto-generated note with an actual explanation and, if useful, an ETA. Commit directly to `main` — the next scheduled run won't overwrite a resolved incident's note.
