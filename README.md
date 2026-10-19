# debmandal.github.io

Academic homepage of Debmalya Mandal, built on [al-folio](https://github.com/alshedivat/al-folio) v1.

## Setting it up (one time)

1. **Back up the old site.** In your current `debmandal.github.io` repo, keep these files, because existing links point to them:
   - `papers/` (all paper PDFs, linked from the publication list as `https://debmandal.github.io/papers/...`)
   - `cv.pdf` and `statement.pdf` (stay at the top level of the repo)
   - `me-small.jpg` (moves to `assets/img/me-small.jpg`)
2. **Replace the repo contents** with this folder, keeping `.git`. Put the three items above back in place.
3. **Push to `main`.** The "Deploy site" GitHub Action builds the site and pushes it to a `gh-pages` branch.
4. **In GitHub → Settings → Pages**, set *Source* to "Deploy from a branch", branch `gh-pages`, folder `/ (root)`.
5. **In GitHub → Settings → Actions → General → Workflow permissions**, choose "Read and write permissions" so the deploy action can push.

The first build takes a few minutes. If it fails, open the Actions tab and the log says which file broke.

To preview locally (needs Docker): `docker compose pull && docker compose up`, then open <http://localhost:8080>.

## Before you go live — please fill in

- [ ] `_pages/service.md`: paste your list from the old `service.html`.
- [ ] `_pages/teaching.md`: your modules.
- [ ] `_pages/about.md`: uncomment `prospective:` if you are taking students; optionally add `teaching:` / `service:` highlights for the home page.
- [ ] `_news/`: the dates are month-level estimates; correct them.
- [ ] `_data/group.yml`: add Jiaying’s topic (`note:`) and any alumni, interns or visitors.
- [ ] `_data/coauthors.yml`: Andi Nika’s homepage appeared with two spellings on the old site; check which is right.
- [ ] `_data/socials.yml`: add ORCID / DBLP if you want those icons.

## Everyday edits

| To change… | Edit |
| --- | --- |
| Bio, pitch line, buttons, address | `_pages/about.md` |
| Research themes on the home page | `_data/research.yml` |
| Papers | `_bibliography/papers.bib` (field guide at the top of the file) |
| Which papers are on the home page | add `selected = {true}` to an entry |
| Venue-box colours (conference / journal / preprint) | `_data/venues.yml`; a new journal abbreviation needs a line there |
| Preprints section | any `@misc` entry in `papers.bib` is listed under Preprints, above the years |
| News | add a file to `_news/` (copy an existing one) |
| Statements, slides and other writing | `_data/writings.yml` (put the PDF in the repo, e.g. `slides/`, and add an item) |
| Group members | `_data/group.yml` |
| Co-author links in author lists | `_data/coauthors.yml` |
| Colours and fonts | `assets/_sass/_custom.scss` (tokens at the top) |

Topic filters on the Publications page match the `topics` field in `papers.bib`. If you add a new topic, add it to `topic_filters` in `_pages/publications.md` too.

## What is custom here (vs. stock al-folio)

- `_layouts/home.liquid`, `_includes/dm_group_list.liquid`: the home page and group list (new files, not overrides).
- `_includes/hook/bib.liquid`: an official al-folio hook that prints each paper’s topics.
- `assets/_sass/_custom.scss`: the site’s look, loaded by one added line at the end of `assets/css/main.scss`. It lives in `assets/_sass/` (set as a Sass load path in `_config.yml`) so that editing it re-versions `main.css` and browsers fetch the new styles.
- `assets/css/main.scss` is the only file that shadows a theme file. After updating al-folio gems, run
  `bundle exec al-folio upgrade overrides audit` to see if it needs refreshing.
- `_pages/old-urls/`: forward `pubs.html`, `group.html` and `service.html` to the new pages.
