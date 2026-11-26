# Contributing to Spam Email Classifier

Thank you for your interest in contributing to the **Spam Email Classifier** project (`DSCI-522-group-16-Spam-Email-Classifier`)! This document outlines how to propose a change.

Please take a moment to review this document to make the contribution process smooth and effective for everyone.

---

## Code of Conduct

This project adheres to a Code of Conduct to ensure a welcoming and inclusive environment for all contributors. By participating, you are expected to uphold this code. Please see our [CODE_OF_CONDUCT.md](https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier/blob/main/CODE_OF_CONDUCT.md) for full details and reporting procedures.

---

## How Can I Contribute?

### Fixing Typos
Small typos or grammatical errors in documentation may be edited directly using the GitHub web interface, so long as the changes are made in the *source* file. 

- YES: you can edit the Quarto source file `analysis/spam-email-classifier-report.qmd`.
- NO: you edit the rendered `.html` file.

### Prerequisites
Before you make a substantial pull request, you should always file an issue and make sure someone from the team agrees that it is a problem. If you have found a bug, create an associated issue and include:  
   - A clear description of what happened versus what you expected to happen.
   - The exact commands you ran to reproduce it. 
   - Error messages and full stack traces (if applicable).
   - Your operating system and whether the problem happens inside the container.

For major changes (such as switching classifiers or altering the data pipeline), wait for feedback from the team before writing extensive code. 

## Setting up the project
 
We develop in the same Docker container that users run the analysis in, so everyone uses the same software and package versions. First follow the [Usage section of the README](README.md#usage) (install Docker and Git, clone the repository, make an ssh key, and download the image with `docker compose pull`). We do not repeat those steps here. Run all commands below from the root of this repository.
 
## Working in the container
 
We edit and run the code inside the container by connecting Positron to it over ssh. Your project folder is shared with the container at `/workspace`, so a file you change there changes on your computer too.
 
### Once, before your first connection
 
1. Install [Positron](https://positron.posit.co/download.html) on your computer. Its **Remote SSH** feature, which connects to the container, is built in, so you don't need to install an extension.
2. Make sure you followed the [Usage section of the README](README.md#usage): you made an ssh key (check that the file `~/.ssh/id_ed25519.pub` exists) and you ran `docker compose pull`.
3. Check that Git knows who you are on your computer:
```
git config --global user.email
```
 
   It should print the email of your GitHub account. If it prints nothing, set your name and email:
 
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
 
   `docker-compose.yml` shares your `~/.gitconfig` with the container, so the commits you make there count as yours.
 
### Each time you work on the project
 
1. In a terminal, in the root of this repository, start the container in the background:
```
docker compose up -d
```
 
   `docker compose ps` should list `analysis-env` as running.
 
2. In Positron, open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows).
3. Type and run **Remote SSH: Show Remote Menu**, then pick **Connect to Host**.
4. Type `root@localhost:2222` and press Enter. A new Positron window opens.
   - If it asks for the platform of the remote host, pick **Linux**.
   - If it asks whether you trust the host (a "fingerprint"), click **Continue**.
   - The first time, Positron installs its server inside the container. This can take several minutes.
5. **Open the project folder.** The bottom left corner now shows `SSH: localhost:2222`, but the Explorer says **No folder opened** and the terminal starts in `/root`, which has no project files. That is normal.
   - Click **Open Folder** in the Explorer.
   - Delete what is in the path box at the top of the window, type `/workspace`, and press Enter (or click "OK"; you may need to click "OK" a few times before this works).
   - The window reloads, and the Explorer shows **WORKSPACE [SSH: LOCALHOST:2222]** with the project files. A file you change here changes on your computer too.
6. **Pick the Python interpreter.** Positron may start a different Python than the project's, so check this every time.
   - Click the interpreter button at the top right of the window. The **Running Interpreter Sessions** menu only lists sessions that are already running (such as `/usr/bin/python3`, the container's system Python: not this one).
   - Click **New Console Session...** and pick the one named **Python 3.x (uv: your-project-name)** with the path `/opt/venv/bin/python`. This is the environment built from `uv.lock`, and the top right button then shows that name.
   - If it isn't in the list, run **Python: Select Interpreter** from the Command Palette, choose **Enter interpreter path...** and type `/opt/venv/bin/python`.
   - Don't pick `/workspace/.venv`: that is an environment from your own computer, and it doesn't run in the container.
   - To check, run `import sys; print(sys.executable)` in the Console. It should print `/opt/venv/bin/python`.
7. Work as usual. The Terminal, the Console and the **Render** button all run inside the container.
8. When you are done, close the Positron window, then stop and remove the container in a terminal on your computer:
```
docker compose down
```
 
### If it doesn't connect
 
- **`~/.ssh/id_ed25519.pub` is a folder:** Docker made it because the key didn't exist yet. Run `docker compose down`, delete that folder, make the key (see the [README](README.md#usage)), and start again.
- **`~/.gitconfig` is a folder, or Git in the container doesn't know your name:** the same thing happened with your Git settings. Run `docker compose down`, delete that folder, set your name and email (see above), and start again.
- **It asks for a password:** the container can't see your key. Check that your key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.
- **"Remote host identification has changed":** you are using a new image. Run `ssh-keygen -R "[localhost]:2222"`, then connect again.
- **GitHub asks you to sign in when you push from the container:** sign in once in the browser window Positron opens. Positron remembers it.
- **Linux laptops:** ssh refuses the key because the file belongs to you, not `root`. Remove the `#` from the `StrictModes no` line in the `Dockerfile` and push, so the workflow publishes a fixed image.
- **Port 2222 is already in use:** change the first `2222` in `docker-compose.yml` to another number (e.g. `2223`), and connect to that port instead.
More detail: [Working in a container over ssh with Positron](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/lectures/containers-ssh-positron.html).
 
To re-run the analysis and render the report without opening the container in Positron:
 
```
docker compose run --rm analysis-env uv run quarto render analysis/spam-email-classifier-report.qmd
```
 
## Adding or updating a package
 
On a new branch, add the package with `uv add <package>==<version>` (this pins the version in `pyproject.toml` and updates `uv.lock`), then commit the changed `pyproject.toml` and `uv.lock` together and push them. GitHub Actions then builds and publishes a new image on Docker Hub, and commits the new `sha-` tag to the `image:` line of `docker-compose.yml` on your branch. When the workflow finishes, get that commit and download the new image:
 
```
git pull
docker compose pull
```
 
Then merge the branch into `main` in a pull request.
 
## Publishing the report
 
The report on GitHub Pages is a copy of the rendered report in `docs/index.html`. Each time you re-render the report, copy it there again, then commit and push:
 
```
cp analysis/spam-email-classifier-report.html docs/index.html
```
 
(On Windows PowerShell, use `Copy-Item analysis/spam-email-classifier-report.html docs/index.html`.)
 
## Pull request process
 
We follow a standard GitHub workflow.
 
- Create a new Git branch for each pull request (PR), starting from an up-to-date `main`. Do not commit directly to `main`.
- Give the branch a short name that describes the work, for example `fix-readme-typo` or `add-roc-curve`.
- Keep each branch small: one independent piece of work per branch.
- Before opening the PR, render the report in the container to check that the analysis still runs from start to finish.
- Open a PR into `main` and describe what changed and why. Link the related issue (e.g., `Closes #12`).
- At least one other team member must review and approve the PR before it is merged. The reviewer, not the author, merges it.
- New code should follow the PEP8 [style guide](https://peps.python.org/pep-0008/).

## Generative AI Policy

We recognize that generative AI tools (such as ChatGPT, GitHub Copilot, and Claude) can be helpful aids during software development and data analysis. However, to maintain code quality, reproducibility, and academic/course integrity, all contributors must follow these rules:

1. **Human-Driven Workflow (No Autonomous AI Agents):**
   - All issues and pull requests **must be opened, reviewed, and merged by a human contributor**, not by an autonomous AI agent or bot.
   - Do not submit unreviewed, bulk AI-generated code or documentation.
2. **What is Allowed:**
   - You may use generative AI tools to assist with brainstorming, debugging error messages, writing boilerplate code, refactoring functions, or drafting documentation.
3. **Mandatory Disclosure:**
   - If you use generative AI tools to substantially generate or modify code, tests, or text in a pull request, you **must disclose** this in your PR description (e.g., noting which tool was used and which files or functions were assisted by AI).
4. **Contributor Responsibility:**
   - **You are 100% responsible for every line you submit.** Before opening a PR, you must thoroughly read, understand, test, and verify all AI-assisted code to ensure it is accurate, secure, properly licensed, and adheres to our project's style and reproducibility standards.

---

## Attribution

- The structure and workflow sections of this document were adapted from the [Altair Contributing Guide](https://github.com/vega/altair/blob/main/CONTRIBUTING.md) and the [dplyr Contributing Guide](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md).
- The Generative AI Policy was adapted from the AI contribution guidelines of [SciPy](https://docs.scipy.org/doc/scipy/dev/core-dev/index.html#use-of-generative-ai) and [earthaccess](https://github.com/nsidc/earthaccess/blob/main/CONTRIBUTING.md).