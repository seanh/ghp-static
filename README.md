# ghp-static

A GitHub Actions reusable workflow for deploying static files to GitHub Pages -
no Jekyll or static site generator, just deploy a directory of static
files directly to your GitHub Pages site.

Usage
=====

1. Enable GitHub Pages in your repo: go to **Settings &rarr; Pages** and choose **GitHub Actions** as the **Source**:

   ![GitHub Pages deployment settings](/settings.png)

2. Add a `.github/workflows/pages.yml` file to your repo with these contents:

   ```yaml
   name: Deploy static files to GitHub Pages
   on:
     push:
       branches: ["main"]
     workflow_dispatch:
   jobs:
     Deploy:
       uses: seanh/ghp-static/.github/workflows/static.yml@main
       with:
         path: 'site/'
       permissions:
         contents: read
         pages: write
         id-token: write
   ```

   Replace `'site/'` with the path to the directory in your repo that contains
   the static files (`'.'` if they're in the root directory).

   You may want to replace the `@main` with the ID of a specific commit in this
   repo in order to pin the version of the reusable workflow that you're using.
   For example: `uses: seanh/ghp-static/.github/workflows/static.yml@9a13b3aad0068ddf819d72a37f94061f9358e72f`

3. Go to the **Actions** tab in your repo
   (`https://github.com/YOUR_USER/YOUR_REPO/actions`) and you should see a
   **Deploy static files to GitHub Pages** workflow running.

4. Once the workflow completes you should see your static site deployed at
   your repo's GitHub Pages URL: `https://YOUR_USER.github.io.` for a user or
   organization site, or `https://YOUR_USER.github.io/YOUR_REPO` for a project
   site.

For an example see [this repo's own `pages.yml` workflow](.github/workflows/pages.yml) which deploys [this repo's `site/` directory](site/) to <https://seanh.github.io/ghp-static/>.
