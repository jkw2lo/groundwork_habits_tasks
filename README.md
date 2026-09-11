# Groundwork

Habit tracker + task focus timer, published as a private Claude artifact.

**Live:** https://claude.ai/code/artifact/44836f7b-0c38-41be-9d02-43ed79cb8c22

## Files

| file | role |
|---|---|
| `groundwork.html` | **the source.** Artifact source form — no `<!doctype>`/`<html>`/`<head>`/`<body>`; the publish step adds those. Edit this. |
| `index.html` | generated preview wrapper. Disposable — regenerate with the command below. |

## Updating

Republish `groundwork.html` to the same URL (pass the URL so it updates in place
rather than creating a second artifact). Re-read the live version first — the app
publishes new versions by itself whenever data is saved.

## Careful: `data/tracker.json`

The artifact publishes two files. `data/tracker.json` is **live user data**, written
by the page itself on every check-in — not source, and not in this folder on purpose.
A normal republish of the page carries it over untouched. Never publish a local copy
of it; that would overwrite real history.

## Local preview

```
cd "/Users/jenniferlo/Claude Code/Groundwork" && python3 -m http.server 5191
```

Regenerate the wrapper after editing the source:

```
cd "/Users/jenniferlo/Claude Code/Groundwork" && { printf '<!doctype html>\n<html lang="en">\n<head>\n<meta charset="utf-8">\n<meta name="viewport" content="width=device-width,initial-scale=1">\n</head>\n<body>\n'; cat groundwork.html; printf '\n</body>\n</html>\n'; } > index.html
```
