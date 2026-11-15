---
title: Writing extensions · Kura
---

# Writing extensions

Kura comes **without extensions**. An extension is a small JavaScript file plus a
manifest that teaches Kura how to read **one website** for **one content type**.
This page has the essentials, written so that a person or an AI assistant can build
one correctly.

> **Your responsibility.** You choose the sites your extension reads, and you are
> responsible for them. Only write extensions for sources you are allowed to use.
> The Kura project does not provide, host or check any extension or site.

## 1. Files

```
my-extension/
├── manifest.json   # who the extension is
├── main.js         # the code: one kura.<type>({...}) call
└── icon.png        # optional, square
```

## 2. manifest.json

```json
{
  "id": "example.myanimesite",
  "name": "My Anime Site",
  "version": "1.0.0",
  "apiVersion": 0,
  "type": "anime",
  "language": "en",
  "baseUrl": "https://anime.example"
}
```

| Field | Notes |
|---|---|
| `id` | unique and **never changed** (the library refers to it); lower case, dot-separated: `^[a-z0-9]+(\.[a-z0-9-]+)+$` |
| `name` | shown to the user |
| `version` | semantic version; raise it at every change |
| `apiVersion` | contract version: `0` |
| `type` | `"anime"`, `"manga"`, `"light_novel"` or `"series_movies"` |
| `language` | language of the content: `"en"`, `"it"`, `"ja"`... or `"multi"` |
| `baseUrl` | `https://` address of the site, no trailing slash; the script reads it as `kura.baseUrl` |
| `adultOnly` | optional: `true` if the site has only adult content (hidden while the adult filter is on) |
| `description` | optional: one line |
| `hosts` | optional: other hosts of the site (`"cdn.example.com"`, `"*.video.example"`) that an extension with `"transport": "browser"` may load; with that transport any host outside the `baseUrl` domain and this list is refused |

Unknown fields are an error.

## 3. main.js: the contract

The script calls **one** registration function, matching `type`, with an object of
`async` functions:

| `type` | Register with | Required functions |
|---|---|---|
| `anime` | `kura.anime({...})` | `search`, `details`, `episodes`, `videos` |
| `manga` | `kura.manga({...})` | `search`, `details`, `chapters`, `pages` |
| `light_novel` | `kura.lightNovel({...})` | `search`, `details`, `chapters`, `text` |
| `series_movies` | `kura.show({...})` | `search`, `details`, `episodes`, `videos` |

Optional for every type: `popular(page)`, `latest(page)`, `filters()`.

### Common rules

- **Ids** are strings chosen by the extension to find an item again (usually the
  path on the site). They must be **stable** and must not depend on the user,
  session or time. Prefer relative paths (`/anime/123`) and build URLs with
  `kura.baseUrl`.
- **Lists** (`search`, `popular`, `latest`) return a page:
  `{ items: TitleSummary[], hasNextPage: boolean }`. Pages start at 1.
- **Global variables** may only be a cache: the app can restart the script at any
  time.
- Episodes and chapters are returned in **ascending** order of `number` (decimals
  allowed: `12.5`).

### Data

`TitleSummary`: `{ id, title, cover?, adult? }`

`TitleDetails`: `{ id, title, altTitles, cover?, description?, genres?, year?,
status?, externalIds?, adult? }`

- `altTitles` (other names: romaji, English, native) may be an empty list, but fill
  it when possible: it is how Kura matches the title to AniList, MyAnimeList or TMDB.
- `externalIds`: `{ anilist?, mal?, tmdb? }` as numbers, when the site shows them.
- `status`: `"ongoing"`, `"completed"`, `"upcoming"` or `"unknown"`.

Extra fields per type:

| Type | In `details` | Items |
|---|---|---|
| anime | `format` (`tv`, `tv_short`, `movie`, `ova`, `ona`, `special`), `episodeCount`, `episodeDuration` (minutes) | `Episode`: `{ id, number, title?, date?, filler?, thumbnail? }` |
| manga | `format` (`manga`, `manhwa`, `manhua`), `readingMode?` (`rtl`, `ltr`, `vertical`), `chapterCount`, `authors` | `Chapter`: `{ id, number, title?, volume?, date?, scanlator? }` |
| light novel | `chapterCount`, `authors` | `Chapter`, as manga |
| series & movies | `kind` (**required**: `series` or `movie`), `animated?`, `seasonCount?`, `episodeCount?`, `episodeDuration?` | `Episode` plus `season` (1, 2...; 0 for specials). A movie returns one episode without `season` |

What the last function returns:

- **`videos(episodeId)`** (anime, series): a list of
  `{ url, server?, quality?, headers?, audioLanguage?, hardSubs?, subtitles?, audioTracks? }`.
  `url` is an HLS playlist (`.m3u8`) or a video file; `headers` are sent to the
  playlist and every segment. `subtitles`: `{ url, language, label?, format? }`.
- **`pages(chapterId)`** (manga): the page images in reading order, each a URL or
  `{ url, headers }`. Kura downloads and caches them itself.
- **`text(chapterId)`** (light novels): a list of blocks, **never HTML**: a string
  (paragraph), `{ type: "heading", text }`, `{ type: "image", url }` or
  `{ type: "separator" }`. `node.toBlocks()` converts a chapter element for you.

Images (`cover`, pages) are a URL string or `{ url, headers }`.

### Errors

Throw `new KuraError(code, message)`:

| Code | When |
|---|---|
| `NOT_FOUND` | the item no longer exists on the site |
| `CHANGED` | the page does not look as expected (a selector found nothing...) |
| `NETWORK` | the site does not answer |

Any other exception counts as `CHANGED`. Network failures are converted for you.

## 4. What the script can use

The script runs in a sandbox with only these globals: no files, no device access,
no modules, no `fetch`, no timers.

| Global | Use |
|---|---|
| `http.get(url, { headers })`, `http.post(url, body, { headers })` | network requests. The answer has `status`, `url`, `headers`, `body`, `json()`. Non-2xx answers are returned, not thrown: check `status` |
| `html.parse(body, baseUrl)` | parses HTML; nodes have `select(css)`, `selectFirst(css)`, `text()`, `attr(name)`, `absUrl(name)`, `html()`, `toBlocks()` |
| `JSON.parse`, `JSON.stringify` | standard JSON |
| `kura.baseUrl`, `kura.resolveUrl(base, relative)` | the site's address, relative URLs |
| `await kura.sleep(ms)` | waits up to 5000 ms, before retrying a busy site |
| `console.log`, `log` | messages to the device's local log |

Limits: `http:`/`https:` only, never the local network; 30 s and 20 MB per request;
60 s per call; 64 MB of memory. Do not keep parsed nodes between calls (keep plain
strings).

## 5. Example (invented site)

```js
kura.anime({
  async search(query, page) {
    const res = await http.get(`${kura.baseUrl}/search?q=${encodeURIComponent(query)}&page=${page}`);
    const doc = html.parse(res.body, res.url);
    const items = doc.select("ul.results > li").map((li) => ({
      id: li.selectFirst("a").attr("href"),
      title: li.selectFirst(".title").text(),
      cover: li.selectFirst("img")?.absUrl("src"),
    }));
    return { items, hasNextPage: doc.selectFirst("a.next") !== null };
  },

  async details(id) {
    const doc = html.parse((await http.get(kura.baseUrl + id)).body);
    return {
      id,
      title: doc.selectFirst("h1").text(),
      altTitles: doc.select(".alt-title").map((e) => e.text()),
    };
  },

  async episodes(id) {
    const doc = html.parse((await http.get(kura.baseUrl + id)).body);
    return doc.select(".episodes a").map((a) => ({ id: a.attr("href"), number: Number(a.attr("data-n")) }));
  },

  async videos(episodeId) {
    const doc = html.parse((await http.get(kura.baseUrl + episodeId)).body);
    return [{ url: doc.selectFirst("video source").attr("src"), server: "Main" }];
  },
});
```

## 6. Testing: the kura tool

`kura-cli-windows-x64.zip` on the
[Releases page](https://github.com/PROPULSORE/kura/releases) holds `kura.exe`, the
command-line tool. It runs extensions with the same engine as the app.

```
kura check my-extension                          # manifest, script, required functions
kura run   my-extension search '"frieren"' 1 '{}'  # live call on the real site, prints JSON
kura run   my-extension details /anime/1 --save  # same, and saves the pages for tests
kura test  my-extension                          # offline, from the saved pages
kura pack  my-extension                          # the zip users install
```

`run` takes the function name and its arguments as JSON values. In Git Bash, set
`MSYS_NO_PATHCONV=1` first, or arguments such as `/anime/1` become Windows paths.

`kura test` answers every request from `tests/fixtures.json` (written by
`run --save`) and checks the calls in `tests/cases.json`. An expectation matches
when every key it gives has that value; a list matches when its first elements do.

```json
[
  { "call": "search", "args": ["frieren", 1, {}],
    "expect": { "items": [{ "id": "/anime/1", "title": "Frieren" }] } },
  { "call": "episodes", "args": ["/anime/1"], "expect": [{ "number": 1 }] },
  { "call": "details", "args": ["/anime/gone"], "expectError": "NOT_FOUND" }
]
```

Each case has `call`, `args` (optional) and either `expect` or `expectError`
(`NOT_FOUND`, `CHANGED`, `NETWORK`). Other fields are refused, so a typo such as
`"expected"` is caught. Exit codes: `0` all good, `1` a check or case failed, `64`
wrong usage; `--verbose` shows the details of an unexpected error.

## 7. Sharing

### As a zip

Put `manifest.json`, `main.js` and the icon in a zip (`kura pack` does it). In
Kura: **Profile › Extensions › ⋮ › Install from zip files**. Zip installs do not
update by themselves.

### As a catalog

A catalog lets users get updates. It is a folder of static files on any HTTPS host,
for example a GitHub repository:

```
my-catalog/
├── keys/catalog.pub          # your public key
├── extensions/<name>/        # one folder per extension, with tests/cases.json
└── catalog/                  # written by kura sign: index.json, index.json.sig, key.pub
```

1. **Once, create your key:** `kura keygen my-keys`. It asks a password (12+
   characters) and writes `catalog.key` and `catalog.pub`. Copy `catalog.pub` to
   `keys/catalog.pub`. **Never publish `catalog.key`**: keep it and its password
   safe. If you lose it, users must add the catalog again.
2. **At every update:** raise the extension's `version`, then
   `kura sign my-catalog --key my-keys/catalog.key --name "My catalog"`. It tests
   every extension, lists each failing one as `FAIL`, refuses to sign if any
   fails, and otherwise writes `catalog/`. Never edit
   `catalog/index.json` by hand after signing. Then commit and push.
3. **Check:** `kura verify my-catalog` checks the signature and files as the app does.
4. **Share the index address**, for example
   `https://raw.githubusercontent.com/<you>/<repo>/main/catalog/index.json`.

Users add it in **Profile › Extensions › Catalogs**. Kura shows your public key with
a warning that the catalog is **not official**, and from then on accepts only
updates signed by that key. Kura refuses unsigned catalogs and changed files.

Contract version `0` may still change before version 1.
