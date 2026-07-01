# doubletap.sskplay.com

A tiny, self-contained web probe for diagnosing **double-tap / double-click**
behavior — built to debug the [AirPlay Touch](https://github.com/ssk-play/airplay_touch)
companion, where a human double-taps the Android mirror surface and the macOS
companion synthesizes a double-click on the Mac.

## Why

A synthetic double-click only "counts" if the browser/OS sees the two clicks as a
pair: close enough in **time**, close enough in **position**, and (for synthetic
events) with the click-count surviving to the receiving app. This page shows,
live, exactly what the browser received so we can tell *which* of those failed on
a given machine.

## What it measures

Open it in the mirrored Mac's browser, then double-tap via the Android touchback
(or just double-click/tap directly). For every `click` it logs:

- **detail** — the browser's click count (a real double-click reaches `detail=2`)
- **Δt** — milliseconds since the previous click
- **Δpx** — distance from the previous click (the jitter)
- **x / y** — coordinates
- and a green **dblclick** row when the `dblclick` event actually fires

The verdict banner turns green on a recognized double-click, red when the second
tap was counted as a fresh single click (`detail=1`) — with the gap and distance
that explain why.

## Deploy

Static single file. Served via GitHub Pages at `doubletap.sskplay.com`
(`CNAME` + a Cloudflare `CNAME doubletap → ssk-play.github.io` record).
