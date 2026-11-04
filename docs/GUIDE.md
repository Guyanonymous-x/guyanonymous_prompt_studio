# Guyanonymous' Prompt Studio v3.1: User Guide

A single HTML file for building image-generation prompts out of wildcard text files. It runs in your browser, works offline and never uploads anything.

## 1. What it does

- Scans a folder of `.txt` wildcard files (one option per line) and lists them.
- Lets you write a prompt template mixing normal text with `__filename__` references.
- Shows a live sample with every wildcard, including wildcards nested inside wildcards, filled with a random line.
- Saves templates and samples, and exports up to 1,000 random prompts, every combination of one wildcard, or a sweep through one wildcard.
- Estimates prompt length against the model you use and warns you before you pass its limit.

**Privacy.** The page blocks every network request. It can only read and write folders you choose.

**Browser.** Use Microsoft Edge or Google Chrome on Windows for the full feature set (remembered folders, saving straight into folders). Other browsers still load wildcard folders, but saves go to Downloads.

## 2. Quick start

1. Open `guyanonymous_prompt_studio.html` in Edge or Chrome.
2. Click **Choose folder…** and pick the folder that holds your `.txt` wildcard files. Subfolders are included.
3. In the big editor, type a prompt, for example: `A photo of __hair__ __person__ in __place__, __lighting__`. Type `__` to get suggestions. Green means the file was found, red means it wasn't.
4. Watch the **Sample** panel. Press **Roll new sample** (Ctrl+Enter) for another.
5. **Save template** (Ctrl+S) keeps your template as a `.txt`. **Save sample .txt** saves the filled-in prompt as one paragraph.
6. Use the right-hand cards for batches and other exports. Click a card's title to collapse it to its title bar, or use **Collapse all** and **Expand all** at the top of the column. The app remembers which are collapsed.

You can also drag a file from the left list into the editor, or double-click it to insert its tag.

## 3. Template syntax

| You type | What happens |
|---|---|
| `__file__` | A random line from `file.txt`. Subfolders: `__people/hair__`. |
| `{a\|b\|c}` | A random choice inline (turn on **Inline choices**). Can nest. |
| `{2-3$$, $$a\|b\|c}` | Picks 2 to 3 different options joined with `, ` (any separator between the `$$` pairs). |
| `{2$$, $$__props__}` | Picks 2 different lines from one wildcard file. |
| `3:: text` | A weight, in wildcard files and inside `{…}` (turn on **Weighted options**). `0::` switches the line off. |
| `${name=__a__ __b__}` | Pick once, remember it as `name`. Prints nothing. Can sit anywhere in the template. |
| `${name}` | Print the remembered value. Every use is identical. |
| `__file$name__` | Pick from `file`, remember it as `name` and print it. A later `__file$name__` repeats the same pick. |
| `$$` | A literal dollar sign when the variable syntax is on. |
| `# comment` | Lines starting with `#` in a wildcard file are skipped (optional). |

Wildcard files can themselves contain `__other__` references, `{…}` choices and `${name}` uses.

### Reusing one pick (names, text overlays)

Say `names.txt` holds character names and you want the same name in the prompt and in a sign:

```
${hero=__names__}A portrait of ${hero}, holding a sign that reads "${hero}".
```

Select any text or tags in the editor and press **Remember…** and the app writes the definition for you. The editor underlines each name in its own colour and marks undefined names red.

## 4. The Sample panel

- **Coloured parts** are filled-in wildcards. Click one to re-roll only that part.
- **Small arrow** on a part opens it to show the wildcards inside it (for example `__body__` opens into `__head__`, `__torso__`, `__limbs__`). **Expand all**, **Collapse all** and **Levels** control it in bulk. Parts called by the same wildcard share a colour.
- **Right-click** a part for: re-roll, **lock** (Roll new sample keeps it), **choose a line** (pick the exact line from a filterable list), copy its text.
- **Remembered values strip** shows each `${name}` with buttons to re-roll, lock or choose its line.
- **Unlock all** releases every lock and chosen line.
- **Exactly what gets saved** is the final text after tidy, prefix, suffix and weight handling.
- **Seed**: the same seed and template give the same sample. Editing text keeps the other choices stable.

In the template editor, click inside a green tag and press the **▸** button at the right edge of the line. You see the file's lines and can replace the tag with one of them.

## 5. Model and length

Pick your model under **Model and length**. A gauge under the sample shows an estimated token count with the model's recommended length and hard cutoff.

- Numbers are **estimates** until you calibrate: press **Calibrate…** and enter the token count your own tool reports for the shown sample.
- Profiles are starting points. Many limits are unverified, and some frontends (ComfyUI) pass long prompts through while others (Forge, sd_webui) chunk or truncate. Set **Frontend** to match.
- **Manage…** lets you edit any profile, save it under a new name, copy or delete a profile or a whole family, import and export profiles, and **Revert all defaults** to the originals.
- **Apply recommended options** sets single paragraph, tidy spacing and weight handling to suit the model.
- **Check length over 200 rolls** shows the shortest, typical and longest prompts and how many exceed the limits.

## 6. Prefix, suffix and negative prompt

Set text added to every copy, saved sample and export. They may contain wildcards, but are chosen separately from the template. **Remove (word:1.2) weights** applies when the chosen model ignores weights.

## 7. Exports

**Batch of random prompts** (up to 1,000): a fresh random seed per prompt, optional duplicate skipping, optional reproducible seeds. Choose the format:

- **Text**: one prompt per line. Optionally a matching `_negative` file with the same number of lines.
- **CSV**: number, seed, prompt, negative, and the picks that made it.
- **JSON**: the same, structured.

**Split every N prompts** writes several numbered files.

**Sweep one wildcard** writes one prompt for every line of the chosen wildcard while everything else is random. Repeat each value several times for variety.

**All possible prompts** writes every combination. It is available when the template uses exactly one wildcard (or when you allow several). A reused `${name}` counts once.

If no output folder is set, saves go to the browser's Downloads (a save dialog appears when the browser supports it).

## 8. History, Library, Tabs, Versions, Projects

- **History** keeps the last 60 samples. **★ Keep** stores favourites with their template. **Restore** brings back template, seed, locks and chosen lines.
- **Library**: *Search lines* across every file; *Health check* finds empty files, missing references, loops, duplicate and near-duplicate lines, unbalanced braces and unused files; *Where used* shows which files and templates use a wildcard. In the file viewer, **Remove duplicates** cleans a file (then **Save file**).
- **Rescan on return** (Output options) refreshes the list when you come back to the window after editing files elsewhere.
- **Tabs** hold several templates at once. Closing a tab keeps a version.
- **Versions…** lists autosaved and named versions, compares them with the current text and restores them. They live inside this browser.
- **Projects** save the open tabs (with prefix, suffix, negative and model) and your output settings under a name, and can be exported and imported as files.

## 9. Folders

**Folders** in the header sets separate remembered folders for wildcards, templates, single samples, batches and all-prompts exports. Windows may ask you to re-allow access after you reopen the app. Browsers refuse a few top-level system folders (Documents, Downloads, Desktop); pick a subfolder inside them.

## 10. Shortcuts

Ctrl+S save template · Ctrl+Shift+S save as · Ctrl+Enter new sample · Ctrl+O open · Esc closes menus.

## 11. Troubleshooting

- **All tags are red.** The linked folder has no matching files. Check that you linked the folder holding your wildcards, not your batch output folder.
- **Typed `${` and nothing happens.** Turn **Remember and reuse** on in Output options. Turn it off if your prompts need a literal `${`.
- **Weights look ignored.** Tick **Weighted options**, and put the weight first: `3:: a red coat`.
- **A tab or sample came back different.** Wildcard files or output settings changed since it was saved.
- **Saved to Downloads, not my folder.** Set the folder under **Folders**; use Edge or Chrome.
- **The token gauge disagrees with my tool.** Press **Calibrate…**.

## 12. Honest limits

- Token counts are estimates until calibrated. Exact tokenizers need large vocabulary files that this offline page does not include.
- Model limits are starting points from research and community reports, several marked estimate or unverified. Test yours and edit the profile.
- Versions, history, favourites, projects and tabs live in the browser's own storage. Export projects you care about. Clearing site data erases them.
