# GitHub Action — generates an animated contribution‑snake every day
name: Generate Snake

on:
  # run automatically at 02:00 UTC (≈ 10 PM Toronto) every day
  schedule:
    - cron: "0 2 * * *"
  # allow manual re‑runs from the Actions tab
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    # ⚠️  Needed since the default GITHUB_TOKEN is read‑only on new repos
    #     (GitHub changed this in 2023) :contentReference[oaicite:0]{index=0}
    permissions:
      contents: write

    steps:
      - name: Generate snake SVG / GIF
        uses: Platane/snk@v3.3.0     # latest tag at time of writing :contentReference[oaicite:1]{index=1}
        with:
          # whose contribution graph to read
          github_user_name: ${{ github.repository_owner }}

          # output files (add or tweak colours if you like)
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/github-snake.gif
