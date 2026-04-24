+++
title = "Linuxdownload.org, vibecoded end-to-end"
description = "A new toy project, built exclusively with AI tools"
date = 2026-04-24

[taxonomies]
tags = ["Linux", "AI", "side-project"]

[extra]
copy_button = true
+++

## A new toy project

Meet [linuxdownload.org](https://linuxdownload.org), my latest weekend toy. The idea is simple: make it easier for someone curious about Linux to actually get started. The site has side-by-side distro comparisons, a "which distro fits me" quiz, an app-equivalent finder (think: "what do I use instead of Photoshop?"), gaming readiness scores, post-install setup generators, and even a Windows 10 migration guide for those finally jumping ship now that [Win10 is EOL](https://www.microsoft.com/en-us/windows/end-of-support). Over 20 distros covered so far, from the obvious (Ubuntu, Debian, Fedora) to the more exotic (CachyOS, Bazzite, NixOS, Tails).

## Built exclusively with AI tools

What's interesting about it, at least to me: I didn't write a single line of code or push a single pixel by hand. Every part of the project, design, frontend, backend, scraper, infra, was created with AI tools.

For the design and overall vibe, I used [Google Stitch](https://stitch.withgoogle.com/) to mock up the layout and color palette. Surprisingly, the output didn't have that generic "AI-generated UI" look that everything seems to default to these days.

For the code, I leaned on [qwen3-coder](https://qwenlm.github.io/blog/qwen3-coder/) running locally on the [Ryzen AI machine](/blog/year-of-the-linux-desktop/) for the cheap, fast iteration loop, and [Claude Code](https://www.claude.com/product/claude-code) for the heavier lifting. The stack is FastAPI + SQLite on the backend, [Caddy](https://caddyserver.com/) in front, and a Python scraper that auto-detects the latest ISOs and their SHA sums for each distro on a schedule, so the download links and checksums never go stale. All of it agent-written.

## Is "vibecoding" actually viable?

For a toy project like this? Absolutely. From zero to a deployed, working site in a couple of evenings. The catch: you still need to know what you want, when something is off, and how to wire the pieces together. The AI is fast at typing; it's still you doing the thinking.

Anyway, give it a spin: [linuxdownload.org](https://linuxdownload.org). Feedback welcome.
