<div align="center">

# Blogsta-Cloner

Generate Podcast RSS feeds from YAML data files effortlessly

[![Release](https://img.shields.io/badge/RELEASE-v1.0-0078d4?style=flat-square&labelColor=555d6b)](https://github.com/samuelaberenika/Blogsta-Cloner/releases)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Blogsta--Cloner-24292f?style=flat-square&logo=github&logoColor=white)](https://github.com/marketplace)
[![Repo](https://img.shields.io/badge/REPO-Blogsta--Cloner-0078d4?style=flat-square&labelColor=555d6b)](https://github.com/samuelaberenika/Blogsta-Cloner)
[![License](https://img.shields.io/badge/LICENSE-MIT-2da44e?style=flat-square&labelColor=555d6b)](./LICENSE)

</div>

---

## 🚀 Features

* YAML to RSS — Convert YAML files into Podcast RSS 2.0 feeds
* Automated Updates — Automatically regenerate your feed whenever you push changes to your repository
* Infrastructure as Code — Keep your podcast metadata version-controlled and history tracked
* Easy Hosting — Works perfectly with GitHub Pages to host your generated feed for free

---

## 📖 Usage

Create a workflow file in your repository:

.github/workflows/main.yml

### Example Workflow

This workflow listens for pushes to the main branch, generates feed.xml from your YAML file, and commits the result.

```yaml
name: Generate Podcast Feed

on:
  push:
    branches: ["main"]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Generate Podcast Feed
        uses: samuelaberenika/Blogsta-Cloner@v1.0
        with:
          source_file: "podcast.yaml"
          output_file: "feed.xml"

      - name: Commit Generated Feed
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"
          git add feed.xml
          git commit -m "Update podcast feed" || echo "No changes to commit"
          git push
```

---

## ⚙️ Configuration

### Inputs

| Input       | Description                                          | Required | Default      |
| ----------- | ---------------------------------------------------- | -------- | ------------ |
| source_file | Path to the YAML source file containing podcast data | Yes      | podcast.yaml |
| output_file | Filename for the generated RSS feed                  | No       | feed.xml     |

---

## 📄 YAML File Structure

Create a `source_file` (for example `podcast.yaml`) in your repository root.

```yaml
title: "My Awesome Podcast"
description: "A podcast about technology and coding."
link: "https://example.com"
language: "en-us"
author: "Samuel Aberenika"
email: "email@example.com"
category: "Technology"
image: "https://example.com/cover.png" # Optional podcast cover art

episodes:
  - title: "Episode 1: Getting Started"
    description: "Introduction to the series."
    pubDate: "2023-10-27"
    url: "https://example.com/audio/ep1.mp3"
    length: "12345678"
    type: "audio/mpeg"

  - title: "Episode 2: Deep Dive"
    description: "We dive deeper into the code."
    pubDate: "2023-11-03"
    url: "https://example.com/audio/ep2.mp3"
    length: "9876543"
    type: "audio/mpeg"
```

---

## 🛠️ Contributing

Contributions are welcome. If you have suggestions for improvements or find a bug, feel free to open an issue or submit a pull request.

1. Fork the repository
2. Create your feature branch

```
git checkout -b feature/AmazingFeature
```

3. Commit your changes

```
git commit -m "Add some AmazingFeature"
```

4. Push to the branch

```
git push origin feature/AmazingFeature
```

5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License.
See the `LICENSE` file for details.

---

## ⚠️ Disclaimer

This action is provided by a third party and is not certified by GitHub.
