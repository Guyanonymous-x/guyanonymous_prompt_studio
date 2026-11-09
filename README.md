# Guyanonymous' Prompt Studio

A single-file, fully offline prompt builder for wildcard text files.

**[Launch the app online](https://guyanonymous-x.github.io/guyanonymous_prompt_studio/)** (runs in your browser; nothing is uploaded)

Current version: **v3.3**

**Contents:** [Introduction](#introduction) · [What's New in v3.3](#whats-new-in-v33) · [Features](#features) · [Getting Started](#getting-started) · [Using the Features](#using-the-features) · [Full Changelog](#full-changelog) · [License](#license)

## Introduction

Guyanonymous' Prompt Studio is one HTML file, `guyanonymous_prompt_studio.html`, for building image-generation prompts out of wildcard text files. Open it in Microsoft Edge or Google Chrome, point it at your folder of `.txt` wildcards, and design prompts with a live nested preview. No install, no server, no account.

It is for people who keep wildcard folders for tools such as ComfyUI or Forge / A1111. Wildcard folders get huge and nested, and it's hard to know what a template will actually produce, which wildcard picked what, or whether a prompt has blown past your model's token limit. The Studio shows all of it as you type, then saves single samples or exports batches, sweeps and every combination.

**Privacy.** The page blocks every network request (a content-security rule in the file), so nothing can be uploaded. It can only read and write folders you choose.

## What's New in v3.3

Changes since v3.2:

- **Folder view.** The wildcard list now groups files by folder, with a file count on each folder. Click a folder to open or close it; **Collapse all** and **Expand all** sit under the filter box. Typing in the filter opens every folder that has a match. **Folders: on/off** switches back to the flat list, and the choice is remembered.
- **Faster Library search.** It reads files several at a time, shows live progress, and stops once it has 500 matches instead of reading the whole library first. In a folder over 20,000 files it reads, searches and discards each file, so memory stays flat. A new search cancels the one still running. Health check also reads files in parallel.
- **Model presets.** A new card saves the model, frontend, prefix, suffix, negative prompt and the weight, single-paragraph and tidy options under a name. Tick "Apply automatically when I pick this preset's model" and choosing that model in "Model and length" loads the preset. Presets can be exported to a JSON file and imported on another machine.
- The page title, header badge and JSON export name now read v3.3.

For reference, the previous release, **v3.2**, kept very large folders fast (see the [Full Changelog](#full-changelog)).

## Features

- **Offline and private:** a single HTML file. Every network request is blocked; it reads and writes only folders you choose.
- **Folder scan:** every `.txt` in a folder (and, optionally, its subfolders) becomes a wildcard. No file-list limit, a filter box, wrap-long-names option and a resizable panel. Demo files are built in.
- **Wildcard file viewer and editor:** view, edit and save a file, create a new wildcard file, remove duplicate lines, see where a file is used.
- **Template editor:** `__file__` tags with autocomplete, drag-and-drop or double-click to insert, green/red highlighting for found/missing files, and a **▸** peek button that shows a file's lines and replaces the tag with one of them.
- **Live sample:** every wildcard (including wildcards nested inside wildcards) resolved with a seeded random generator, so a seed always reproduces the same sample. Nested parts open up to show which sub-wildcard supplied what, with Expand all, Collapse all, Levels and colour by parent.
- **Per-part control:** click a part to re-roll it; right-click to lock it, choose an exact line, or copy its text. **Unlock all** releases everything.
- **Reusable picks:** `${name=__a__ __b__}`, `${name}` and `__file$name__`, with a **Remember…** button and a remembered-values strip.
- **Syntax extras:** inline choices `{a|b|c}`, pick-several `{2-3$$, $$a|b|c}`, weighted lines `3:: text`, and `#` comment lines.
- **Model profiles:** 18 starter profiles with an estimated token gauge (recommended length and hard cutoff), a Frontend setting, calibration, editable/importable profiles, recommended options and a length check over 200 rolls.
- **Prefix, suffix and negative prompt:** added to every copy, save and export, and able to contain wildcards; optional removal of `(word:1.2)` weights.
- **Saving and exports:** save templates and single samples (one paragraph); batch of up to 1,000 random prompts as TXT, CSV or JSON with split files and a matching `_negative` file; sweep one wildcard; all possible prompts.
- **History and favourites:** the last 60 samples plus **★ Keep** favourites, restorable with template, seed, locks and chosen lines.
- **Library:** search every line of every file, health check, and where-used.
- **Tabs, versions and projects:** several templates at once, autosaved and named versions with compare and restore, and named projects you can export and import.
- **Layout:** resizable panels and centre sections, and collapsible right-hand cards, all remembered between sessions.
- **Separate remembered folders** for wildcards, templates, single samples, batch exports and all-prompts exports.

## Getting Started

### Requirements

- A desktop web browser. Use **Microsoft Edge or Google Chrome** (on Windows) for the full feature set: remembered folders and saving straight into folders.
- Other browsers still load wildcard folders, but cannot remember folders, and saves go to Downloads. The app shows a banner when that applies.
- No install, server, account or internet connection.

### Download and open

Prefer not to download? Use the live version: [https://guyanonymous-x.github.io/guyanonymous_prompt_studio/](https://guyanonymous-x.github.io/guyanonymous_prompt_studio/)

1. Download `guyanonymous_prompt_studio.html` from this repository (it is always the latest version), or clone the repository.
2. Open the file in Edge or Chrome (double-click it or drag it into a browser window).

### First steps

1. Click **Choose folder…** (top of the left panel) and pick the folder that holds your `.txt` wildcard files. Each file holds one option per line. Subfolders are included (switch this with **Include subfolders when scanning** in Output options). No folder yet? Click **Load demo files instead** to try it with built-in demo files (kept in memory only).
2. In the big editor, type a prompt, for example: `A photo of __hair__ __person__ in __place__, __lighting__`. Type `__` to get suggestions. Green means the file was found, red means it wasn't. You can also drag a file from the left list into the editor, or double-click it (or press its **+** button) to insert its tag.
3. Watch the **Sample** panel. Press **Roll new sample** (Ctrl+Enter) for another.
4. **Save template** (Ctrl+S) keeps your template as a `.txt`. **Save sample .txt** saves the filled-in prompt as one paragraph.
5. Optionally open **Folders** in the header to choose where templates, samples and exports are saved. Without output folders, saves go to Downloads.
6. Use the right-hand cards for batches and other exports. Click a card's title to collapse it to its title bar, or use **Collapse all** and **Expand all** at the top of the column.

The [user guide](docs/GUIDE.md) covers the same ground in more detail.

## Using the Features

### Wildcard folder and file list

- **Choose folder…** links the wildcard folder; **Rescan** re-reads it. If the browser needs you to re-allow access after reopening, a **Reconnect** link appears next to the wildcard-folder status.
- **Filter files…** narrows the list. **Wrap long names** shows long file names in full (rows also have tooltips).
- Drag a file name into the editor, double-click it, or press its **+** button to insert its tag at the cursor.
- **+ New wildcard file** asks for a name and creates the file in the linked folder.
- **Rescan the wildcard folder when I return to this window** (Output options) picks up files you edited in another program. It never interrupts an unsaved edit in the file viewer.

### Wildcard file viewer and editor

Click a file in the list to open it in the viewer below the list. One option per line; blank lines are ignored.

- **Insert tag** inserts its tag into the template.
- **Remove duplicates** removes repeated lines (then press **Save file**).
- **Where used** shows which wildcard files and templates use this one.
- **Save file** writes your edits; **✕** closes the viewer.

### Template syntax

| You type | What happens |
|---|---|
| `__file__` | A random line from `file.txt`. Subfolders: `__people/hair__`. A bare `__name__` also works if that name is unique. |
| `{a\|b\|c}` | A random choice inline (turn on **Inline choices**). Can nest. |
| `{2-3$$, $$a\|b\|c}` | Picks 2 to 3 different options joined with `, ` (any separator between the `$$` pairs). |
| `{2$$, $$__props__}` | Picks 2 different lines from one wildcard file. |
| `3:: text` | A weight, in wildcard files and inside `{…}` (turn on **Weighted options**). Higher is picked more often; `0::` switches the line off. |
| `${name=__a__ __b__}` | Pick once, remember it as `name`. Prints nothing. Can sit anywhere in the template. |
| `${name}` | Print the remembered value. Every use is identical. |
| `__file$name__` | Pick from `file`, remember it as `name` and print it. A later `__file$name__` repeats the same pick. |
| `$$` | A literal dollar sign when the variable syntax is on. A lone `$` (as in `$5`) needs no escape. |
| `# comment` | Lines starting with `#` in a wildcard file are skipped (**Ignore lines starting with #**). |

Wildcard files can themselves contain `__other__` references, `{…}` choices and `${name}` uses. A saved template is itself a `.txt` file: put it in your wildcard folder and it becomes a wildcard, with each line treated as one option.

### Template editor

- Type `__` (or `${`) for autocomplete. Use **Arrow Up/Down** to move through suggestions, **Enter** or **Tab** to accept, **Esc** to close.
- **Peek and replace:** click inside a green tag and press the **▸** button at the right edge of that line. A panel shows the file's lines, a filter box, and a marker for the line used in the current sample. **Replace** swaps that one tag for the line you choose (Undo restores it). It works for nested wildcards too: replace `__body__` with a snippet that still contains tags, then keep drilling in. **Esc** closes the panel.
- **Remember…:** select text or tags, press **Remember…**, give it a name, and the app writes the `${name=…}` definition and leaves `${name}` in its place. The editor underlines each name in its own colour and marks undefined names red.
- **Clear** empties the editor. The name box next to "Prompt template" sets the file name used when saving; an **unsaved** badge shows pending changes.

#### Reusing one pick (names, text overlays)

Say `names.txt` holds character names and you want the same name in the prompt and in a sign:

```
${hero=__names__}A portrait of ${hero}, holding a sign that reads "${hero}".
```

### The Sample panel

- **Coloured parts** are filled-in wildcards. Click one to re-roll only that part.
- **Small arrow** on a part opens or closes it to show the wildcards inside it (for example `__body__` opens into `__head__`, `__torso__`, `__limbs__`). **Expand all**, **Collapse all** and **Levels** control this in bulk.
- **Colour by parent** (Output options): parts called by the same wildcard share a colour. Off = colour by depth. **Colour-code wildcard results** switches the colouring on or off.
- **Right-click** a part for: **Re-roll this part**, **Lock this part** (Roll new sample keeps it), **Choose a line…** (pick the exact line from a filterable list), **Go back to a random line**, and **Copy this text**. **Esc** closes the menu.
- **Remembered values strip** shows each `${name}` with buttons to re-roll, lock or choose its line.
- **Unlock all** releases every lock and chosen line.
- **Seed:** the same seed and template give the same sample. Editing text keeps the other choices stable.
- **★ Keep** stores the sample in Favourites; **Copy** copies it; **Save sample .txt** saves it.
- **Exactly what gets saved** is the final text after tidy, prefix, suffix and weight handling.
- **Update sample as I type** (Output options) keeps the sample live while you edit.

### Model and length

Pick your model under **Model and length**. A gauge under "Exactly what gets saved" shows an estimated token count with the model's recommended length and hard cutoff.

- There are 18 starter profiles across CLIP tag models, anime tag models, T5 natural-language models, LLM-encoder models, hosted models and video. Each is marked verified, estimate or unverified.
- **Frontend** (ComfyUI, Forge / A1111 / sd_webui, or Other or hosted) changes how long prompts are interpreted, including 75-token chunk counts for CLIP models. ComfyUI passes long prompts through while others chunk or truncate.
- Numbers are **estimates** until you calibrate: press **Calibrate…** and enter the token count your own tool reports for the shown sample.
- **Manage…** lets you edit any profile, **Save as new…**, copy or delete a profile or a whole family, **Import…** and **Export…** profiles, and **Revert all defaults** to the originals.
- **Apply recommended options** sets single paragraph, tidy spacing and weight handling to suit the model.
- **Check length over 200 rolls** shows the shortest, typical and longest prompts and how many exceed the limits.

### Prefix, suffix and negative prompt

Text added to every copy, saved sample, batch line and export. They may contain wildcards, but are chosen separately from the template, so `${name}` values don't carry into them. **Remove (word:1.2) weights** applies when the chosen model is marked "no weights".

### Output options

Checkboxes in the **Output options** card: **Single paragraph**, **Tidy spacing and commas**, **Inline choices**, **Remember and reuse `${name}`** (turn off if your prompts use a literal `${`), **Weighted options**, **Ignore lines starting with #**, **Include subfolders when scanning**, **Rescan the wildcard folder when I return to this window**, **Update sample as I type**, **Colour-code wildcard results**, **Colour by parent**, and **Windows line endings (CRLF) in saved files**.

### Saving and exports

- **Save template** (Ctrl+S), **Save as…** (Ctrl+Shift+S), **Open** (Ctrl+O) and **New** (opens a new tab).
- **Save sample .txt** saves the evaluated sample as a single paragraph.
- **Batch of random prompts (up to 1,000):** set **How many**, optionally **Skip duplicates**, **Reproducible** (derive each prompt's seed from the Seed box) and **Write each seed before its prompt** (`seed | prompt`). Choose the **File format**:
  - **Text**: one prompt per line. Optionally a matching `_negative` file with the same number of lines (when a negative prompt is set).
  - **CSV**: number, seed, prompt, negative, and the picks that made it.
  - **JSON**: the same, structured.

  **Split every N prompts** writes several numbered files (0 = one file). Press **Generate and save batch**; a length summary and a preview of the last batch appear afterwards. **Cancel** stops a running batch.
- **Sweep one wildcard:** choose a wildcard and **Repeat each** count, then **Export sweep**. It writes one prompt for every line of that wildcard while everything else is random, using the batch file format and split settings.
- **All possible prompts:** available when the template uses exactly one wildcard (or when you tick **Allow several wildcards**, which can be enormous). Optionally **Remove duplicate lines** and set **Maximum lines**; a combination counter shows the total. A reused `${name}` counts once. Press **Export all prompts**.
- **Checks** card: lists problems such as missing files and undefined, unused or twice-defined variables, plus a **Resolution trace**.

If no output folder is set, saves go to the browser's Downloads (a save dialog appears when the browser supports it).

### History, Library, Tabs, Versions and Projects

- **History** (header) keeps the last 60 samples. **★ Keep** stores favourites with their template. **Restore** brings back template, seed, locks and chosen lines. The list can be saved as `.txt` or cleared.
- **Library** (header): *Search lines* across every file; *Health check* finds empty files, missing references, loops, duplicate and near-duplicate lines, unbalanced braces, very long lines and unused files; *Where used* shows which files and templates use a wildcard.
- **Tabs** hold several templates at once, each with its own prefix, suffix, negative prompt and model. Press **+** in the tab strip for a new tab. Closing a tab keeps a version. Tabs and the draft are restored when you reopen the app.
- **Versions…** lists autosaved and named versions (**Save a named version now**), compares them with the current text and restores them. **Label / pin…** and **Delete** manage them. They live inside this browser.
- **Projects** (header) save the open tabs (with prefix, suffix, negative and model) and your output settings under a name. **Open**, **Update**, **Export…**, delete, and **Import file…**. Wildcard and output folders are not part of a project.

### Folders

**Folders** in the header sets separate remembered folders for wildcards, templates, single samples, batch exports and all-prompts exports, or **Use one folder for all outputs…**. Windows may ask you to re-allow access after you reopen the app. Browsers refuse a few top-level system folders (Documents, Downloads, Desktop); pick a subfolder inside them.

### Layout

- Drag the edge of the left panel to resize the file list (and the middle column). Drag the handles between Prompt template, Sample and Exactly what gets saved to adjust their heights.
- Double-click a handle to reset it. Focus a handle with Tab and use the **arrow keys** to nudge it.
- Click a right-hand card's title (or press **Enter** or **Space** on it) to collapse or open it. **Collapse all** and **Expand all** sit at the top of the column.
- Sizes and collapsed states are remembered between sessions.

### Keyboard shortcuts

| Keys | Action |
|---|---|
| Ctrl+S | Save template |
| Ctrl+Shift+S | Save as |
| Ctrl+Enter | Roll a new sample |
| Ctrl+O | Open template |
| Esc | Close autocomplete, the peek panel, the right-click menu or line picker, or a name prompt |
| Arrow Up/Down, Enter or Tab | Move through and accept autocomplete suggestions |
| Arrow keys (on a focused resize handle) | Nudge the panel size |
| Enter or Space (on a card title) | Collapse or open the card |

The **?** button in the header opens the in-app "Syntax and shortcuts" help.

### Troubleshooting

- **All tags are red.** The linked folder has no matching files. Check that you linked the folder holding your wildcards, not your batch output folder.
- **Typed `${` and nothing happens.** Turn **Remember and reuse** on in Output options. Turn it off if your prompts need a literal `${`.
- **Weights look ignored.** Tick **Weighted options**, and put the weight first: `3:: a red coat`.
- **A tab or sample came back different.** Wildcard files or output settings changed since it was saved.
- **Saved to Downloads, not my folder.** Set the folder under **Folders**; use Edge or Chrome.
- **The token gauge disagrees with my tool.** Press **Calibrate…**.

### Good to know

- Token counts are estimates until calibrated, because exact tokenizers need large vocabulary files that an offline page does not include.
- Model limits are starting points from research and community reports, several marked estimate or unverified. Test yours and edit the profile.
- History, versions, favourites, projects and tabs live in the browser's own storage. Export projects you care about, since clearing site data erases the rest.

### Documents and repository layout

- [User guide](docs/GUIDE.md), [Changelog](CHANGELOG.md), [Share post](docs/SHARE_POST.md) (also as [copy-ready HTML](docs/SHARE_POST.html))
- `guyanonymous_prompt_studio.html`: the app (always the latest version)
- `docs/`: guide and share post
- Every release is its own commit whose message starts with the version (see `git log`).
- Large wildcard data archives (`*.zip`) are not stored in this repository.

### Releasing a new version

1. Edit `guyanonymous_prompt_studio.html`. Update the title, the header badge and the exported-JSON app name to the new version, and the version tag text in `index.html`.
2. Add the new section to `CHANGELOG.md` (and to the Full Changelog below), and update `docs/` if features changed.
3. Commit with a message beginning with the version, for example `v3.2: ...`.
4. Tag it: `git tag -a v3.2 -m "v3.2: ..."`.
5. Push the branch and tags: `git push origin main --tags`.
6. Keep the live-app link at the top of this README's introduction (`https://guyanonymous-x.github.io/guyanonymous_prompt_studio/`) and in `index.html`.

## Full Changelog

Newest first. Earlier versions were called Offline Wildcard Prompt Studio. Dates are the commit dates in this repository's git history. The same notes, oldest first, are in [CHANGELOG.md](CHANGELOG.md).

### v3.3: folder view, faster search, presets (2026-11-09)

**Added**
- Folder view for the wildcard list, with file counts, Collapse all, Expand all and a Folders on/off switch.
- Model presets card: save, overwrite, delete, auto-load per model, export and import.

**Changed**
- Library search reads files in parallel, shows progress, stops at 500 matches, and does not keep files in memory for libraries over 20,000 files. Health check reads in parallel.

### v3.2: large folders (2026-11-09)

**Changed**
- Wildcard list shows 1,000 files at a time with "show 1,000 more"; filter is debounced. 90,000 files now load in roughly 0.15 s instead of about 4.6 s.
- Auto-rescan on focus compares file names only for folders over 5,000 files.

### v3.1: MOSS-Image limit (2026-11-04)

**Changed**
- MOSS-Image profile now treats about 4,000 tokens as its cutoff, with 3,000 recommended (previously 1,500 recommended).

### v3: renamed, collapsible panels (2026-11-04)

**Changed**
- The app is now **Guyanonymous' Prompt Studio**, in the page title, header, and exported JSON.
- File renamed to `guyanonymous_prompt_studio_v3.html` (in this repository the app is kept as `guyanonymous_prompt_studio.html`).

**Added**
- Every card in the right-hand column collapses to its title bar when you click the title (or press Enter on it), so unused tools stay out of the way.
- **Collapse all** and **Expand all** buttons at the top of the column.
- Collapsed or open states are remembered between sessions.

### v2.5: models, exports, library and projects (2026-11-04)

**Added: model and length**
- Model profiles with an estimated token gauge under "Exactly what gets saved", showing the recommended length and hard cutoff.
- Eighteen starter profiles across CLIP tag models, anime tag models, T5 natural-language models, LLM-encoder models, hosted models and video. Each is marked verified, estimate or unverified.
- A Frontend setting (ComfyUI, Forge/A1111 or other) that changes how long prompts are interpreted, including 75-token chunk counts for CLIP models.
- **Manage…** window: edit any profile, save it under a new name, copy or delete a profile or a whole family, import and export profiles, and revert to the originals.
- **Calibrate…** to teach the counter from the token count your own tool reports.
- **Apply recommended options** and **Check length over 200 rolls**, which reports shortest, typical and longest prompts and how many pass the limits.

**Added: output shaping and exports**
- Prefix, suffix and negative prompt fields, added to every copy, save and export, and able to contain wildcards.
- Option to remove `(word:1.2)` weights for models that ignore them.
- Batch export formats: text, CSV or JSON, with each prompt's seed and the lines that were picked.
- Split every N prompts into numbered files, and an optional matching `_negative` text file.
- A length summary after each batch.
- **Sweep one wildcard:** one prompt per line of a chosen wildcard while everything else stays random, with an optional repeat count.

**Added: history and library**
- **History:** the last 60 samples, plus **★ Keep** favourites that store their template. Restore brings back the template, seed, locks and chosen lines.
- **Library:** search every line of every file, a health check (empty files, missing references, loops, duplicate and near-duplicate lines, unbalanced braces, very long lines, unused files), and where-used.
- **Remove duplicates** in the file viewer.
- Optional rescan of the wildcard folder when you return to the window, which never interrupts an unsaved edit.

**Added: tabs, versions and projects**
- Template tabs, each with its own prefix, suffix, negative prompt and model. New and Open now use tabs instead of discarding your work.
- **Versions…:** autosaved and named versions with a compare view and restore.
- **Projects:** save and reopen whole sets of tabs and output settings, and export or import them as files.
- Tabs and the draft are restored when you reopen the app.

**Changed**
- Save dialogs and downloads now choose the right file type for CSV and JSON.
- The all-possible export applies prefix, suffix and weight handling.
- Help window updated for every new feature.

**Documents**
- A user guide and a ready-to-post share text now ship with the app.

### v2.4: reusable picks, locks and weights (2026-11-04)

**Added**
- **Reusable picks.** `${name=__a__ __b__}` picks once and prints nothing. `${name}` prints the same value everywhere. `__file$name__` picks, remembers and prints in one go. Definitions can be anywhere in the template, and wildcard files can use `${name}` too. `$$` gives a literal dollar sign.
- **Remember…** button: select text or tags in the editor, name it, and the app writes the definition and the use for you.
- Editor colouring for variables, a red mark for undefined names, and autocomplete for `${`.
- **Remembered values strip** above the sample, with re-roll, lock and choose-a-line buttons for each value.
- **Right-click menu** on any part of the sample: re-roll, lock, choose a specific line from a filterable list, copy text. Locks and chosen lines survive **Roll new sample**, with **Unlock all** to release them.
- **Weighted lines:** `3:: text` in wildcard files and inside `{…}`, with `0::` switching a line off.
- **Pick several:** `{2-3$$, $$a|b|c}` and `{2$$, $$__file__}` choose different options and join them.
- New checks for undefined, unused and twice-defined variables.
- On/off checkboxes for the variable and weight syntax, so prompts with a literal `${` still work.
- Counts and the all-possible export treat a reused value as a single choice, and every enumerated prompt keeps that value consistent.

**Fixed**
- Pressing Enter in a name prompt no longer leaks a line break into the editor.

### v2.3: adjustable layout (2026-11-04)

**Added**
- Drag the edge of the left panel to resize the wildcard list, which also resizes the middle column. Double-click the edge to reset.
- **Wrap long names** option so long file names show in full instead of being cut off, plus tooltips on rows.
- Drag handles between the three centre sections (Prompt template, Sample, Exactly what gets saved) to adjust their heights.
- Sizes are remembered between sessions, can be nudged with the keyboard, and are kept within limits so nothing disappears.

### v2.2: peek in the template editor (2026-11-04)

**Added**
- Click inside a green tag in the template editor and a **▸** button appears at the right edge of that line.
- It opens a panel with the file's lines, a filter box, and a marker for the line used in the current sample.
- **Replace** swaps that one tag for the line you choose, and Undo restores it.
- Works for nested wildcards too: replace `__body__` with a snippet that still contains tags, then keep drilling in.

**Changed**
- The button sits in a gutter at the edge of the editor so it never covers text.
- Autocomplete no longer pops up when you click inside a finished tag.

### v2.1: sample breakout (2026-11-04)

**Added**
- Wildcards nested inside wildcards can open up in the Sample panel, showing the parent tag and every wildcard inside it (for example `__body__` opening into `__head__`, `__torso__` and `__limbs__`).
- Each opened part shows its tag name and the text it supplied.
- A small arrow on every part opens or closes it, and the state stays until you change it.
- **Expand all**, **Collapse all** and a **Levels** control.
- **Colour by parent**: parts called by the same wildcard share a colour (switchable back to colour by depth).

### v2.0: version 2 and sizing (2026-11-04)

**Changed**
- Larger, scrollable sample panel. The Prompt Template editor and the Sample panel share the centre column's height equally, and both scroll when prompts get long.
- Removed the 1,000-file display limit in the left wildcard list.
- Labelled the app **version 2** in the title and header badge.

**Fixed**
- Wildcards not appearing after loading a saved prompt. The cause was that the linked folder was the output folder rather than the wildcard folder; the guidance and checks now make that clearer.
- A mistaken rebuild that dropped the right-hand information panels was thrown away. Version 2 was rebuilt from the file where the features worked, changing only the sizing of the centre panels.

### v1: the rewrite (2026-11-04)

The first full rewrite of the original Gemini-generated prototype, keeping its look and headings but rebuilding how it works.

**Core**
- Single offline HTML file. A content-security rule blocks every network request, so nothing can be uploaded.
- Scans a folder of `.txt` wildcard files (with subfolders) and lists them.
- Template editor with `__filename__` tags, autocomplete when you type `__`, and green or red highlighting for found or missing files.
- Drag a file name into the prompt, or use the **+** button or double-click to insert its tag.
- Live sample with every nested wildcard resolved to a random line, using a seeded random generator so a seed always reproduces the same sample.
- Click a coloured part of the sample to re-roll just that part.
- Save and open templates as `.txt`. Save the evaluated sample as a single paragraph with no line breaks.
- Batch export of up to 1,000 random prompts, each with a new seed, with optional duplicate skipping and optional reproducible seeds.
- "All possible prompts" export when the template uses exactly one wildcard, with a combination counter, a line cap and optional duplicate removal.
- Separate remembered folders for wildcards, templates, samples, batches and all-prompts exports (saved in the browser, re-allowed on reopen).
- Right-hand panels: output options, batch card, all-possible card, checks and a resolution trace.
- Optional inline choices `{a|b|c}`, optional comment lines starting with `#`, tidy spacing and commas, Windows line endings option.
- In-app wildcard file viewer and editor with Save.
- Fallbacks for browsers without folder access (folder picker, Downloads).

## Live version

Once GitHub Pages is on, the app runs in the browser at https://guyanonymous-x.github.io/guyanonymous_prompt_studio/ (landing page in `index.html`, app in `guyanonymous_prompt_studio.html`). Nothing is uploaded; it works the same as the downloaded file.

## License

Free for non-commercial use, including making prompts and images you then use however you like. Selling the app, or including or integrating it in a commercial product, service or paid platform, needs prior written permission; ask through this GitHub repository. Free redistribution for non-commercial use is allowed; keep the notice and copyright line, and mark modified versions as modified. See [LICENSE](LICENSE) for the full terms.
