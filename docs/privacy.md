---
title: Privacy policy
permalink: /privacy
---

# Kura privacy policy

*Last updated: 21 October 2026*

Kura is a free app for Android and Windows made by PROPULSORE, an individual
developer in Italy ("we", "the developer"). This policy explains what data
Kura handles, where it goes and what control you have.

**In short:** your library stays on your device. Kura has no account system,
no ads, no analytics and no tracking. The developer has no server and never
receives your data. Whatever you choose to back up or sync is encrypted on your
device with a key that only you have.

## Data stored on your device

Kura keeps on your device:

- your library: titles, progress, statuses, ratings, notes and history;
- your settings, the extensions and catalogs you added, and the keys or logins
  you enter (for example your TMDB key, or AniList, MyAnimeList and Trakt
  logins);
- downloaded chapters and episodes, encrypted and usable only inside Kura on
  that device;
- cookies of websites where you passed an anti-bot check, kept only on that
  device for that website;
- a diagnostics log of errors (see below).

This data is not sent to the developer. Uninstalling Kura deletes it from the
device, except backups saved in a folder you chose.

## Backup and sync (optional)

You can choose, in the app, to:

- save **backups** to a folder you choose (for example on the device or on a
  USB stick);
- save backups and **sync** your library between your devices through **your
  own Google Drive**;
- sync through **your own Kura server**, which you run yourself.

Everything Kura writes to Google Drive or to your server is **encrypted on your
device** before it leaves it, with a key shown to you once as a **recovery
code**. Without that code nobody can read the data: not Google, not the owner
of the server, not the developer, and not you if you lose both the code and
your devices. The storage can only see technical information such as file
names, sizes, dates and a key identifier.

Downloads and website cookies are never backed up or synced.

## Google user data

If you choose Google Drive for backup or sync, Kura asks you to sign in with
Google and to grant access to the **Drive app data folder**
(`https://www.googleapis.com/auth/drive.appdata`), plus your basic account
identity (email address).

- **What Kura accesses:** only the hidden application data folder that Google
  Drive reserves for Kura, and the email address of the account you signed in
  with. Kura **cannot see, open or change any other file** in your Google
  Drive.
- **Why:** to store your own encrypted backups and sync files there, and to
  read them back on your other devices. The email address is only shown in
  the app, so you know which account is in use.
- **Where it goes:** the files go from your device directly to your Google
  Drive. The sign-in tokens are kept on your device (and, encrypted, on your
  other devices through sync). Nothing passes through any server of the
  developer.
- **Sharing:** Google user data is **not shared, sold or transferred** to
  anyone, and is not used for advertising, profiling or training any model.
  It is not read by any human.
- **Limited use:** Kura's use and transfer of information received from Google
  APIs adheres to the
  [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy),
  including the Limited Use requirements.
- **How to stop and delete it:**
  1. in Kura, turn off Google Drive backup and sync;
  2. remove Kura's access in your Google Account at
     [myaccount.google.com/permissions](https://myaccount.google.com/permissions);
  3. delete Kura's hidden data from Google Drive: open
     [drive.google.com](https://drive.google.com) on a computer, go to
     **Settings › Manage apps**, find Kura, choose **Options › Delete hidden
     app data**.

## Services Kura contacts

Kura talks directly from your device to these services. Each of them receives
your IP address and the requests needed to work, under its own privacy policy.

| Service | When | What for |
|---|---|---|
| Websites of the extensions you install | When you search, browse, read or watch | Reading the content you asked for |
| Catalogs you add | When you check or install extensions | Listing and downloading extensions |
| [AniList](https://anilist.co) | When you use anime, manga or light novels | Titles, covers, related works; your list, if you connect AniList |
| [TMDB](https://www.themoviedb.org) | When you use series and movies, with your own API key | Titles, seasons, episodes, images |
| [AniSkip](https://aniskip.com) | When you watch anime (can be turned off in the player) | Intro and outro times |
| [MyAnimeList](https://myanimelist.net) | Only if you connect it | Syncing your list |
| [Trakt](https://trakt.tv) | Only if you connect it | Syncing your history and watchlist |
| Google Drive | Only if you choose it | Encrypted backup and sync |
| Your own server | Only if you choose it | Encrypted sync and backup |
| [GitHub](https://github.com) | At start-up and once a day | Checking whether a new version of Kura is out (no account, no personal data) |

Kura comes without extensions. Extensions are third-party scripts that you
choose to install; the websites they read are not operated by the developer,
and Kura is not affiliated with them.

## Diagnostics log

Kura keeps a log of errors **only on your device**: app version, system, what
failed and, for extensions, which website and step. Keys, tokens, cookies and
the recovery code are removed from it. It is never sent automatically: it
leaves the device only if you copy it or save it to a file and send it
yourself, for example in a bug report. You can read and clear it in
**Profile › Diagnostics**.

## What Kura does not do

- No ads, no analytics, no crash reporting services, no tracking.
- No account with the developer.
- No selling or sharing of your data.

## Children

Kura is not directed at children under 13 (or the minimum age in your country)
and does not knowingly handle their data. Kura does not collect personal data
from anyone.

## Your rights

Because the developer does not receive or store your data, there is nothing for
us to give, correct or delete: you control it in the app and in the services
you connect. If you have a question about your data, you can ask us anyway
(see below). If you live in the EU, you also have the right to complain to your
data protection authority.

## Changes

If this policy changes, the new version is published on this page with a new
date. Important changes are also mentioned in the release notes.

## Contact

Open an issue at
[github.com/PROPULSORE/kura/issues](https://github.com/PROPULSORE/kura/issues).
For security problems, see the
[security policy](https://github.com/PROPULSORE/kura/security/policy).
