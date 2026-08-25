# How the README works

This repo generates a dynamic profile README as an SVG (`dark_mode.svg` / `light_mode.svg`), rendered live by `README.md`.

1. **[.github/workflows/build.yaml](.github/workflows/build.yaml)** runs `today.py` on every push to `main` and on a daily cron schedule.
<br><br>
2. **[today.py](today.py)** queries the GitHub GraphQL API (using a personal access token in `ACCESS_TOKEN`) for account age, commit count, stars, repos, contributions, and followers.
<br><br>
3. Lines-of-code counts are computed by walking commit history per repo and cached in `cache/<sha256 of username>.txt` so unchanged repos aren't re-queried on every run. `cache/requirements.txt` lists the Python dependencies installed by the workflow.
<br><br>
4. The results are stamped into the two SVG templates (`justify_format` / `find_and_replace`), padding values with dots so everything stays aligned.
<br><br>
5. The workflow commits and pushes the updated SVGs back to the repo, so the README (embedded via GitHub's raw SVG URLs) always shows current stats.

## Credit

This project is built on [Andrew6rant](https://github.com/Andrew6rant)'s original dynamic-README generator. All credit for the original design and implementation goes to him - this repo is a personalized fork/adaptation.
