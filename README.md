<p align="center">
  <img src="screenshots/icon.png" width="96" alt="YT Shield icon">
</p>

<h1 align="center">YT Shield</h1>
<p align="center"><b>A quiet YouTube ad remover that YouTube doesn't notice, on laptop and phone.</b></p>

> **Showcase repository.** This page describes the project and shows it working. The source
> code is kept private and is not published here.

---

## The problem

Most ad blockers, including the one built into Opera GX, work by **blocking ad network
requests**. YouTube's player expects those requests to succeed. When they fail, it knows a
blocker is running and shows the *"Ad blockers are not allowed on YouTube"* warning.

## The approach

YT Shield doesn't block a single request. It runs inside the page before any YouTube code
and **removes the ad instructions from the data YouTube sends**, before the player reads it.
The player never learns an ad was planned, so it never asks for one, and nothing fails that
it could detect.

| Layer | What it does |
|---|---|
| **Data pruning** | Strips video ad breaks plus feed, search and Shorts promotions from YouTube's page data and API responses |
| **Stealth** | The few browser functions it hooks still look like untouched built-in code to anything that inspects them |
| **Safety net** | If an ad ever gets through, it is muted, played at 16× and skipped automatically |
| **Warning removal** | If the anti-adblock dialog appears, it is dismissed and playback resumes |
| **Cosmetic backup** | Any leftover ad containers are hidden |

## Platforms

| Where | How |
|---|---|
| Chrome, Opera GX, Edge, Brave | Manifest V3 browser extension with a popup (on/off switch and live counters) |
| Android | Same engine as a userscript in Firefox + Violentmonkey |
| iPhone / iPad | Same engine as a userscript in Safari via the Userscripts app |

One shared engine is built into both the extension and the userscript, so every platform gets
the same protection.

## Screenshots

**Extension popup**

<img src="screenshots/popup.png" width="352" alt="YT Shield popup showing counters">

**Desktop: video starts immediately, no ad** · **Mobile site: no ad**

<p>
  <img src="screenshots/desktop-watch.png" width="560" alt="YouTube watch page with no ad">
  <img src="screenshots/mobile-watch.png" width="200" alt="Mobile YouTube with no ad">
</p>

**Search results with no promoted listings**

<img src="screenshots/desktop-search.png" width="560" alt="YouTube search with no promoted results">

## Test results

Tested automatically against live YouTube:

- **Without YT Shield:** YouTube served ad placements on the test videos.
- **With the extension:** no ad data reached the player, no ad played, no warning appeared,
  and every video played normally. In-app navigation and search results were also ad-free.
- **Mobile userscript:** no ads on the mobile YouTube site.
- **Result:** 15 of 15 live checks and 7 of 7 unit tests passed.

## Built with

JavaScript · Chrome Extensions Manifest V3 · Userscripts · Node.js test runner · Playwright

---

<p align="center">Built by <a href="https://github.com/Jinadev15">Jinadev15</a>. Source available privately.</p>
