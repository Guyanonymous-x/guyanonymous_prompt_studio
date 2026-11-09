# Guyanonymous' Prompt Studio v3.3

**A single-file, fully offline prompt builder for wildcard files.**

I built this for my own ComfyUI / Forge Neo workflow and it grew into something worth sharing. It's one HTML file. Open it in Edge or Chrome on Windows, point it at your folder of `.txt` wildcard files, and design prompts with a live preview. No install, no server, no account, and it cannot upload anything (the page blocks every network request).

## Why

Wildcard folders get huge and nested, and it's hard to know what a template will actually produce, which wildcard picked what, or whether a prompt has blown past your model's token limit. This shows all of it as you type.

## What it does

- Scans a folder (and subfolders) of `.txt` wildcards, with no file limit, a filter, and resizable panels
- Template editor with `__file__` tags: autocomplete, drag-and-drop, green/red validity, and a peek button that shows a file's lines and swaps the tag for one you choose
- Live sample with every nested wildcard resolved. Open any part to see which sub-wildcard supplied what
- Click a part to re-roll just that part. Right-click to lock it, or pick an exact line from the file
- Reuse one pick everywhere: `${hero=__names__}` then `${hero}` (great for names and text overlays), or `__names$hero__`
- Optional weights (`3:: text`), inline choices `{a|b|c}`, and pick-several `{2-3$$, $$a|b|c}`
- Model profiles with a token gauge (recommended length vs. hard cutoff), calibration, editable limits, and a "check length over 200 rolls" report
- Prefix, suffix and negative prompt, and it strips `(word:1.2)` weights for models that ignore them
- Saves the sample as **one paragraph**. Batch export of up to 1,000 random prompts (new seed each) as TXT, CSV or JSON, with split files and a matching negative file
- Sweep export: every line of one wildcard while the rest stays random
- "All possible prompts" export for one wildcard (reused picks counted once)
- History, favourites, library search, health check (missing refs, loops, duplicates), where-used, tabs, autosaved versions and projects
- Folder view for the wildcard list, with file counts; stays fast with 90,000+ files
- Model presets: save model, prefix, suffix and negative prompt together and load them per model
- Collapsible tool cards, so the right-hand column shows only what you need
- Remembers separate folders for wildcards, templates, samples, batches and exports

## How to start

1. Open the `.html` file in Edge or Chrome
2. Click **Choose folder…** and pick your wildcard folder
3. Type a prompt and use `__` for suggestions
4. **Ctrl+Enter** for a new sample, **Ctrl+S** to save the template

The included guide covers everything in about five minutes.

## Version history

- **v3.3:** Folder view for the wildcard list (counts, collapse/expand all); faster Library search that stops at 500 matches and copes with 90,000+ files; model presets (model, prefix, suffix, negative and weight options saved by name, loaded automatically per model, exportable).
- **v3.2:** Very large folders (90,000+ files) stay fast: the list draws 1,000 rows at a time with a filter, and the focus auto-rescan no longer reads every file.
- **v3.1:** MOSS-Image profile updated to its 4,000-token limit.
- **v3:** Renamed Guyanonymous' Prompt Studio. Every right-hand card collapses to its title bar (with Collapse all / Expand all, remembered between sessions).
- **v2.5:** Model profiles with a token gauge; prefix, suffix and negative prompt; TXT/CSV/JSON batch export with split files and a matching negative file; sweep export; history and favourites; library search, health check and where-used; template tabs, autosaved versions and projects.
- **v2.4:** Reusable picks (`${name=__a__}`, `${name}`, `__file$name__`) with a Remember… button and a values strip; right-click to lock a part or choose an exact line; weighted lines; pick-several.
- **v2.3:** Drag-to-resize left panel and centre sections, wrap long file names, sizes remembered.
- **v2.2:** Peek button in the template editor: see a wildcard's lines and swap the tag for one of them.
- **v2.1:** Nested wildcards open up in the sample (`__body__` → `__head__`, `__torso__`, `__limbs__`) with Expand all, Collapse all, Levels and colour by parent.
- **v2.0:** Larger scrolling sample panel sharing height with the editor; no limit on the file list.
- **v1:** First full rewrite: offline folder scan, live nested sample, seeded re-rolls, save/open templates, one-paragraph sample save, batch export, all-possible export, separate remembered folders.

## Good to know

- Token counts are estimates until you calibrate them with your own tool's number, and model limits are editable starting points (some unverified), not guarantees
- History, versions and projects live in your browser's storage. Export projects you care about
- Use Edge or Chrome for remembered folders and saving straight into folders; other browsers fall back to Downloads

Free to use and share. Feedback, bug reports and feature ideas welcome.

#StableDiffusion #ComfyUI #Wildcards #PromptEngineering #Offline

---

**Short version (for a character limit):**

Guyanonymous' Prompt Studio v3.3: one HTML file, no install, nothing uploaded. Point it at your wildcard .txt folder and build prompts with a live nested preview, re-roll/lock/choose any part, reuse one pick across a prompt, model token gauge, batch/sweep/all-combinations export (TXT/CSV/JSON), history, library health check and projects. Works offline in Edge/Chrome. Guide included.
