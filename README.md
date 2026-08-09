# TAK Video Wall

**ATAK plugin for simultaneous multi-stream video monitoring: adaptive paged grid, CoT-based feed discovery, snap-to-sender map integration.**

ATAK's built-in video player shows one feed at a time. TAK Video Wall runs an independent decoder per feed and tiles them into a single wall, so an operator can watch every drone, body cam, and fixed camera in an incident at once — spot activity on one feed, and jump straight to that sender's location on the map.

---

## Features

### Automatic feed discovery
Any CoT marker advertising video appears in the feed list on its own — drone PLIs carrying a video detail, EUDs streaming their camera, fixed cameras publishing into the TAK stack. Liveness tracks the sender's own field-of-view reporting: a feed appears the moment its sensor cone appears on the map, and drops off when the sender stops streaming. No manual URL entry, no stale entries.

### Adaptive tiling — no wasted space
The grid picks the row/column split that maximizes the on-screen area of the videos themselves, for any feed count and any screen shape. Two feeds fill the pane side-by-side or stacked (whichever shows more video), three tile as 2+1 with the odd feed spanning full width, four form a clean 2×2. There is never an empty cell or a letterboxed gap at the edges.

### Paged wall with a decode budget
Feeds beyond the first four move to additional 2×2 pages with a pager bar in its own strip below the video. Only the visible page decodes — off-page feeds stop cleanly — so the wall stays inside the device's hardware decoder limit no matter how many feeds are added. Scan a large incident four feeds at a time without ever exhausting the codec pool.

### Snap-to
Every tile carries the standard TAK pan-to control. One tap collapses the wall to a single feed beside the map, centered on the marker that is publishing it — see the video and the location together, then one tap returns to the grid page you came from.

### Feed list with sender telemetry
The feed drawer shows each sender the way the map does:

- The marker's own **2525 symbol** in its team color — the UAS icon for a drone, the team-colored PLI dot for a person
- **Team name** and connection protocol
- A live **battery gauge** with the level reported by the sending EUD (green / amber / red)
- The same **pan-to control** as the map, so you can locate a sender before ever playing its feed

### Map-view filter
A "Show all" toggle limits the list to senders inside the current map view, using ATAK's own field-of-view filter — the same one Overlay Manager uses — so it agrees with the map under rotation and tilt. Working a sector? See only the feeds in it.

### Seamless resize
Expanding the wall to full screen (and collapsing back) resizes in place. Streams are never reconnected for a layout change — no spinner, no gap in playback.

### Lightweight by design
The plugin bundles **no native libraries and no codecs**. All decoding and rendering runs through ATAK's own video stack, in-process — the APK is under 40 KB.

---

## Compatibility

Official ATAK release builds are version-matched. Install the APK that corresponds to the ATAK version on the device:

| Plugin APK | ATAK version |
|---|---|
| `ATAK-Plugin-TAKVideoWall-1.0--5.6.0-civ-release.apk` | ATAK-CIV **5.6.x** |
| `ATAK-Plugin-TAKVideoWall-1.0--5.7.0-civ-release.apk` | ATAK-CIV **5.7.x** |

Both APKs are TPC-signed release builds from the tak.gov third-party pipeline.

## Installation

1. Download the APK matching your ATAK version from **[Releases](../../releases)**.
2. Install it on the device (`adb install`, or side-load the file and open it).
3. In ATAK, the plugin is picked up automatically — confirm it is loaded under **Settings → Tool Preferences → Plugins** if it doesn't appear.
4. A **Video Wall** button is added to the ATAK toolbar.

## Usage

1. Tap **Video Wall** in the toolbar. The wall opens with the live feed list.
2. Tap a feed's **play** button to add it to the wall. Tap **+** to open the list again and add more — the grid re-tiles as you go.
3. **Double-tap** a tile to spotlight it full-bleed; double-tap again to restore the grid.
4. Tap a tile's **pan-to** control to collapse to that single feed beside the map, centered on its sender.
5. Use **‹ ›** to page when more than four feeds are on the wall; **⛶** toggles full screen; **✕** removes a feed.
6. Feeds appear and disappear from the list automatically as senders start and stop streaming.

## Notes

- Feeds are discovered from the local ATAK's map state, so anything visible to the device — direct, via TAK Server, or federated — is eligible.
- Feed URLs are never displayed in the UI; streams carrying embedded credentials stay off-screen.
- Hidden feeds (off-page, or while the plugin is closed) do not decode, spending no battery or bandwidth.

## Version history

**v1.0** — Initial release. Adaptive grid, paged 2×2 wall, CoT feed discovery with FOV-based liveness, snap-to, feed drawer with 2525 symbols / team / battery, map-view filter, full-screen toggle with uninterrupted playback. Builds for ATAK-CIV 5.6 and 5.7.
