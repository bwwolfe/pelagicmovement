# Pelagic Movement website

Source for [pelagicmovement.com](https://pelagicmovement.com), built with [Quarto](https://quarto.org) and published to GitHub Pages by a GitHub Actions workflow on every push to `main`.

## What is where

| File | What it holds |
|:--|:--|
| `index.qmd` | Home page: intro, research themes, student project cards, study with me |
| `research.qmd` | Student projects and collaborations, each with margin facts and a photo |
| `people.qmd` | About page: bio, students, teaching, collaborators, study with me |
| `publications.qmd` + `data/publications.yml` | Publication list; add papers to the YAML file |
| `credits.qmd` | Photo credits (keep this up to date while any placeholder photos remain) |
| `_quarto.yml` | Site settings, navigation bar and footer |
| `styles/theme.scss` | Colours, fonts and layout |
| `images/` | Logo, favicon and (later) your own photos |
| `CNAME` | The custom domain |
| `.github/workflows/publish.yml` | Renders and deploys the site |

Margin notes use Quarto's `::: {.column-margin}` blocks. Quarto lines a margin block up with the block just before it, which is easy to get wrong, so every section that has a margin note is wrapped in its own grid with the note first:

```
:::: {.project .page-columns .page-full}
::: {.column-margin}
The margin note, photo or facts.
:::

<h3>Heading</h3>

Body text.
::::
```

The note then starts level with the top of that section and never runs into the next one. Add `.theme` (as on the home page) to drop a text-only note down level with the heading, or `.intro` for the block under a page title.

## Replacing placeholder photos

The photos are CC BY 4.0 placeholders linked from iNaturalist and credited on `credits.qmd`. To use your own, copy the file into `images/` (around 2000 px on the long edge for the hero, 1200 px elsewhere, JPEG), change the image link in the page to `images/your-file.jpg`, update or remove the credit line under it, and remove its row from `credits.qmd`.

## Adding a publication

Copy an entry in `data/publications.yml`, keep newest first, and fill in `year`, `authors_before`, `me`, `authors_after`, `title` (use `<em>` for species names), `venue`, `details` and `doi`. An optional `note` shows in the margin.

## Previewing locally

Install Quarto from <https://quarto.org/docs/get-started/>, then from this folder run:

```
quarto preview
```

## Publishing

Pushing to `main` publishes the site. The first time:

1. Create an empty repository on GitHub (for example `pelagicmovement`) and push this folder to it.
2. In the repository go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. Under **Custom domain** enter `pelagicmovement.com` and save.
4. In Cloudflare, open the domain's **DNS** page and add these records with **Proxy status: DNS only** (grey cloud):
   - `A` records for `@` pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`
   - `AAAA` records for `@` pointing to `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153` and `2606:50c0:8003::153`
   - a `CNAME` record for `www` pointing to `<your-github-username>.github.io`
5. Back in **Settings → Pages**, tick **Enforce HTTPS** once GitHub has issued the certificate (this can take up to a day).
6. Optionally verify the domain under your GitHub account's **Settings → Pages → Add a domain**, which adds a TXT record in Cloudflare and stops anyone else claiming the domain on GitHub.

Check the **Actions** tab after each push; a green tick means the site is live.
