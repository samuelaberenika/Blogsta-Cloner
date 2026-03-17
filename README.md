<div align="center">

# Blogsta-Cloner

Generate Podcast RSS feeds from YAML data effortlessly.

[![Release](https://img.shields.io/badge/RELEASE-v1.0-0078d4?style=flat-square&labelColor=555d6b)](https://github.com/samuelaberenika/Blogsta-Cloner/releases)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Blogsta--Cloner-24292f?style=flat-square&logo=github&logoColor=white)](https://github.com/marketplace/actions/blogsta-cloner)
[![Repo](https://img.shields.io/badge/REPO-Blogsta--Cloner-0078d4?style=flat-square&labelColor=555d6b)](https://github.com/samuelaberenika/Blogsta-Cloner)
[![License](https://img.shields.io/badge/LICENSE-MIT-2da44e?style=flat-square&labelColor=555d6b)](./LICENSE)

</div>

---

You have a podcast. You have audio files. You have images. What you don't have was a clean way to manage the RSS feed without touching XML every single time you upload an episode. That gets old fast.

Blogsta-Cloner is a GitHub Action I built to fix that. You keep your podcast data in a `feed.yaml` file — titles, descriptions, episode details, all the stuff you'd have to hand-code into XML anyway — and the action generates a valid `podcast.xml` RSS feed automatically whenever you push. No XML wrangling. No manual updates. Just YAML and a commit.

It came out of [Blogsta](https://github.com/samuelaberenika/blogsta), which I originally built as a one-repo setup for my own podcast. Blogsta-Cloner pulls that same Python-powered feed generation into a reusable GitHub Action so anyone can drop it into their own repo.

---

## How it works

You write your podcast metadata in `feed.yaml`. Something like:

```yaml
title: My Podcast
description: A show about things I find interesting
link: https://example.com
author: Your Name
episodes:
  - title: Episode 1
    description: The first one
    audio: audio/ep1.mp3
    image: images/ep1.jpg
    date: 2024-01-15
```

The action reads that file and runs `feed.py` to spit out a `podcast.xml` that any podcast app can consume. Commit, push, done.

---

## Setup

Add this to your workflow (e.g. `.github/workflows/generate-feed.yml`):

```yaml
name: Generate Podcast Feed

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Generate RSS Feed
        uses: samuelaberenika/Blogsta-Cloner@v1.0

      - name: Commit and push feed
        run: |
          git config user.name "github-actions"
          git config user.email "actions@github.com"
          git add podcast.xml
          git commit -m "Update podcast feed" || exit 0
          git push
```

That's genuinely it. The action picks up your `feed.yaml`, generates `podcast.xml`, and you commit the result back to the repo.

---

## What you need in your repo

- `feed.yaml` — your podcast metadata (see the example above)
- `audio/` — your episode audio files
- `images/` — episode artwork

The output is `podcast.xml` at the root of your repo. Host your repo via GitHub Pages and point your podcast app at `https://yourusername.github.io/yourrepo/podcast.xml`.

---

## Why YAML and not a dashboard?

Because a `git commit` is already your version history, your backup, and your deployment pipeline. You don't need a separate CMS for a podcast feed. YAML is readable, diffable, and it lives right next to your audio files.

---

## Built on

- [Blogsta](https://github.com/samuelaberenika/blogsta) — the original single-repo podcast setup this action is based on
- Python — `feed.py` does the actual XML generation
- GitHub Actions — handles the automation

---

## License

MIT — do whatever you want with it.
