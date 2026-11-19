# Jordan Yeo

**Computer Science in Real-Time Interactive Simulation (RTIS) | Student at DigiPen Institute of Technology Singapore**

Systems, graphics, and gameplay programmer building custom C++ engines, cross-platform OpenGL ES rendering pipelines, and low-level simulation tools.

* **Focus Areas:** Real-Time Rendering (`C++20`, `OpenGL ES 3.0`, `OpenGL 4.3`, `GLSL`), Mobile Systems (`Android NDK/JNI`), Multiplayer Networking (`Winsock TCP`)

## Engineering Case Studies

### 1. Runi — Cross-Platform Running & Ghost-Racing Engine

**Role:** Graphics & Systems Programmer | **Stack:** `C++20` · `OpenGL ES 3.0` · `OpenGL 4.3` · `Android JNI / Kotlin` · `SDL3` · `Mapbox` · `FreeType`

* **The Problem:** High-level mobile UI wrappers introduce visible latency and marker jitter when rendering live GPS telemetry, multi-ghost race replays, and particle effects over interactive vector maps.

* **The Constraint:** Sustain a locked **60 FPS** within a strict $\le 10$ **draw calls per frame** budget on physical mobile hardware (**Google Pixel 9a**) while maintaining $< 0.5\text{ px}$ **overlay alignment** across map zoom tiers **Z12 through Z18**.

* **What I Tested:** Unified the core renderer across Android (`GLSurfaceView` over `Mapbox MapView`) and Desktop (`SDL3`), stress-testing 1 player + 3 simultaneous ghost runners, pace-driven route ribbons, fading ring-buffer trails, and multi-zoom coordinate projection (`Z12–Z18`) via `adb logcat` and headless `CTest` offscreen FBO image diffs.

* **What Failed:** Rendering individual FreeType labels per racer risked breaching the $\le 10$ draw-call ceiling under multi-ghost load, while missing Mapbox tokens and offline states caused early Android startup failures.

* **What Changed:** Built a **single-draw-call packed FreeType glyph atlas**, standardized world Mercator-to-screen transforms across both platforms, added offline tile/token guards, and implemented an automated headless FBO regression test comparing rendered frames against reference PNGs.

* **What Happened:** Verified $< 0.5\text{ px}$ **maximum alignment drift** across **Z12–Z18** and a locked **60 FPS** at $\le 10$ **draw calls/frame** on physical Pixel 9a hardware.

### 2. BitBlast — 2D Multiplayer Pixel-Art Tank Shooter

**Role:** Network, Particle & Gameplay Systems Programmer | **Stack:** `C++` · `Winsock (TCP)` · `Alpha Engine`

* **The Problem:** Build a real-time 2D pixel-art multiplayer tank shooter from scratch in C++ without a commercial game engine's built-in networking or VFX tools.

* **The Constraint:** Keep tank movement, combat state, and hundreds of active explosion particles synchronized across connected clients on a custom engine loop without frame drops or state desync.

* **What I Tested:** Tested multi-client TCP state replication and high-density combat particle bursts across local/LAN setups while profiling physics and gameplay loop stability.

* **What Failed:** Early builds hit Windows Firewall connection blocks, client-server state drift when packet timing varied, and frame-time spikes when spawning hundreds of unpooled particles during multi-tank combat.

* **What Changed:** Implemented server-authoritative tickrate synchronization with a client-server history queue over **Winsock TCP**, built a lifecycle-managed C++ particle system to render hundreds of active particles cleanly, and optimized core physics and gameplay loops.

* **What Happened:** Shipped a stable, responsive multiplayer tank shooter with synchronized client state and punchy explosion effects.

### 3. Duck Duck Goods - Duck Shopping Survival Game (48-Hour Game Jam)

**Playable Web Build:** [Play in Browser on itch.io](https://jaslynnn.itch.io/duck-duck-goods) | **Source:** Private Team Repo (GameJam+ Global 26/27)

**Role:** Gameplay & Economy Systems Programmer | **Stack:** `C#` · `Unity` · `WebGL`

* **Problem:** Ship a complete, replayable shop-survival game under the theme "One More Time" with a 4-person team inside a strict 48-hour game jam window.

* **Constraint:** Zero room for scope creep or fragile state logic, as every mechanic had to be playable, balanced, and bug-free in a browser build within 48 hours.

* **What Failed:** Early prototype runs lacked risk-reward tension between rounds, and players could soft-lock their economy if they overspent before unlocking higher-tier shop items.

* **What Changed:** Built a keyboard-controlled shopping survival loop in Unity (C#) backed by a Waddles movement resource economy, a cashback carryover system between rounds, and a 10-day progressive shop catalogue expansion.

* **What Happened:** Delivered a finished WebGL build within the 48-hour deadline that runs directly in the browser with balanced multi-day progression and replayability.

## Project Summary

| Project | Domain | Repository Status | Core Tech | 
| :--- | :--- | :--- | :--- | 
| **Runi** | Gamified Mobile Running App | Private Academic Repo | `C++20`, `OpenGL ES 3.0`, `Android JNI`, `SDL3` | 
| **BitBlast** | 2D Multiplayer Tank Game | Private Academic Repo | `C++`, `Winsock (TCP)`, `Alpha Engine` | 
| **Duck Duck Goods** | 3-Day Shop Survival Game (48-Hour Jam) | [Play in Browser (itch.io)](https://jaslynnn.itch.io/duck-duck-goods) | `C#`, `Unity` |

## Core Technical Stack

* **Languages:** `C++17/20`, `C`, `C#`, `GLSL`, `Kotlin`, `Python`

* **Graphics & Simulation:** `OpenGL ES 3.0`, `OpenGL 4.3 Core`, `FreeType`, `SDL3`, Custom Spatial & Mercator Projection Math

* **Systems & Networking:** `Android NDK/JNI`, `Winsock (TCP)`, POSIX IPC (`pthreads`, `ucontext`, pipes), `CMake` / `CTest`
