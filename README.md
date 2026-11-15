# Kura

[![Latest release](https://img.shields.io/github/v/release/PROPULSORE/kura?label=Latest%20release&logo=github)](https://github.com/PROPULSORE/kura/releases/latest)
[![Android](https://img.shields.io/badge/-Android-34d399?logo=android&logoColor=white)](https://github.com/PROPULSORE/kura/releases/latest/download/kura-android.apk)
[![Windows](https://img.shields.io/badge/-Windows-22d3ee?logo=windows&logoColor=white)](https://github.com/PROPULSORE/kura/releases/latest/download/kura-setup-x64.exe)

**English** · [Italiano](#italiano)

Kura is a free app for **Android and Windows** that keeps your anime, manga,
light novels, TV series and movies in one library, and lets you watch episodes
and read chapters in the same place.

> **Status: beta.** Kura is in daily use, but things can still change or break.
> Keep the backups on (see below).

This repository only holds the releases and the public documents of Kura. The
source code is not public.

## Features

- **One library** for anime, manga, light novels, series and movies, with
  progress, statuses, statistics and a trash you can restore from.
- **Video player** (resume, next episode, intro and outro skipping) and
  **reader** for manga and light novels.
- **Extensions**: small scripts that read the websites *you* choose. Kura comes
  **without any extension** and this repository does not distribute any.
- **Downloads** to watch or read offline; they stay encrypted on the device.
- **Data from AniList** (anime, manga, light novels) and **TMDB** (series and
  movies, with your own free API key).
- **Trackers**: optional two-way sync with AniList, MyAnimeList and Trakt.
- **Backup and sync** between your devices, through your own Google Drive or
  your own server, **end-to-end encrypted**.
- No ads, no analytics, no account with us.

## Download

| Platform | File |
|---|---|
| Android | [kura-android.apk](https://github.com/PROPULSORE/kura/releases/latest/download/kura-android.apk) |
| Windows (installer) | [kura-setup-x64.exe](https://github.com/PROPULSORE/kura/releases/latest/download/kura-setup-x64.exe) |
| Windows (portable) | [kura-windows-x64.zip](https://github.com/PROPULSORE/kura/releases/latest/download/kura-windows-x64.zip) |

All versions are on the [Releases page](https://github.com/PROPULSORE/kura/releases).
Download Kura only from here.

## Installing

### Android

1. Download `kura-android.apk` on the phone or tablet and open it.
2. If Android asks, allow your browser or file manager to **install unknown
   apps**, then go back and tap **Install**.

### Windows (64-bit)

1. Download `kura-setup-x64.exe` and run it. It installs Kura for your user
   only, no administrator rights needed.
2. Kura is not signed with a certificate, so Windows may show a **SmartScreen**
   warning: click **More info**, then **Run anyway**.

Prefer no installation? Download `kura-windows-x64.zip`, extract it to a folder
of your choice and start `kura.exe`.

### Updating

Kura checks once a day whether a new version is out and shows it in
**Profile**. Download the new file and install it over the old version
(installer: just run the new one; portable: extract it over the old folder):
your data stays.

## First steps

A tour of the app with screenshots: [Getting started](https://propulsore.github.io/kura/guide).

1. **TMDB key** (for series and movies): make a free account on
   [themoviedb.org](https://www.themoviedb.org), ask for an API key for
   personal use in **Settings › API**, then paste it in Kura under
   **Profile › Trackers**.
2. **Extensions**: in **Profile › Extensions**, add a catalog with its index
   URL, or install an extension from a `.zip` file. Only install extensions
   from people you trust. Want to write one? See
   [Writing extensions](https://propulsore.github.io/kura/extensions).
3. **Backup and sync**: in **Profile › Backup** and **Profile › Sync**, keep
   the **recovery code** in a safe place, then choose a backup folder, Google
   Drive or your own server.

## Your own sync server (optional)

Sync works out of the box with your Google Drive. If you have a small home
server (a mini PC, a NAS, a Raspberry Pi), you can run **kura-server** on it
instead: changes reach your other devices at once, and your data never leaves
your home.

- It only keeps **encrypted** files (library, progress, settings): it never
  sees your key and has no web interface. Videos never pass through it.
- One small program, no database to install. Files on the
  [Releases page](https://github.com/PROPULSORE/kura/releases):
  `kura-server-linux-amd64` (most PCs and servers) and
  `kura-server-linux-arm64` (Raspberry Pi). A Docker image is coming.
- Android needs **HTTPS**: the easy way is [Tailscale](https://tailscale.com)
  (`tailscale serve`), which also lets you sync away from home.

Step-by-step guide: [Own sync server](https://propulsore.github.io/kura/server).

## Privacy

Your library stays on your device. Backups and sync go only where you choose
(a folder, your own Google Drive, your own server), always encrypted with a key
only you have. The developer has no server and cannot read your data. No ads,
no analytics, no tracking.

Read the full [privacy policy](https://propulsore.github.io/kura/privacy).

## Help and feedback

- Bugs and ideas: [open an issue](https://github.com/PROPULSORE/kura/issues/new/choose).
  See [CONTRIBUTING.md](CONTRIBUTING.md).
- Security problems: please report them privately, see [SECURITY.md](SECURITY.md).

## Terms of use

Kura is free to use, but it is **not open source**. See the
[terms of use](LICENSE). Third-party libraries keep their own licenses, listed
in the app under **Profile › About › Licenses**.

## Credits

- Anime, manga and light novel data from [AniList](https://anilist.co).
- Series and movie data from [TMDB](https://www.themoviedb.org).
  *This product uses the TMDB API but is not endorsed or certified by TMDB.*
- Intro and outro times from [AniSkip](https://aniskip.com).
- Video playback by [mpv](https://mpv.io) and [FFmpeg](https://ffmpeg.org),
  under the GNU LGPL v3.

Kura is not affiliated with AniList, TMDB, MyAnimeList, Trakt, AniSkip or any
website that extensions read.

---

## Italiano

Kura è un'app gratuita per **Android e Windows** che tiene anime, manga, light
novel, serie TV e film in un'unica libreria, e permette di guardare episodi e
leggere capitoli nello stesso posto.

> **Stato: beta.** Kura si usa ogni giorno, ma qualcosa può ancora cambiare o
> rompersi. Tieni attivi i backup.

Questa repository contiene solo le release e i documenti pubblici di Kura. Il
codice sorgente non è pubblico.

### Cosa fa

- **Una libreria** per anime, manga, light novel, serie e film, con progressi,
  stati, statistiche e un cestino da cui recuperare.
- **Player video** (riprende da dove eri, episodio successivo, salto di sigla
  e coda) e **lettore** per manga e light novel.
- **Estensioni**: piccoli script che leggono i siti che scegli *tu*. Kura non
  include alcuna estensione e questa repository non ne distribuisce.
- **Download** per guardare o leggere offline; restano cifrati sul dispositivo.
- **Dati da AniList** (anime, manga, light novel) e **TMDB** (serie e film, con
  una tua chiave API gratuita).
- **Tracker**: sincronizzazione facoltativa con AniList, MyAnimeList e Trakt.
- **Backup e sync** tra i tuoi dispositivi, tramite il tuo Google Drive o un
  tuo server, **cifrati end-to-end**.
- Niente pubblicità, niente statistiche d'uso, nessun account da creare con noi.

### Scaricare

- Android: [kura-android.apk](https://github.com/PROPULSORE/kura/releases/latest/download/kura-android.apk)
- Windows (installer): [kura-setup-x64.exe](https://github.com/PROPULSORE/kura/releases/latest/download/kura-setup-x64.exe)
- Windows (portatile): [kura-windows-x64.zip](https://github.com/PROPULSORE/kura/releases/latest/download/kura-windows-x64.zip)

Tutte le versioni sono nella [pagina Releases](https://github.com/PROPULSORE/kura/releases).
Scarica Kura solo da qui.

### Installare

**Android:** scarica `kura-android.apk` e aprilo. Se Android lo chiede,
permetti al browser o al gestore file di **installare app sconosciute**, poi
torna indietro e tocca **Installa**.

**Windows (64 bit):** scarica `kura-setup-x64.exe` e avvialo: installa Kura
solo per il tuo utente, senza permessi da amministratore. Kura non è firmata
con un certificato, quindi può comparire l'avviso di **Windows SmartScreen**:
clicca **Ulteriori informazioni**, poi **Esegui comunque**. Senza installazione:
scarica `kura-windows-x64.zip`, estrailo in una cartella e avvia `kura.exe`.

**Aggiornare:** Kura controlla una volta al giorno se c'è una nuova versione e
lo mostra in **Profilo**. Scarica il nuovo file e installalo sopra la versione
vecchia (installer: avvia quello nuovo; portatile: estrailo sopra la vecchia
cartella): i dati restano.

### Primi passi

Un giro dell'app con le foto (in inglese): [Getting started](https://propulsore.github.io/kura/guide).

1. **Chiave TMDB** (per serie e film): crea un account gratuito su
   [themoviedb.org](https://www.themoviedb.org), chiedi una chiave API per uso
   personale in **Settings › API** e incollala in Kura in **Profilo › Tracker**.
2. **Estensioni**: in **Profilo › Estensioni** aggiungi un catalogo con il suo
   indirizzo, oppure installa un'estensione da un file `.zip`. Installa solo
   estensioni di persone di cui ti fidi. Vuoi scriverne una? Vedi
   [Writing extensions](https://propulsore.github.io/kura/extensions) (in inglese).
3. **Backup e sync**: in **Profilo › Backup** e **Profilo › Sync** conserva il
   **codice di recupero** in un posto sicuro, poi scegli una cartella di backup,
   Google Drive o un tuo server.

### Server di sync tuo (facoltativo)

Il sync funziona subito con il tuo Google Drive. Se hai un piccolo server in
casa (mini PC, NAS, Raspberry Pi) puoi usare **kura-server**: le modifiche
arrivano subito sugli altri dispositivi e i dati non escono di casa.

- Tiene solo file **cifrati** (libreria, progressi, impostazioni): non vede la
  tua chiave e non ha un'interfaccia web. I video non passano di lì.
- Un solo programma, senza database da installare. Nella
  [pagina Releases](https://github.com/PROPULSORE/kura/releases):
  `kura-server-linux-amd64` (quasi tutti i PC e server) e
  `kura-server-linux-arm64` (Raspberry Pi). L'immagine Docker è in arrivo.
- Android vuole **HTTPS**: il modo più semplice è [Tailscale](https://tailscale.com)
  (`tailscale serve`), che permette anche il sync fuori casa.

Guida passo passo (in inglese): [Own sync server](https://propulsore.github.io/kura/server).

### Privacy

La libreria resta sul tuo dispositivo. Backup e sync vanno solo dove scegli tu
(una cartella, il tuo Google Drive, un tuo server), sempre cifrati con una
chiave che hai solo tu. Lo sviluppatore non ha server e non può leggere i tuoi
dati. Niente pubblicità, niente statistiche, nessun tracciamento.

Leggi l'[informativa sulla privacy](https://propulsore.github.io/kura/privacy)
(in inglese).

### Aiuto e segnalazioni

- Bug e idee: [apri una issue](https://github.com/PROPULSORE/kura/issues/new/choose)
  (anche in italiano). Vedi [CONTRIBUTING.md](CONTRIBUTING.md).
- Problemi di sicurezza: segnalali in privato, vedi [SECURITY.md](SECURITY.md).

### Condizioni d'uso

Kura è gratuita ma **non è open source**. Vedi le [condizioni d'uso](LICENSE)
(in inglese). Le librerie di terze parti mantengono le proprie licenze, elencate
nell'app in **Profilo › Informazioni › Licenze**.

### Riconoscimenti

Dati di anime, manga e light novel da [AniList](https://anilist.co); dati di
serie e film da [TMDB](https://www.themoviedb.org) (*This product uses the TMDB
API but is not endorsed or certified by TMDB.*); tempi di sigle e code da
[AniSkip](https://aniskip.com); riproduzione video con [mpv](https://mpv.io) e
[FFmpeg](https://ffmpeg.org), sotto GNU LGPL v3. Kura non è affiliata con
nessuno di questi servizi né con i siti letti dalle estensioni.
