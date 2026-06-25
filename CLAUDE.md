# ahotimski00.github.io — portfolio site

Personal portfolio site for Al Hotimski, geospatial data scientist at The Conservation Fund. Live at https://ahotimski00.github.io.

## Tech

Jekyll + Minimal Mistakes theme, served by GitHub Pages from the `main` branch. Source pages are markdown under `_pages/`; navigation is data-driven from `_data/navigation.yml`. Local builds via `bundle exec jekyll serve`.

## Repo structure

```
.
├── _config.yml           # Jekyll config (theme, plugins, defaults)
├── _data/
│   └── navigation.yml    # Top-nav order: About | Projects | Tools | Resume
├── _includes/            # Partial templates (head, footer)
├── _pages/
│   ├── about.md          # /about/  - bio, education, experience, skills
│   ├── projects.md       # /projects/ - three deep case studies (Land Ownership, ACEP, FHSZ)
│   ├── tools.md          # /tools/  - smaller open-source pieces (cogsieve so far)
│   └── resume.md         # /resume/ - resume content + PDF download (PDF currently TODO)
├── assets/
│   ├── img/              # All site images (project carousels, screenshots)
│   └── al_hotimski_resume.pdf  # TODO - not yet uploaded
├── index.md              # / - homepage (3 What-I-Do cards, 3 project teasers, skills table)
└── .gitignore            # Includes _site/ - never commit Jekyll build output
```

## Sister repos

- **resume-coach** (private): holds working resume artifacts and the career-goals strategy. When updating the public Resume page here, check that the base resume there is in sync.
- **cogsieve** (public, at github.com/ahotimski00/cogsieve): featured on the Tools page. Its live Streamlit demo at https://cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app/ is the headline interactive surface for the portfolio.

## Page conventions

- Project sections use anchor IDs (`{#land-ownership}`, `{#farm-parcel}`, `{#fire-hazard}`) so the TOC sidebar links work.
- Image carousels use the inline `<div class="carousel-wrapper">...` structure with the shared JS at the bottom of `projects.md` (lightbox + arrow navigation). Don't duplicate that script across pages.
- Tables prefer markdown over HTML for readability.
- Don't write multi-paragraph docstring-style sections. One section per concrete thing.
- The Resume page should never reproduce the full PDF content - it should be a compact summary with a "Download PDF" button.

## Outstanding TODOs in the source

Grep for `<!-- TODO` to find them. As of last edit:

- Upload the resume PDF and uncomment the download link in `_pages/resume.md`.
- Confirm/correct the tooling list on the Land Ownership project (rapidfuzz, shapely, etc.).
- The home page Skills row and About page once listed NLTK/NLP, but no project actually uses NLP. Replace with "fuzzy matching, record linkage, entity resolution" or add an actual NLP project. (Source-code TODO comment flags this in projects.md.)
- Add a deeper RF-model section to the FHSZ project: feature importance, hyperparameter tuning, class-weighted training rationale.
- When the ACEP source is approved for public release, add the GitHub link.

## Recent design decisions (newest first)

- **Tools page added** as a new top-nav tab between Projects and Resume. Hosts smaller open-source pieces (cogsieve and future). Keeps the Projects page as the long-form case-study surface and the Tools page as the runnable-code surface.
- **Em/en dashes are banned project-wide.** Use hyphens. There's a memory rule about this globally; respect it here too.
- **No AI-sounding language.** A skeptical-reviewer audit flagged "Passionate," triplet rhythm, "actionable insights," "not just X but Y," and the like. Cut on sight, rewrite specific to projects.
- **The 93% QA-reduction metric is scoped per-state-per-month** on the recurring monthly Regrid refresh that drives the parcel-change pipeline. Don't drop the scope.
- **ACEP project is internal-source.** The Projects page leads with a one-line note explaining why no GitHub link.
- **Engineering-practices block on Tools page** was rewritten as a longer "Approach" section that walks through decisions made while building cogsieve. Reads as thinking during the build, not a checklist of best practices.

## Voice

- First person where natural ("I built", "I designed"). Not third person, not passive ("was developed").
- Lead with the concrete thing, then the why.
- Numbers earn trust when they have units the reader can multiply (per-state, per-month, per-snapshot, per-parcel).
- If a sentence could appear on any portfolio in any sector, rewrite it to be specific to Al's actual work.

## Useful one-liners

```bash
# Local preview
bundle exec jekyll serve

# Find any em or en dashes that slipped in
grep -rn $'—\|–' _pages/ index.md _config.yml

# Find open source-code TODOs
grep -rn 'TODO' _pages/ index.md
```
