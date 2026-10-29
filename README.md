# Homelab Edge: Kinoseed from main for umbrelOS

A Community App Store for umbrelOS with one app, **Kinoseed Edge** (`homelab-edge-kinoseed`): Kinoseed
as it is on its main branch, rebuilt after every merge, for trying changes before they are released.
The released app is in [umbrel-homelab-store](https://github.com/MrShakhov/umbrel-homelab-store).

Nothing here is edited by hand. The Kinoseed repository's Edge workflow builds
`ghcr.io/mrshakhov/kinoseed:edge` (linux/arm64) on every push to its main branch, then commits here:
the image by tag and digest in `docker-compose.yml`, and in `umbrel-app.yml` the version (Kinoseed's
version and the commit, `0.6.0+abc1234`, as Settings → About shows it) and the commits since the
previous build as release notes. umbrelOS checks the store every 5 minutes and offers the update.

## Layout

```
umbrel-app-store.yml              id: homelab-edge, the prefix for every app in this store
homelab-edge-kinoseed/
  umbrel-app.yml                  manifest (port 8796 on Umbrel); version and release notes set by the workflow
  docker-compose.yml              app_proxy + web service; image set by the workflow
  data/                           copied to the app's data folder, where Kinoseed keeps its settings
```

The package is the released one's with another id, name and port. It keeps its own settings (the TMDB
key is asked for again) and its own torrent-to-title matches, but works with the same qBittorrent and
Prowlarr apps, so pausing, moving or deleting a torrent in it is real.

## Install in umbrelOS

1. Open **App Store** → the **⋯** menu at the top right → **Community App Stores**.
2. Paste `https://github.com/MrShakhov/umbrel-homelab-edge` → **Add**.
3. Open **Homelab Edge App Store** → **Kinoseed Edge** → **Install**. It opens at `http://umbrel.local:8796`.
