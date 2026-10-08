# Games

The home page for https://games.shauna.digital, listing Shauna's browser games.

## How it is set up

- This repository is a plain static site: `index.html` plus `vercel.json`. There is no build step and no framework.
- Hosting: Vercel project `games` (team `shaunagits-projects`), deployed automatically from the `main` branch. Pushing to `main` updates the live site.
- Domain: `games.shauna.digital` is attached to that Vercel project. DNS for `shauna.digital` is managed at Namecheap, where a CNAME record for the host `games` points to Vercel.
- Each game lives in its own repository and its own Vercel project. This site mounts a game under a path using a rewrite in `vercel.json`, so the game appears at `games.shauna.digital/<path>` without being copied here.

## Games mounted here

| Path | Repository | Vercel project | Address it forwards to |
|---|---|---|---|
| `/13-beads` | `shaunagits/13-beads` | `13-beads` | `https://13-beads.vercel.app` |
| `/homebeforedark` | `shaunagits/homebeforedark` | `homebeforedark` | `https://homebeforedark.vercel.app` |

## Add a game

1. Deploy the game as its own Vercel project. It must use relative asset paths so it works under a subpath (for a Vite project, set `base: './'`).
2. In `vercel.json`, add three rules for its path. All three are needed:
   - a redirect from `/<path>` to `/<path>/`, so relative asset paths resolve correctly;
   - a rewrite for `/<path>/` itself (the wildcard rule does not match the bare folder path);
   - a rewrite for `/<path>/:path*`.
3. Add a card for it to the list in `index.html`, linking to `/<path>/`.
4. Add a row to the table above.
5. Push to `main`, then check the home page, `/<path>`, and that the game's script files load.

## Things to know

- A game saves player data per web address. Data saved at a game's own `vercel.app` address does not appear at `games.shauna.digital/<path>`.
- The home page design is a placeholder and is expected to change. Colors and fonts are defined at the top of the `<style>` block in `index.html`.
- All artwork is original. No artist names, logos, album artwork, or lyrics.
