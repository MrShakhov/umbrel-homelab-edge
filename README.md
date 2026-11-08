# Homelab Edge: Kinopeer from main for umbrelOS

A Community App Store for umbrelOS with one app, **Kinopeer Edge** (`homelab-edge-kinopeer`): Kinopeer
as it is on its main branch, rebuilt after every merge, for trying changes before they are released.
The released app is in [umbrel-homelab-store](https://github.com/MrShakhov/umbrel-homelab-store).

Nothing here is edited by hand but the app's links in `umbrel-app.yml`. The [Kinopeer repository](https://github.com/kinopeer/kinopeer)'s
Edge workflow builds
`ghcr.io/kinopeer/kinopeer:edge` (linux/arm64) on every push to its main branch, then commits here:
the image by tag and digest in `docker-compose.yml`, and in `umbrel-app.yml` the version (Kinopeer's
version and the commit, `0.6.0+abc1234`, as Settings → About shows it) and the commits since the
previous build as release notes. umbrelOS checks the store every 5 minutes and offers the update.

Kinopeer was called Kinoseed up to version 0.7. The old app, **Kinoseed Edge** (`homelab-edge-kinoseed`,
port 8796), left this store on 2026-11-06: an Umbrel that has it keeps running it, with no more updates.
Its settings and title matches are in its data folder, `settings.json` and `matches.json`, which can be
copied to Kinopeer Edge's before uninstalling it.

## Layout

```
umbrel-app-store.yml              id: homelab-edge, the prefix for every app in this store
homelab-edge-kinopeer/
  umbrel-app.yml                  manifest (port 8798 on Umbrel); version and release notes set by the workflow
  icon.svg                        the app's icon, a copy of Kinopeer's scripts/icons/icon.svg, which the manifest links to
  docker-compose.yml              app_proxy + web service; image set by the workflow
  data/                           copied to the app's data folder, where Kinopeer keeps its settings
```

The package is the released one's with another id, name and port. It keeps its own settings (the TMDB
key is asked for again) and its own torrent-to-title matches, but works with the same qBittorrent and
Prowlarr apps, so pausing, moving or deleting a torrent in it is real.

## Install in umbrelOS

1. Open **App Store** → the **⋯** menu at the top right → **Community App Stores**.
2. Paste `https://github.com/MrShakhov/umbrel-homelab-edge` → **Add**.
3. Open **Homelab Edge App Store** → **Kinopeer Edge** → **Install**. It opens at `http://umbrel.local:8798`.
