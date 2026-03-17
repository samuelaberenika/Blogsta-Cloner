# Blogsta-Cloner

![GitHub release (latest by date)]()
![GitHub Marketplace]()
![GitHub stars]()

Blogsta-Cloner is a GitHub Action that generates a valid Podcast RSS feed from a YAML configuration file.  
It brings the power of the Blogsta engine to your CI/CD workflow, allowing you to manage your podcast as code.

---

## 🚀 Features

- YAML to RSS — Convert human-readable YAML files into standard Podcast RSS 2.0 feeds  
- Automated Updates — Automatically regenerate your feed whenever you push changes to your repository  
- Infrastructure as Code — Keep your podcast metadata version-controlled and history tracked  
- Easy Hosting — Works perfectly with GitHub Pages to host your generated feed for free  

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
