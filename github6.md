# Anaesthetic logbook

An offline case logbook for the phone. No accounts, no server, no dependencies.
Cases live only in the browser storage of the device that logged them.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: form, list, storage, Excel writer |
| `sw.js` | Service worker, so it opens with no signal |
| `manifest.webmanifest` | Makes iOS treat it as an installed app, not a web page |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | Home screen icon |

Keep all six in the same folder. Paths are relative, so a repository
subfolder (`username.github.io/logbook/`) works as well as a root domain.

## Hosting it

Any static HTTPS host will do. GitHub Pages: create a repository, upload
these six files, then Settings → Pages → deploy from `main` / root.

HTTPS is not optional — service workers and persistent storage both need it.

## One thing to be careful about

Browser storage is tied to the exact origin. If the URL changes, the app
looks empty because it is a different origin, not because the data is gone.
Pick a URL once and stay on it, and use **Save a backup file** periodically.

## Changing the dropdowns

The option lists are plain arrays at the top of the `<script>` block in
`index.html`: `ASA`, `CASETYPE`, `SUPERVISION`, `SPECIALTIES`, `MODES`,
`REGIONAL`, `PROCEDURES`. Edit them, then bump `CACHE` in `sw.js` to
`logbook-v2` so installed copies pick up the change.
