# mazimaos-appstore

A **personal** AppStore for ZimaOS / CasaOS, focused on clean Docker setups (explicit volumes, secure DNS, and sane defaults).

This repository contains `docker-compose.yml` files adapted to the ZimaOS/CasaOS AppStore format, using `x-casaos` metadata for direct integration into the ZimaOS UI.

---

## 🚀 Features

- Apps packaged as `docker-compose.yml` compatible with the CasaOS/ZimaOS AppStore format.
- Clean default volume paths (e.g. `/DATA/AppData/...`), easy to adjust to your own storage.
- Network, ports and environment settings designed to be simple but robust.
- Plug-and-play integration into the ZimaOS dashboard by adding this GitHub repo as an AppStore source.

---

## 📦 Included applications

### Myst Node

A Mysterium VPN node with:

- Cloudflare 1.1.1.1 for Families DNS (`1.1.1.3` / `1.0.0.3`) to block malware and adult content at DNS level.
- Default persistent volume: `/DATA/AppData/myst-node:/var/lib/mysterium-node`, which can be changed before installation in the ZimaOS UI.
- Restricted UDP port range to reduce exposure while staying compatible with Mysterium’s documentation.

More apps will be added over time as the home lab and use cases grow.

### Honeygain

Honeygain bandwidth sharing client running in a Docker container, using the official `honeygain/honeygain` image. [web:268][web:269]

- No ports or volumes required; configuration is done entirely via command‑line arguments. [web:268][web:270]
- Uses `--restart unless-stopped` so it comes back automatically after a reboot. [web:269][web:289]
- Very lightweight in terms of CPU/RAM (well within typical ZimaOS home server resources). [web:279]

**Important:**  
Before deploying from this AppStore, edit the app in ZimaOS/CasaOS and replace:

- `TON_EMAIL` with your Honeygain account email
- `TON_PASSWORD` with your Honeygain account password
- `ZimaBoard` with a unique device name for this machine (as shown in the Honeygain dashboard) [web:269][web:289]

The underlying Docker command matches the official Honeygain Docker guide:  

```bash
docker run -d --restart unless-stopped \
  honeygain/honeygain \
  -tou-accept \
  -email ACCOUNT_EMAIL \
  -pass ACCOUNT_PASSWORD \
  -device DEVICE_NAME
```

---

## 🔗 AppStore URL for ZimaOS / CasaOS

To add this AppStore to ZimaOS/CasaOS, use this ZIP URL:

```text
https://github.com/mazama923/mazimaos-appstore/archive/refs/heads/main.zip
```

ZimaOS / CasaOS will read the manifests from this archive and show the apps in the AppStore interface.

---

## 🛠 Install on ZimaOS / CasaOS (UI)

1. Open the ZimaOS / CasaOS Dashboard.
2. Go to App Store.
3. Click Add Source / Add Repository.
4. Paste the ZIP URL:

   ```text
   https://github.com/mazama923/mazimaos-appstore/archive/refs/heads/main.zip
   ```

5. Confirm and wait for the store list to refresh (or reboot if needed).
6. Search for Myst Node (Self) in the App Store and install it like any other app.

---

## 🧩 Repository structure

```text
mazimaos-appstore
├─ Apps/
│  └─ myst/
│     ├─ docker-compose.yml   # app definition + x-casaos metadata
│     └─ icon.png             # icon used in ZimaOS/CasaOS
└─ README.md
```

---

## 🤝 Contribute / Fork

You can:

- Fork this repo and adjust volume paths, ports, or DNS to match your environment.
- Add your own apps under `Apps/<app-name>/docker-compose.yml` following the same `x-casaos` pattern.

Third-party AppStores are listed on Awesome CasaOS; this repo follows the same philosophy: simple, readable, and easy to maintain.
