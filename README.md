Blogsta-Cloner

GitHub release (latest by date)GitHub MarketplaceGitHub stars

Blogsta-Cloner is a GitHub Action that generates a valid Podcast RSS feed from a YAML configuration file. It brings the power of the Blogsta engine to your CI/CD workflow, allowing you to manage your podcast as code.
🚀 Features

    YAML to RSS: Convert human-readable YAML files into standard Podcast RSS 2.0 feeds.
    Automated Updates: Automatically regenerate your feed whenever you push changes to your repository.
    Infrastructure as Code: Keep your podcast metadata version-controlled and history tracked.
    Easy Hosting: Pairs perfectly with GitHub Pages to host your generated feed for free.

📖 Usage

To use this action, create a workflow file in your repository (e.g., .github/workflows/main.yml).
Example Workflow

This workflow listens for pushes to the main branch, generates the feed.xml from your source YAML, and commits the result back to the repo.

name: Generate Podcast Feedon:  push:    branches: [ "main" ]  workflow_dispatch:jobs:  build:    runs-on: ubuntu-latest    steps:      - name: Checkout Repository        uses: actions/checkout@v3      - name: Generate Podcast Feed        uses: samuelaberenika/Blogsta-Cloner@v1.0        with:          source_file: 'podcast.yaml'   # Path to your YAML file          output_file: 'feed.xml'       # Desired output filename      - name: Commit Generated Feed        run: |          git config --global user.name "github-actions[bot]"          git config --global user.email "github-actions[bot]@users.noreply.github.com"          git add feed.xml          git commit -m "Update podcast feed" || echo "No changes to commit"          git push

 
⚙️ Configuration 
Inputs 
Input
 
	
Description
 
	
Required
 
	
Default
 
 
source_file	Path to the YAML source file containing podcast data.	Yes	podcast.yaml 
output_file	The filename for the generated RSS feed (e.g., feed.xml).	No	feed.xml 
   
YAML File Structure 

Create a source_file (e.g., podcast.yaml) in your repository root. Below is the supported structure compatible with the Blogsta engine: 
yaml
 
  
 
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
    length: "12345678"  # File size in bytes
    type: "audio/mpeg"
  - title: "Episode 2: Deep Dive"
    description: "We dive deeper into the code."
    pubDate: "2023-11-03"
    url: "https://example.com/audio/ep2.mp3"
    length: "9876543"
    type: "audio/mpeg"
 
 
 
🛠️ Contributing 

Contributions are welcome! If you have suggestions for improvements or encounter any bugs, please feel free to open an issue or submit a pull request. 

    Fork the repository. 
    Create your feature branch (git checkout -b feature/AmazingFeature). 
    Commit your changes (git commit -m 'Add some AmazingFeature'). 
    Push to the branch (git push origin feature/AmazingFeature). 
    Open a Pull Request. 

📄 License 

This project is licensed under the MIT License - see the LICENSE  file for details. 

Disclaimer: This action is provided by a third-party and is not certified by GitHub.
