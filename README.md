# Bun egg for Pelican

Import [`egg-bun.yaml`](egg-bun.yaml) using its raw GitHub URL, create a server, and configure the variables below. Pelican pulls the published Debian image and installs Bun automatically.

Upload your Bun project or set a GitHub repository, which is cloned during installation. Each startup optionally pulls, installs dependencies from `package.json` plus any additional packages, and runs `bun run <file>`. Pull or install failures stop startup.

| Variable | Default | Description |
| --- | --- | --- |
| `BUN_FILE` | `index.ts` | File or `package.json` script passed to `bun run`. |
| `BUN_PACKAGES` | Empty | Optional space-separated packages, e.g. `zod@3 dotenv`. |
| `GITHUB_REPO` | Empty | Optional `owner/repo` or GitHub URL; `/tree/dev` selects `dev`. |
| `GITHUB_TOKEN` | Empty | Optional read-only PAT, set in admin startup settings. |
| `PULL_ON_STARTUP` | `0` | Set to `1` to pull before installing dependencies. |

Public repositories need no token. Cloning requires an empty server directory, so set `GITHUB_REPO` before installing, or clear the files and reinstall. Pulls are fast-forward-only. Branch URLs select that branch; plain repository URLs use the default branch on clone and the current branch afterward. Dependencies are installed with `--no-save`, so `package.json` and `bun.lock` are never modified. Reinstall to update Bun and the startup script in `.pelican`; don't delete that folder.

For network services, bind to `0.0.0.0` and read `SERVER_PORT`. Stopping sends SIGINT.
