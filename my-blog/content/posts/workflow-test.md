+++
date = '2025-06-27T17:00:35+09:00'
draft = false
title = 'Workflow Test'
+++

# Github Actionsを使って自動デプロイ

## やりたいこと
- mainブランチにpushすると自動的にデプロイされるようにしたい 
## やり方
- 以下のyamlファイルを.github/workflowにおく
```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main  # ← mainにpushされたときに実行される

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v3

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'

      - name: Build site
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages
```
## 別のやり方
- github公式のhugoのworkflowがあるので、それを利用する