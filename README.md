# Cherubino — Umbrel Community App Store

A media-focused Umbrel Community App Store for **umbrelOS 2.x** containing:

- Lidarr
- slskd
- Soularr
- Whisparr v3
- Stash

## Umbrel 2.x compatibility

This store intentionally uses `manifestVersion: 1`. Current working Umbrel community stores still use manifest v1; Umbrel 2.x compatibility comes from the storage and Compose configuration, not from switching to a nonexistent generic "manifest v2" format.

Each app follows the same compatibility pattern used by the reference Media community store:

- `storage.dataRoot: data`
- `permissions: [STORAGE_DOWNLOADS]` where shared Downloads is required
- `${UMBREL_ROOT}/data/storage/downloads:/downloads`
- UID/GID `1000:1000` for apps that support explicit user mapping
- `restart: on-failure`
- standard Umbrel `app_proxy` service

## Shared storage

The apps intentionally see Umbrel's standard Downloads directory as `/downloads`.

- Lidarr: `/downloads`
- slskd: `/downloads/soulseek/complete` and `/downloads/soulseek/incomplete`
- Soularr: `/downloads/soulseek/complete`
- Whisparr: `/downloads`
- Stash: `/data` inside the container, backed by the same shared Downloads directory

This avoids host-path and permission mismatches after upgrading to umbrelOS 2.x.

## Soularr setup

Install Lidarr and slskd first. Open Soularr's web UI and set the Lidarr and slskd API keys in its configuration editor.

slskd also exposes TCP/UDP `50300` for Soulseek connectivity.

## Important

Docker Compose validation could not be executed here because Docker is not installed in this build environment. YAML was parsed and the archive structure was checked.
