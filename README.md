# A Society Lab @ KAIST (ASK): The Website

Welcome to the source for [the lab website](https://emwithanm.github.io/society.github.io/), currently served via GitHub Pages! This repo started as a fork of [Litlab's website repo](https://github.com/litlabkaist/litlabkaist.github.io), so some structure/conventions carry over from that. 

## Structure

Flat, plain HTML/CSS/JS, without any build step, framework, or Jekyll templating (no `_config.yml`, no layouts/includes). Each page is fully self-contained with its own `<style>` block.

```
index.html         Homepage (intro blurb + News section)
people.html         People (PI, Postdocs, Researchers, Students)
research.html        Research projects
publications.html      Publications, grouped by year
style.css          Shared base styles (nav, footer, etc.)
script.js          Shared JS
img/              Images, organised by page (img/news/, img/research/, etc.)
CNAME             Custom domain config for GitHub Pages
```

## Previewing Locally

No Ruby/Jekyll setup is required for editing, but `jekyll serve` is a convenient way to preview since there's no build step to worry about:

```bash
jekyll serve --watch
```

Then, open http://127.0.0.1:4000. `--watch` auto-rebuilds when you save a file, so you can just refresh the browser tab. If you ever see a "not found" error, the `_site/` build folder may be stale/missing—please stop the server (`Ctrl+C`) and rerun `jekyll serve`.

## Editing Content

- **News** (`index.html`): Add new `<div class="news-item">` entries at the top of `#newsGrid`, newest first. Only the first 6 show by default—older ones appear after clicking "Show More".
- **People** (`people.html`): Each person is a `<div class="person-card">` inside the relevant section (`Principal Investigator` / `Postdocs` / `Researchers` / `Students`). To add a photo, be sure to uncomment the `<!-- <div class="image-container">...</div> -->` block and point `src` at the real image (portrait crop, about 200px wide on desktop).
- **Research** (`research.html`): Each project is a `<div class="research-project">` block with a title, keyword pills, optional image, and description.
- **Publications** (`publications.html`): Grouped by `<h2>` year. I suggest keeping the author's name bolded (e.g., `<strong>Jeon, J.</strong>`) and journal names italicised, consistent with existing entries.

**Styling Convention:** The accent purple used throughout (names, links, dates, project/publication titles) is `#611e7b`—feel free to reuse it for new elements, or replace it with a different colour better fitting.

## To-Do

- `people.html`: Some members currently have "Placeholder" text for degree/keywords/email/bio, and everyone's photo is commented out, pending real images.
- `publications.html` and `research.html` are awaiting more information.
- All logos are placeholders from Google Images, and the favicon is still Litlab's.
- A tagline on `index.html`, underneath the main heading, would be a nice touch.

## Deployment

GitHub Pages serves directly from the `main` branch root—**anything pushed to `main` goes live immediately**, without any review/build step in between.

### Custom Domain Status

Our intended domain is `society.kaist.ac.kr` (see `CNAME`), but it is not live yet, as GitHub requires verifying domain ownership before it'll accept a custom domain (anti-takeover protection). As per [Github's instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site):

1. Go to the repo's Settings > Pages (or https://github.com/settings/pages for account-level verification) > "Add a domain".
2. GitHub provides a TXT record to add to DNS.
3. Since this is a `kaist.ac.kr` subdomain, whoever manages KAIST's DNS zone needs to add that record.
4. Once verified, set `society.kaist.ac.kr` as the Pages custom domain (Settings > Pages > Custom domain).

Please note that until then, the site is only reachable at the default GitHub Pages URL for this repo.

**I would avoid switchinf the internal nav links back to root-relative paths** (e.g. `href="/people"`). They're intentionally relative (`href="people"`) so navigation works correctly both under the default GitHub Pages URL (which includes a repo-name subpath) and once the custom domain goes live at root—root-relative links break under the subpath.
