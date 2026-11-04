# Guyanonymous' Prompt Studio

A single-file, fully offline prompt builder for wildcard text files. Open `guyanonymous_prompt_studio.html` in Microsoft Edge or Google Chrome, point it at your folder of `.txt` wildcards, and design prompts with a live nested preview. No install, no server, no account. The page blocks every network request, so nothing can be uploaded.

Current version: **v3.1**

## Highlights

- Folder scan, template editor with `__file__` tags, autocomplete and peek/replace
- Live sample with nested wildcards that open up, re-roll, lock and choose-a-line
- Reusable picks (`${name=__a__}`, `${name}`, `__file$name__`), weights, pick-several
- Model profiles with a token gauge, prefix, suffix and negative prompt
- Batch (TXT, CSV, JSON), sweep and all-combinations export
- History, favourites, library search and health check, tabs, versions and projects

## Documents

- [User guide](docs/GUIDE.md)
- [Changelog](CHANGELOG.md)
- [Share post](docs/SHARE_POST.md) (also as [copy-ready HTML](docs/SHARE_POST.html))

## Repository layout

- `guyanonymous_prompt_studio.html`: the app (always the latest version)
- Git tags `v1` to `v3.1`: every released version. Check one out with `git checkout v2.5`.
- `docs/`: guide and share post

## Releasing a new version

1. Edit `guyanonymous_prompt_studio.html`. Update the title, the header badge and the exported-JSON app name to the new version.
2. Add the new section to `CHANGELOG.md`, and update `docs/` if features changed.
3. Commit with a message beginning with the version, for example `v3.2: ...`.
4. Tag it: `git tag -a v3.2 -m "v3.2: ..."`.
5. Push the branch and tags: `git push origin main --tags`.

Large wildcard data archives (`*.zip`) are not stored in this repository.

## License

Free for non-commercial use. Commercial use, and integration into commercial products, needs written permission. See [LICENSE](LICENSE).
