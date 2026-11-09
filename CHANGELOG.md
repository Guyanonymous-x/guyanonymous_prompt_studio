# Guyanonymous' Prompt Studio: Changelog

From v1 to v3.3 (earlier versions were called Offline Wildcard Prompt Studio). Newest changes are at the bottom of each section's list; versions run oldest to newest.

---

## v1: the rewrite

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

---

## v2.0: version 2 and sizing

**Changed**
- Larger, scrollable sample panel. The Prompt Template editor and the Sample panel share the centre column's height equally, and both scroll when prompts get long.
- Removed the 1,000-file display limit in the left wildcard list.
- Labelled the app **version 2** in the title and header badge.

**Fixed**
- Wildcards not appearing after loading a saved prompt. The cause was that the linked folder was the output folder rather than the wildcard folder; the guidance and checks now make that clearer.
- A mistaken rebuild that dropped the right-hand information panels was thrown away. Version 2 was rebuilt from the file where the features worked, changing only the sizing of the centre panels.

---

## v2.1: sample breakout

**Added**
- Wildcards nested inside wildcards can open up in the Sample panel, showing the parent tag and every wildcard inside it (for example `__body__` opening into `__head__`, `__torso__` and `__limbs__`).
- Each opened part shows its tag name and the text it supplied.
- A small arrow on every part opens or closes it, and the state stays until you change it.
- **Expand all**, **Collapse all** and a **Levels** control.
- **Colour by parent**: parts called by the same wildcard share a colour (switchable back to colour by depth).

---

## v2.2: peek in the template editor

**Added**
- Click inside a green tag in the template editor and a **▸** button appears at the right edge of that line.
- It opens a panel with the file's lines, a filter box, and a marker for the line used in the current sample.
- **Replace** swaps that one tag for the line you choose, and Undo restores it.
- Works for nested wildcards too: replace `__body__` with a snippet that still contains tags, then keep drilling in.

**Changed**
- The button sits in a gutter at the edge of the editor so it never covers text.
- Autocomplete no longer pops up when you click inside a finished tag.

---

## v2.3: adjustable layout

**Added**
- Drag the edge of the left panel to resize the wildcard list, which also resizes the middle column. Double-click the edge to reset.
- **Wrap long names** option so long file names show in full instead of being cut off, plus tooltips on rows.
- Drag handles between the three centre sections (Prompt template, Sample, Exactly what gets saved) to adjust their heights.
- Sizes are remembered between sessions, can be nudged with the keyboard, and are kept within limits so nothing disappears.

---

## v2.4: reusable picks, locks and weights

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

---

## v2.5: models, exports, library and projects

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

---

## v3: renamed, collapsible panels

**Changed**
- The app is now **Guyanonymous' Prompt Studio**, in the page title, header, and exported JSON.
- File renamed to `guyanonymous_prompt_studio_v3.html`.

**Added**
- Every card in the right-hand column collapses to its title bar when you click the title (or press Enter on it), so unused tools stay out of the way.
- **Collapse all** and **Expand all** buttons at the top of the column.
- Collapsed or open states are remembered between sessions.

---

## v3.1: MOSS-Image limit

**Changed**
- MOSS-Image profile now treats about 4,000 tokens as its cutoff, with 3,000 recommended (previously 1,500 recommended).

## v3.2: large folders

**Changed**
- Wildcard list shows 1,000 files at a time with "show 1,000 more"; filter is debounced. 90,000 files now load in roughly 0.15 s instead of about 4.6 s.
- Auto-rescan on focus compares file names only for folders over 5,000 files.

## v3.3: folder view, faster search, presets

**Added**
- Folder view for the wildcard list, with file counts, Collapse all, Expand all and a Folders on/off switch.
- Model presets card: save, overwrite, delete, auto-load per model, export and import.

**Changed**
- Library search reads files in parallel, shows progress, stops at 500 matches, and does not keep files in memory for libraries over 20,000 files. Health check reads in parallel.

---

## Known limits

- Token counts are estimates until calibrated, because exact tokenizers need large vocabulary files that an offline page does not include.
- Several model limits are starting points from research and community reports, marked estimate or unverified. Test them in your own setup.
- History, versions, favourites, projects and tabs live in the browser's own storage. Export projects you care about, since clearing site data erases the rest.
