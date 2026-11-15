# Security policy

## Supported versions

Only the **latest release** of Kura receives security fixes. Before reporting,
please check that the problem is still there in the
[latest release](https://github.com/PROPULSORE/kura/releases/latest).

## Reporting a vulnerability

Please **do not** open a public issue for security problems.

Report them privately through GitHub:

1. open the [Security tab](https://github.com/PROPULSORE/kura/security) of this
   repository;
2. click **Report a vulnerability**;
3. fill in the form. Only you and the maintainer can see the report.

Please include:

- the Kura version, the platform (Android or Windows) and the system version;
- what the problem is and what an attacker could do with it;
- the steps to reproduce it, or a proof of concept;
- if relevant, the diagnostics log (Profile › Diagnostics), after reading it
  and removing anything private.

You will get an answer as soon as possible. Please give a reasonable time to
fix the problem before talking about it in public. Kura is made by one person
in their free time, so there is no bug bounty.

## Scope

In scope: the Kura app for Android and Windows as published in this
repository's releases, including how it stores, encrypts, backs up and syncs
data.

Out of scope:

- **extensions**: they are third-party scripts that users choose to install;
  report problems to their authors (a way for an extension to escape Kura's
  limits *is* in scope);
- websites read by extensions, and third-party services such as AniList, TMDB,
  AniSkip, MyAnimeList, Trakt and Google;
- problems that need an already compromised device, or physical access to an
  unlocked device;
- the SmartScreen warning on Windows, which appears because the app is not
  signed.
