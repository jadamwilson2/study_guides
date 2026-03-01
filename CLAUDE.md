# CLAUDE.md — Study Guides Repository

## Project Overview

A static HTML/CSS website hosted on GitHub Pages that serves as a personal study guide library for three kids: **Julian**, **MJ**, and **Zach**. There is no build step, no framework, and no package manager — everything is plain HTML and inline CSS.

Live site: `https://jadamwilson2.github.io/study_guides/`

---

## Repository Structure

```
study_guides/
├── index.html            # Root landing page — links to each kid's section
├── julian/
│   └── index.html        # Julian's guide list (currently empty — no guides yet)
├── mj/
│   └── index.html        # MJ's guide list (currently empty — no guides yet)
└── zach/
    ├── index.html                              # Zach's guide list
    ├── Africa_Study_Guide.html                 # East & West Africa (9th Grade Honors)
    └── ancient_latin_america_study_guide.html  # Ancient Latin America civilizations
```

---

## Two Page Templates

### 1. Index / Navigation Pages (`index.html` files)

Used for the root landing page and each kid's guide-list page. Characteristics:
- Light background (`#f5f7fa`)
- System font stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`)
- Card-based or list-based layout
- Back-link (`← All Kids`) at the top of kid-level pages
- Guide links rendered as styled `<a>` blocks with an emoji icon and text

When a new study guide is added for a kid, **always update that kid's `index.html`** to add a link entry:

```html
<ul class="guide-list">
  <li>
    <a href="new_guide.html">
      <span class="icon">📖</span>
      Guide Title Here
    </a>
  </li>
</ul>
```

If the kid's index currently shows `<p class="empty">No study guides yet.</p>`, replace that element with a `<ul class="guide-list">` block.

### 2. Study Guide Pages

Rich, self-contained single-page HTML documents. Each has:

| Element | Description |
|---|---|
| `<head>` | Inline `<style>` block with CSS variables, no external stylesheets except optional Google Fonts |
| Hero section | Dark gradient background, large title, subtitle |
| Sticky navigation | Tab/pill-style links that jump to in-page `id` anchors |
| Content sections | Color-coded with section headers using emoji icons |
| Inline CSS only | No external CSS files are referenced (Google Fonts CDN is acceptable) |
| No JavaScript dependencies | Any JS should be minimal and inline |

#### Existing color themes (for reference)

**Africa Study Guide** — academic/regal:
```css
--gold: #C9A227; --dark: #1a1a2e; --mid: #16213e;
--accent: #0f3460; --green: #2d6a4f;
```
Fonts: Georgia serif (no Google Fonts import)

**Latin America Study Guide** — ancient/earthy:
```css
--gold: #C8963E; --deep-red: #7A1E1E; --terracotta: #C4572A;
--stone: #2A2420; --parchment: #F5EDD8; --jade: #2D6B4F;
```
Fonts: Cinzel + Crimson Pro via Google Fonts CDN

Choose or create a color theme that fits the subject matter. Reusing an existing theme is fine; creating a new one for new subjects is encouraged.

---

## Conventions

### File Naming
- Kid folders: lowercase first name (`julian/`, `mj/`, `zach/`)
- Study guide HTML files: descriptive, subject-based names. Either `Title_Case_With_Underscores.html` or `lowercase_with_underscores.html` — both exist in the repo, either is acceptable.

### Adding a New Kid
1. Create a folder `<name>/`
2. Add `<name>/index.html` using the same template as `julian/index.html` or `mj/index.html` (swap the kid's name)
3. Add a new card in the root `index.html` inside `.kids`:
```html
<a class="kid-card" href="<name>/index.html">
  <div class="avatar">📚</div>
  <h2><Name></h2>
</a>
```

### Adding a New Study Guide
1. Each kid has a subfolder called syllabi. Within this folder are a list of markdown documents. In each markdown document, there is a summary of the unit, with bullet points for important terms and example questions.
2. For each document, there should be a corresponding html file generated one directory up from the syllabi folder. For example, for the file `zach/syllabi/unit_7.md`, Claude should generate a file `zach/unit_7.html`. 
3. When claude generates this html file, it should create a title based on one of the headers near the top of the markdown file.
4. If the html file already exists, claude does not need to regenerate it. Only generate study guides for syllabus files that do not have a corresponding html file.
5. After an html file is generated, update the index.html file for that kid.
6. No changes to the root `index.html` are needed

### Navigation / Linking
- Root → Kid: `<kid>/index.html`
- Kid index → Study guide: relative filename (e.g., `Africa_Study_Guide.html`)
- Study guide back-link: not required but can point to `../` (the kid's index)
- All links are **relative** — no absolute URLs

---

## Development Workflow

### No Build Step
Open any HTML file directly in a browser. There is no compilation, bundling, or server required (though a local dev server like `python3 -m http.server` in the repo root avoids CORS issues with some browsers).

### Deployment
Pushing to `master` automatically deploys to GitHub Pages. Work on feature branches and merge to `master` when ready.

### Making Changes
- Edit HTML/CSS directly in the files
- Keep all CSS inline within `<style>` tags in the file being edited
- Do not introduce external CSS files or JS frameworks
- Keep each study guide fully self-contained — it must work as a standalone file

---

## Study Guide Content Guidelines

Study guides are school-level reference documents. When generating or editing content:

- **Audience**: middle/high school students
- **Structure**: use clear sections (Geography, History, Key People, Vocabulary, Practice Questions, etc.)
- **Visual hierarchy**: use emoji icons in section headers, color-coded callout boxes, and clear typographic scale
- **Accuracy**: content should be factually accurate and grade-appropriate
- **Completeness**: include vocabulary terms, key dates, important figures, and review questions
- **Prompt**: An example prompt to generate the study guide is:
I am in 9th grade honors world history. I have a test on SOME SUBJECT. The bullet points for this test are X, Y, and Z. Please make a study guide, with example test questions at the end. Let me know if there are any videos available that can help summarize this as well. The study guide should have an overview of concepts, flashcards, a 20 question practice quiz, and a rapid review sheet. Finally, we will also be tested on maps, please create some maps of these civilizations.

---

## Current State (as of March 2026)

| Kid | Guides |
|---|---|
| Julian | None yet |
| MJ | None yet |
| Zach | Africa Study Guide, Ancient Latin America Study Guide |
