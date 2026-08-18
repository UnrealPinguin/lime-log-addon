# Lime Log

Scan the QR code on a Lime scooter and the app tells you whether anyone on the crew has
ridden that exact vehicle before.

## Before you install

The image lives in a private GitHub registry, so Home Assistant needs credentials once:

1. Turn on **Advanced Mode** on your HA profile page (click your name, bottom left).
2. **Settings → Add-ons → Add-on Store → ⋮ (top right) → Registries**.
3. Add `ghcr.io` with your GitHub username and a **classic** personal access token that has
   the `read:packages` and `repo` scopes.

The `repo` scope is needed because the image is attached to a private repository.

## After you install

The web interface is on port **3001**. It has no login of its own — that is deliberate, and
it means **you must not expose it directly to the internet**. Point your Cloudflare tunnel
at it and put an Access policy in front:

- Service: `http://<your Pi's LAN IP>:3001`
- Then add a Cloudflare Access application for the hostname, allowing your crew's email
  addresses.

The admin page at `/admin` can erase the database and is not password protected. Access is
what stands in front of it.

## Bringing an existing database across

1. Copy your `limelog.db` into Home Assistant's `share` folder, named
   **`limelog-import.db`** — over Samba, or with the File Editor add-on.
2. Restart this add-on.

It is adopted on start and the source file is renamed to `.imported` so it cannot be picked
up twice.

**Make that file with `VACUUM INTO`, not a plain copy.** The database runs in WAL mode, so
a bare copy of `limelog.db` leaves recent rides behind in the `-wal` file next to it:

```
sqlite3 limelog.db "VACUUM INTO 'limelog-import.db'"
```

With no database and no import, the add-on creates the crew and no rides, so the app works
from the first start.

## Data and backups

Everything lives in the add-on's `/data`, which survives updates and is included in Home
Assistant's own backups. On top of that, a snapshot is taken into `/data/backups` before
every migration and kept for 14 days.

## Updating

Push to `main` in the app repository, wait for the image to build, then raise `version` in
this add-on's `config.yaml`. Home Assistant will offer the update.
