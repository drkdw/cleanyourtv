# now_playing: a live now-playing bar under the clock

A fork of this repo's launcher with one addition, the `now_playing` theme key (off by default). It shows what an
app plays right now in a bar under the clock, laid out like Android TV's own now-playing card:

- the album art or the app's icon, with moving equalizer bars while it plays and a pause sign while paused;
- the title scrolling over the artist and the app;
- previous, next and stop beside it. OK on the bar pauses and resumes. Stop pauses an app without a real stop
  (Spotify) and hides the bar until it plays again;
- below the dock the bar folds into a small pill in the top bar.

A paused session only shows when Home saw it play in the last 30 minutes, so an app's leftover pause from days
ago stays hidden.

![The bar under the clock](docs/switches/now_playing.jpg)

## Permissions

No new permission and no network. It reads the apps' media sessions through the launcher's existing
GuardRevival notification listener, which you allow once:

```bash
tools/tv.py 'cmd notification allow_listener com.gathin.tvhome/.GuardRevival'
```

Without it the bar stays hidden. Nothing runs with the key off, and with it on the launcher only listens while
Home is started (no polling).

## Turn it on

Add `"now_playing": true` to your theme's `config.json` and push it with `tools/theme.sh`, or set
`now_playing` to `true` in `launcher/app/src/main/res/values/config.xml` before you build.

## Why a fork

The release APK grows by about 4.4 KB, just over the upstream size gate, so it lives here
([PR #2730](https://github.com/Gathin23/cleanyourtv/pull/2730)).

Tested on a Philips 2021/22 UHD (TP Vision, MediaTek), Android TV 11, with Spotify, SmartTube and Stremio.
