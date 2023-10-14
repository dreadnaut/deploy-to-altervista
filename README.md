# deploy-to-altervista

A GitHub Action to upload files to a website on Altervista, based on [git-ftp](https://github.com/git-ftp/git-ftp).

## Example workflow

Create a workflow file in your repository, for example `.github/workflows/publish-to-av.yml`.

```yaml
name: Publish updates to Altervista
on:
  push:
    branches:
      - main

jobs:
  deploy-via-ftp:
    runs-on: ubuntu-latest

    steps:
      - name: 📦 Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: 🌍 Upload to Altervista
        uses: dreadnaut/deploy-to-altervista@v0.1
        with:
          ftp-username: your-altervista-username
          ftp-password: ${{ secrets.ALTERVISTA_FTP_PASSWORD }}
          exclude-patterns: |
            .git*
            README.md
```

## Input parameters

| Input            | Description                                      | Required | Default         |
| ---------------- | ------------------------------------------------ | -------- | --------------- |
| ftp-username     | An Altervista username or FTP user               | ✔️       |                 |
| ftp-password     | Password for the FTP user                        | ✔️       |                 |
| local-root       | Only files under this directory will be uploaded |          | Repository root |
| remote-root      | Files will be uploaded under this FTP directory  |          | FTP root        |
| exclude-patterns | These files will be excluded from the upload     |          | `.git*`         |
