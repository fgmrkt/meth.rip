# meth.rip

A one-page links site. Everything lives in `index.html` — no build step, no
dependencies, no npm. Edit the file, commit, done.

## Deploy

1. **Settings → Pages → Source: Deploy from a branch → `main` / `root`.**
2. **Settings → Pages → Custom domain:** `meth.rip` (the `CNAME` file in this
   repo already says so, so this should already be filled in).
3. Tick **Enforce HTTPS** once the certificate finishes provisioning — it can
   take up to an hour the first time.

At your domain registrar, point the domain at GitHub:

| Type  | Name | Value                                    |
|-------|------|------------------------------------------|
| A     | `@`  | `185.199.108.153`                        |
| A     | `@`  | `185.199.109.153`                        |
| A     | `@`  | `185.199.110.153`                        |
| A     | `@`  | `185.199.111.153`                        |
| CNAME | `www`| `fgmrkt.github.io`                       |

## Editing it

Open `index.html` and scroll to the bottom. Two blocks are all you need:

```js
const CONFIG = {
  name:       "fgmrkt",          // the big text
  bio:        "everything, one place.",
  status:     "The Complex",     // the little line up top
  youtubeId:  "3jqt7MxifiU",     // background video — the bit after "v="
  trackTitle: "Breaking Bad 「Edit」",
  trackSub:   "Money Trees · Jemartob",
  counterKey: "meth-rip",        // set to "" to hide the view counter
};
```

```js
const SOCIALS = [
  { name:"TikTok", handle:"@atlas", url:"https://www.tiktok.com/@atlas", color:"#25F4EE", icon:"tiktok" },
  // ...add, remove or reorder freely — the list renders in this order
];
```

To add a platform you also need an icon. Add an entry to the `ICONS` object
(any 24×24 SVG path works) and reference its key in `icon`.

An entry with `copy:` instead of `url:` copies the handle to the clipboard when
clicked, which is what the Discord row does — Discord has no public profile URL
you can build from a username alone.

## About the background

The background is the YouTube video embedded as a full-bleed player:
desaturated, dimmed, looping, and unmuted the moment someone clicks to enter.

It's done this way on purpose:

- **A GIF can't carry audio.** The format has no sound track at all. A GIF of a
  3-minute video would also land somewhere north of 100 MB, which is over
  GitHub's file limit — that's the wall you hit with `meth.mp4`.
- **Embedding costs you nothing to host.** No large file in the repo, no
  bandwidth, and YouTube keeps the rights side clean for footage and music that
  aren't yours.

Browsers block audio until someone interacts with the page — that's why the
`enter` screen exists. It isn't decoration, it's the thing that legally lets
the sound start.

If you'd rather self-host, drop a `bg.mp4` next to `index.html` and swap the
`#ytwrap` div for a `<video autoplay muted loop playsinline>`. Keep it under
50 MB, keep it muted, and run your audio from a separate short `<audio loop>`
file. Anything bigger belongs on a CDN, not in git.

## Things that will look broken but aren't

- **View counter missing.** It hides itself if the counter API doesn't answer.
- **No video, just drifting lights.** The canvas backdrop is the fallback and
  runs whenever the YouTube player can't load. The site still works.
