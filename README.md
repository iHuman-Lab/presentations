# 🎤 iHuman Lab Presentations

Every talk, poster and tutorial from the iHuman Lab, all in one place and all in the same look: dark background, orange accent, Rubik font. Give a talk? Add it here and it gets its own card on the [presentations site](https://ihuman-lab.github.io/presentations/).

Adding yours takes about 10 minutes. Slides are plain text (Quarto + reveal.js), so there's no PowerPoint to fight with.

---

## 🚀 Add your presentation in 7 steps

### 0. Get the tools (once)

- [Git](https://git-scm.com/) and a [GitHub](https://github.com/) account
- [Quarto](https://quarto.org/docs/get-started/). Check it works with `quarto --version`.

### 1. Fork and clone

Click **Fork** at the top right of this repo (lab members with write access can make a branch instead). Then:

```bash
git clone https://github.com/<your-username>/presentations.git
cd presentations
git checkout -b add-<your-name>-<talk>     # e.g. add-jane-doe-smc2026
```

### 2. Make your folder

Everyone's talks live under `people/`. Use `First_Last` with an underscore, the same as your folder on the [lab website](https://github.com/iHuman-Lab/lab-website). There's no role folder, so nothing moves when you graduate:

```bash
mkdir -p people/Jane_Doe
```

### 3. Copy the starter deck

```bash
cp _template/deck.qmd people/Jane_Doe/smc2026.qmd
```

Rename it for your talk. You only copy this one file. The theme, logo and background are shared, so there's nothing else to copy.

### 4. Fill in the front matter

Open your `.qmd`. The block at the top (between the `---` lines) is the info for your card on the home page:

| Field | What to put |
|---|---|
| `title` | Talk title. Wrap a phrase in `[...]{.accent}` to make it orange. |
| `subtitle` | Where or why you're presenting |
| `author` | Your name |
| `date` | A fixed date like `"2026-01-31"`. **Don't use `today`**, or the cards sort wrong. |
| `description` | One or two sentences about the talk |
| `image` | The picture on your card. Put it in your folder and use its filename. |
| `event_type` | `Conference Talk`, `Poster`, `Defense`, `Tutorial`, `Lab Meeting`... |

Keep the `metadata-files:` line and the `theme:` and `logo:` lines under `format:`. They give your deck the lab theme and logo. Check the `../` counts match how deep your deck is.

### 5. Write your slides and preview

```bash
quarto preview people/Jane_Doe/smc2026.qmd
```

The deck reloads in your browser every time you save. Each `##` heading is a new slide, and a line with only `---` starts an untitled one. The starter deck has an example of every building block (cards, stats, flow diagrams, quotes, dividers...). Copy a slide, then change the text. The full list is in [Slide building blocks](#-slide-building-blocks).

Handy keys in the browser: `f` fullscreen, `s` speaker notes, `o` slide overview.

### 6. Open a pull request

```bash
git add people/Jane_Doe
git commit -m "Add Jane Doe SMC 2026 talk"
git push -u origin add-jane-doe-smc2026
```

Open the PR on GitHub and tick the checklist. A check runs `quarto render` on the whole site. **A green check means your deck builds.** A red one means click *Details* to see the error.

### 7. Celebrate 🎉

Once a maintainer merges your PR into `main`, the site rebuilds on its own and your card shows up on the home page.

### Naming rules

- **Your folder:** `First_Last`, spelled like your folder on the lab website. Plain letters only, with an underscore and no spaces or accents: `Elahe_Oveisi`, not `Elahe Oveisi` or `ElaheOveisi`.
- **Deck files and talk folders:** lowercase with hyphens, starting with the venue or topic and the year: `smc2026.qmd`, `defense-2026.qmd`. Skip `final`, `v2` and `new`.
- **Lab decks:** the same lowercase-hyphen style, like `shasta-tutorial`.

The PR check fails if a folder directly under `people/` isn't `First_Last`.

---

## 📁 Where things go

```
presentations/
├── people/<First_Last>/<talk>.qmd          # a person's own talks (one folder per person)
├── people/<First_Last>/<talk>/<talk>.qmd   # same, when a talk has lots of its own files
├── lab/<name>/<name>.qmd                   # lab-authored tutorials and outreach (e.g. shasta-tutorial/)
├── _template/deck.qmd                      # the starter deck you copy
├── _assets/                                # the shared lab theme (don't edit)
│   ├── theme.scss
│   └── revealjs-defaults.yml
└── assets/                                 # shared logo, background, banner
```

**Your images and videos go in your own folder.** Use a relative path from your `.qmd`, for example `![](figure1.png)`.

**The logo and campus background are shared.** Use `../../assets/logo.png` and `../../assets/background.jpg` when you want them. Decks two folders deep (`people/Jane_Doe/` or `lab/<name>/`) use `../../assets/...`. A deck in its own talk folder (`people/Jane_Doe/smc2026/`) is one deeper, so use `../../../assets/...`.

---

## 🧱 Slide building blocks

All of these are demonstrated in [`_template/deck.qmd`](_template/deck.qmd).

| What you want | How to write it |
|---|---|
| Orange highlight | `[text]{.accent}` |
| Bold opening line | `::: {.hook}` ... `:::` |
| Bold orange closing line | `::: {.punchline}` ... `:::` |
| Two columns | `::: {.columns}` with two `::: {.column width="50%"}` inside |
| Card grid | `::: {.cards}` with `::: {.card}` inside, and `[Title]{.card-title}` |
| Big-number stats | `::: {.stats}` with `::: {.stat}`, `[10+]{.stat-number}` and `[label]{.stat-label}` |
| Step-by-step flow | `::: {.flow-diagram}` with `::: {.flow-step}` and `::: {.flow-arrow}` |
| Section divider | `::: {.divider}` with `[Title]{.divider-title}` |
| Photo tiles | `::: {.impact-grid}` with `::: {.impact-card}` |
| Pull quote | `::: {.quote}` with `[— Name]{.quote-attribution}` |
| Small tag | `[text]{.badge}` |
| Gray, de-emphasized version | add `.secondary`, e.g. `::: {.card .secondary}` |
| Full-slide background image | `## {background-image="pic.jpg" background-opacity="0.4"}` |
| Tables and code | Plain markdown tables and code fences are themed for you |

---

## ✅ Do's and don'ts

- ✅ Use a fixed `date`, not `today`.
- ✅ Keep media small. Compress video and aim for under 25 MB per deck.
- ✅ Embed videos with a `<video src="...">` tag? List the file under `resources:` in your front matter, or Quarto won't copy it.
- ❌ Don't commit build output (`*.html`, `*_files/`). `.gitignore` already skips it.
- ❌ Don't edit `_assets/` or other people's folders. Need a theme change? Ask a maintainer.
- ❌ PDF or image-only posters aren't shown yet. Make a `.qmd` page that embeds the image or PDF.

---

## 🛟 Stuck?

| Problem | Try this |
|---|---|
| `quarto: command not found` | Install [Quarto](https://quarto.org/docs/get-started/) and restart your terminal |
| Your card isn't on the home page | Is your deck in `people/<First_Last>/`? Does it have `title`, `description` and `image`? |
| Card order looks wrong | Use a fixed date like `"2026-01-31"` |
| Image or logo missing | Check the relative path. From `people/Jane_Doe/`, the shared logo is `../../assets/logo.png`. |
| The PR check is red | Open *Details* on the check and read the Quarto error. It usually names the file and line. |
| Anything else | Ask in the lab channel or tag a maintainer on your PR |

---

## 🌐 How the website works

This repo is a [Quarto](https://quarto.org/) website. Any `.qmd` in the layout above becomes a card on the home page, filled from its front matter. Pushing to `main` builds the site and publishes it to GitHub Pages (the `gh-pages` branch) through `.github/workflows/publish.yml`.

To preview or build the whole site yourself:

```bash
quarto preview     # live-reload the whole site
quarto render      # build to _site/
```

Lab decks today: Discovery Day, MOSAIC tutorial, SHaSTA tutorial, physio workshop and IEEE SMC. Yours is next. 😎
