<!--
***
SPDX-FileCopyrightText: 2020 Stagelab Coop SCCL
SPDX-License-Identifier: GPL-3.0-or-later
SPDX-FileContributor: Ion Reguera <ion@stagelab.coop>
***
-->

# FormitGo

<img src="https://stagesoft.github.io/img/formitgo.jpg" height="200">

**Open-source software for the synchronization and control of multimedia installations.**

Modular architecture, precise synchronization, and centralized management.

Website: [stagelab.coop/formitgo](https://stagelab.coop/formitgo/)

## What is FormitGo

**FormitGo** plays back video, audio and DMX lighting cues in sync across several networked machines. It is built on the **cuems** suite (Cue Management System), developed by [Stagelab](https://www.stagelab.coop) for theater and live-entertainment technicians.

<img src="https://stagesoft.github.io/img/original_fons_transparent.png" height=100>

- **Modular system.** One machine acts as the main controller, while the others function as client nodes. The power needed to manage multimedia content is distributed across multiple devices, instead of relying on a single centralized machine.
- **Precise synchronization.** Network-transmitted timecode with a resolution of up to a quarter of a frame keeps every element of your installation in sync. If any slight mismatch occurs, the system automatically and continuously readjusts.
- **Optimized installation.** You only need one network cable to connect each node, so devices can be placed exactly where they are needed: next to the projector, screen, or sound equipment.
- **Centralized management.** FormitGo is managed through a web interface, from any device connected to your local network, whether via cable or WiFi.
- **Simple installation.** FormitGo is a plug-and-play system: a documented power-up and self-configuration protocol makes it adjust itself automatically just by being turned on in a specific way.
- **International.** The interface is available in Catalan, Spanish, and English.

## How it works

```text
Browser (any device on the local network)
   |  HTTP + WebSocket
   v
Controller   cuems-frontend · cuems-editor · cuems-engine
   |  network timecode (MTC over RTP-MIDI) + cluster bus
   v
Nodes        cuems-engine ─┬─ video  → cuems-videocomposer
                           ├─ audio  → cuems-audioplayer (JACK)
                           ├─ DMX    → cuems-dmxplayer → OLA
                           └─ fades  → gradient-motion-engine
```

The controller also works as a node, so a single machine can run a whole show.

## Authoring notes

- **Looping audio with video.** Audio and video stay in sync across the passes of a loop only if **(A) their durations are exactly the same, or (B) they are in the same container** (one file: the audio player extracts the audio track). Two separate files of different lengths drift apart by the difference on every pass. Audio extracted from a video into a separate file comes out slightly longer than the video (the codec's padding), so keep audio and video that loop together in one file. The engine warns at load when two loops started together are close in length but not equal.

## Components

### Core

| Repository | What it does |
| --- | --- |
| [cuems-engine](https://github.com/stagesoft/cuems-engine) | Loads projects, generates the timecode and runs the cues on the controller and on every node. |
| [cuems-editor](https://github.com/stagesoft/cuems-editor) | Back end of the web interface: multi-user project editing and media library. |
| [cuems-frontend](https://github.com/stagesoft/cuems-frontend) | Web interface for programming and running shows. |
| [cuems-videocomposer](https://github.com/stagesoft/cuems-videocomposer) | Multi-layer video compositor with hardware decoding. |
| [cuems-audioplayer](https://github.com/stagesoft/cuems-audioplayer) | Audio player for JACK. |
| [cuems-dmxplayer](https://github.com/stagesoft/cuems-dmxplayer) | DMX lighting player with fades, output through OLA. |
| [gradient-motion-engine](https://github.com/stagesoft/gradient-motion-engine) | Timecode-driven fades and motion. |
| [cuems-utils](https://github.com/stagesoft/cuems-utils) | Shared Python library: cue model, XML schemas, configuration. |
| [cuems-common](https://github.com/stagesoft/cuems-common) | System configuration, services, controller and node roles, WiFi access point. |
| [cuems-midi-connector](https://github.com/stagesoft/cuems-midi-connector) | Wires the MIDI timecode on every machine automatically. |
| [cuems-nodeconf](https://github.com/stagesoft/cuems-nodeconf) | Discovers and adopts nodes on the local network. |
| [rtpmidid](https://github.com/stagesoft/rtpmidid) | Sends the timecode between machines over RTP-MIDI (fork). |

### Libraries

| Repository | What it does |
| --- | --- |
| [libmtcmaster](https://github.com/stagesoft/libmtcmaster) | MIDI Time Code generator. |
| [mtcreceiver](https://github.com/stagesoft/mtcreceiver) | MIDI Time Code receiver used by the players. |
| [oscreceiver](https://github.com/stagesoft/oscreceiver) | OSC receiver used by the players. |
| [cuems-mediadecoder](https://github.com/stagesoft/cuems-mediadecoder) | Shared FFmpeg decoding library. |
| [cuemslogger](https://github.com/stagesoft/cuemslogger) | System log wrapper for the C++ components. |

### Third-party software we maintain forks of

| Repository | What it does |
| --- | --- |
| [ola](https://github.com/stagesoft/ola) | DMX output (Open Lighting Architecture), with support for the Eurolite USB-DMX512 PRO MK2 interface. |
| [jack-volume](https://github.com/stagesoft/jack-volume) | Audio volume control on JACK, used by cuems-audioplayer. |

We also keep builds of [jackd2](https://github.com/stagesoft/jackd2) and [libossia](https://github.com/stagesoft/libossia) adapted to our systems, with no functional changes.

## Installation

FormitGo is already functional and in use in live shows and installations, and it is under active development towards its first release (Release 1). There is no standard installation method yet. It will be documented here when Release 1 is published.

FormitGo runs on **Debian 12 (bookworm), amd64**. In the meantime, you are free to install it from the source code on GitHub and experiment with it: each component's README explains how to build it. Questions are welcome on [Discord](https://discord.gg/VfDjFDSnGW) and in [GitHub Discussions](https://github.com/stagesoft/FormitGo/discussions). For a ready-to-use installation, contact Stagelab at info@stagelab.coop.

## Documentation

Each repository documents itself in its README. Some also publish technical documentation on GitHub Pages:
[cuems-engine](https://stagesoft.github.io/cuems-engine/),
[cuems-editor](https://stagesoft.github.io/cuems-editor/),
[cuems-utils](https://stagesoft.github.io/cuems-utils/),
[cuems-videocomposer](https://stagesoft.github.io/cuems-videocomposer/),
[cuems-nodeconf](https://stagesoft.github.io/cuems-nodeconf/) and
[gradient-motion-engine](https://stagesoft.github.io/gradient-motion-engine/).

## Community

- Chat with users and developers on [Discord](https://discord.gg/VfDjFDSnGW).
- Ask questions and share ideas in [GitHub Discussions](https://github.com/stagesoft/FormitGo/discussions).
- Report bugs in the issues of the repository concerned.

## License

This project is licensed under the terms of the **GNU General Public License v3.0 or later (GPL-3.0-or-later)**.

Being open-source software, **FormitGo** and the **cuems** suite do not depend on a single company: any group of developers can continue the project. Your infrastructure will never become obsolete or unsupported, and your equipment remains functional and versatile.

See the [LICENSE](https://github.com/stagesoft/FormitGo/blob/master/LICENSE) file for the full license text.

## Funding

This project is promoted by:

![promoted_by_gencat](https://stagesoft.github.io/img/generalitat.svg)

![promoted_by_ess](https://stagesoft.github.io/img/economiasocial.svg)

This project is funded by:

![funded_by_ministerio](https://stagesoft.github.io/img/ministerio.svg)

## Acknowledgements

- The first versions of FormitGo were developed in collaboration with [bTactic](https://www.btactic.com).
- cuems-videocomposer is inspired by and partially based on [xjadeo](https://xjadeo.sourceforge.net/) by Robin Gareus and on [mpv](https://mpv.io/).
