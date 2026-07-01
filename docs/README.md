<!--
SPDX-FileCopyrightText: Copyright (c) 2025 Madison Nicole Goodwin https://github.com/NicoleDev021
SPDX-FileCopyrightText: Copyright (c) 2026 Small Steps Studio LLC smallsteps.studio

SPDX-License-Identifier: CC-BY-4.0
-->

# Interactive Wheel of Life

An interactive, printable Wheel of Life self-assessment tool. Rate 8 life categories across 10 rings each, track 10 yearly goals, customize the whole color scheme, and export your progress — all from a single self-contained HTML file with no build step and no external dependencies.

**[Live demo →](https://smallstepsstudio.github.io/Interactive-Wheel-of-Life/)**

---

## Features

- **Click-to-fill rating wheel** — 8 life categories, 10 rings each. Click any ring (or Tab + Enter/Space) to fill that category up to that level; click the same ring again to pull it back down.
- **Curved, hand-lettered category labels** that follow the circumference of the wheel itself.
- **Editable categories** — rename any of the 8 sections (12-character limit), and every dropdown and label updates automatically to match.
- **Full color system**:
  - Six built-in palettes: Cool, Warm, Pastel, Neon, Colorblind-Safe (Okabe–Ito), and Grayscale.
  - A custom color picker per section, for anyone who wants their own palette entirely.
- **10 Goals tracker** with a category tag per goal and freely wrapping text fields.
- **Save** — exports everything you've filled in (wheel progress, goals, colors, category names) as a new standalone HTML file you can reopen later and keep editing.
- **Print-ready** — a dedicated print layout tuned to fit one A4 sheet.
- **Fully offline** — all fonts are embedded directly in the file; it makes zero external network requests once loaded.
- **Accessible** — every clickable ring is keyboard-operable and screen-reader labeled, with a visible focus indicator that adapts its own color to stay legible against whatever's underneath it.

---

## Design & Coding Decisions

A few choices worth explaining, since they weren't the "default" way to build this:

**One self-contained HTML file, on purpose.** No framework, no build step, no external font or asset requests. That was a deliberate trade — it means the tool can be hosted anywhere (GitHub Pages, a single email attachment, a USB stick) and will render identically with or without an internet connection. The cost is a larger single file (fonts embedded as base64), which is a trade worth making for something meant to be portable and durable.

**Hex-based color system with derived "muted" variants.** Rather than hand-picking a light and dark shade for every possible color, every palette (built-in or custom) is stored as a single vivid hex value. A shared HSL-based function derives a matching pastel "muted" version from *any* color automatically — which is what makes the custom color picker actually usable, instead of requiring two picks per category.

**Guardrails on custom colors.** The color picker won't let a chosen color get close enough to the wheel's white separator lines to become illegible against them — it's clamped, not blocked, so the picker never fights you mid-drag.

**Curved labels via SVG `textPath` + `dominant-baseline: middle`.** Getting text to curve symmetrically around a circle — with the *same* visual spacing whether it's sitting on the top or bottom half — took a few iterations to get right, since the naive approach (reversing arc direction so bottom-half text doesn't read upside-down) has a side effect of misaligning how far the text sits from the ring. `dominant-baseline: middle` centers the text on its arc regardless of which direction the arc was drawn, which turned out to be the actual fix.

**A "reload guard" on every dynamically-built element.** The Save feature exports the live page as a new HTML file, which still contains the same script that originally built the page. Every piece the script constructs (the 80 clickable wedges, the labels, the goal rows, the color/category edit panels) checks first whether it's re-opening a previously saved file before building anything — otherwise reopening a save would silently duplicate every element on top of itself.

---

## Contributor Guidance

If you contribute to this repository, **please make sure to review and follow the community standards and reference the following files**:

- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md): Outlines the standards for behavior and participation in this community.
  _Please read and follow the Code of Conduct to help maintain a welcoming environment for all contributors._

- [`CONTRIBUTING.md`](CONTRIBUTING.md): Provides detailed guidelines on how to contribute to this project, including how to submit issues and pull requests, coding standards, and commit message conventions.
  _Please review these instructions before contributing to ensure your submissions align with the project's workflow and expectations._

- [`SECURITY.md`](SECURITY.md): Contains the process for reporting security vulnerabilities or concerns.
  _If you discover a security issue, please follow the instructions in this file to report it responsibly._

We appreciate your attention to these documents to help keep the project collaborative, secure, and compliant.

---

## License

**Source code** in this repository is licensed under the [GNU Affero General Public v3.0 or later (AGPL-3.0-or-later)](https://www.gnu.org/licenses/agpl-3.0.en.html).

**Documentation** (including the README, all files in the `docs/` directory, and all files in the `.github` directory) is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

For code files, you may see the following SPDX identifier at the top:
```
SPDX-License-Identifier: AGPL-3.0-or-later
```
For documentation files, you may see:
```
SPDX-License-Identifier: CC-BY-4.0
```

If you contribute, you agree that your contributions will be licensed under these terms.

---

## How This Was Built

This tool was built collaboratively with Claude (Anthropic) Sonnet 5 Medium Effort with Thinking, through an extended, iterative conversation — not a single prompt. Roughly, the process looked like:

- Starting from a rough concept (a Wheel of Life check-in, inspired by a specific video) and building it up feature by feature: the wheel itself, curved labels, category editing, the color system, save/print, and accessibility — each added and refined in its own back-and-forth.
- A real amount of trial and error, especially on the curved-text geometry — a few rounds landed on a fix that solved one symptom while introducing another, which got caught and corrected through actual testing (verifying the math directly) rather than assuming it was right.
- A dedicated final review pass specifically to check for bugs, redundancy, and security issues before treating the tool as finished — which did catch a real bug (custom colors not surviving a save/reopen cycle) that had been sitting undetected for several turns.

**Conversation length / cost:** this conversation ran long enough to use up a full Claude.ai usage session (100%), and continued into a second session, currently at 48% used. That's session-level usage as reported by the Claude.ai interface, not an exact token count — Claude.ai doesn't expose raw token numbers to users (that level of detail is only available via the Anthropic API/Console, which doesn't apply to Claude.ai conversations like this one). If you want a rough sense of scale: this was a single extended conversation across roughly one and a half full usage sessions, not a quick one-off prompt.
