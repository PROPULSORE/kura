---
title: Own sync server · Kura
---

# Own sync server

**kura-server** keeps your devices in sync through a computer of yours instead of
Google Drive. It is optional: most people never need it.

- It stores only files that the app has already **encrypted**. It never sees your
  key, has no web interface and cannot read your library.
- Videos, chapters and downloads never pass through it: only library, progress,
  settings and backups.
- One program, nothing else to install. It runs on Linux (64-bit PCs and servers,
  Raspberry Pi).

## 1. Download

From the [Releases page](https://github.com/PROPULSORE/kura/releases):

| Machine | File |
|---|---|
| Most PCs, mini PCs, servers, Proxmox | `kura-server-linux-amd64` |
| Raspberry Pi (64-bit OS) | `kura-server-linux-arm64` |

A Docker image is coming.

## 2. Install (Debian, Ubuntu, Raspberry Pi OS)

```
sudo install -m 0755 kura-server-linux-amd64 /usr/local/bin/kura-server
```

Create `/etc/systemd/system/kura-server.service`:

```
[Unit]
Description=Kura sync server
After=network-online.target
Wants=network-online.target

[Service]
ExecStart=/usr/local/bin/kura-server -addr 127.0.0.1:8484 -db /var/lib/kura/kura-server.db
StateDirectory=kura
DynamicUser=yes
Restart=on-failure
NoNewPrivileges=yes
ProtectSystem=strict
ProtectHome=yes
PrivateTmp=yes

[Install]
WantedBy=multi-user.target
```

Then:

```
sudo systemctl enable --now kura-server
sudo journalctl -u kura-server
```

The log of the first start shows the **server key**: the app asks for it once, to
create a library. Save it right away, like a password: the server keeps only a
fingerprint of it and never shows it again. If you lose it, stop the service, run
`sudo kura-server -db /var/lib/kura/kura-server.db -reset-server-key` to get a new
one, then start it. The old key stops working; devices already connected keep
working.

Options: `-quota-mb` (space per library, default 2048), `-max-file-mb` (default 64),
`-tls-cert` and `-tls-key` (HTTPS with your own certificate).

## 3. HTTPS with Tailscale (recommended)

Android only talks to servers over **HTTPS**. The simplest way, which also works
away from home:

1. Install [Tailscale](https://tailscale.com/download) on the server and on your
   devices, with the same account.
2. On the server: `sudo tailscale serve --bg 8484`.
3. The server answers at `https://<name>.<your-tailnet>.ts.net`, with a valid
   certificate, and only for your devices.

Alternatively: your own certificate with `-tls-cert`/`-tls-key` and
`-addr 0.0.0.0:8484`, or a reverse proxy you already use.

## 4. Connect the app

1. On the first device: **Profile › Sync › Own server › New library**, with the
   server address and the server key.
2. On each other device: on the first one open **Sync › Link a device**, then on the
   new one **Own server › Link from a device** and scan the QR code (or paste the
   link under it).
3. A device that reaches the server at another address (for example a home PC with
   `https://myserver:8484`) writes it in **Server address from here**.

## Backups

`/var/lib/kura/` holds everything, already encrypted: back it up like any other
folder. The app also keeps its own backups (Profile › Backup), separate from sync.
