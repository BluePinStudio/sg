# Steam games JSONL (GitHub Pages ready)

Static export of Steam games metadata for use in other projects. When GitHub Pages is enabled, the dataset will be served at:

```
https://YOUR_USER.github.io/steam-games/games.compact.jsonl
```

Replace `YOUR_USER` with your GitHub username or org name.

## What is here?

- `docs/games.compact.jsonl` — JSON Lines file (~65 MB). The first line is a meta record, the remaining lines are individual games.
- `docs/index.html` — Landing page with schema and usage examples.

Field abbreviations per game record:

- `a` App ID
- `n` Name
- `d` Developers (array)
- `p` Publishers (array)
- `u` USD price
- `f` Free flag
- `r` Review count
- `y` Release year
- `cs` Current sales flag
- `h` Header image URL
- `t` Tags (array)

## Enable GitHub Pages

1. Push this repo to GitHub.
2. In repository **Settings → Pages**, choose **Source: Deploy from branch**.
3. Select **Branch: main** and **Folder: /docs**, then save.
4. Wait for the Pages build to finish. Verify by opening `https://YOUR_USER.github.io/steam-games/games.compact.jsonl`.

## Consume from another repo

### cURL / CLI

```bash
curl -L https://YOUR_USER.github.io/steam-games/games.compact.jsonl -o games.compact.jsonl
```

### JavaScript (browser or Node)

```js
const url = 'https://YOUR_USER.github.io/steam-games/games.compact.jsonl';

const res = await fetch(url);
const text = await res.text();
const [metaLine, ...gameLines] = text.trim().split('\n');

const meta = JSON.parse(metaLine); // { _meta: { total: 150565 } }
const firstGame = JSON.parse(gameLines[0]);

console.log(meta, firstGame);
```

This load is plain text over HTTPS, so you can use it anywhere that allows HTTP fetches.
