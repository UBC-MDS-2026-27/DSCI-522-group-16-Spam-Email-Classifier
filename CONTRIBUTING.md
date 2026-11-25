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

### Suggesting Enhancements or Changes

Have an idea to improve feature engineering, model performance, documentation, or visualizations?

1. **Open an issue:** Create a [new issue](https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier/issues) labeled `enhancement`.
2. **Explain your proposal:** Clearly describe the proposed change, why it would be useful for the Spam Email Classifier, and any potential impacts on existing workflows or dependencies.
3. **Discuss first:** For major changes (such as switching classifiers or altering data pipelines), please wait for feedback from the core team before writing extensive code.

---

## Submitting Your Work (Pull Request Workflow)

We follow a standard GitHub fork-and-pull workflow. Follow these steps to submit changes:

1. **Fork the repository:** Click the **Fork** button at the top right of the [repository page](https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier) to create your own copy.
2. **Clone your fork locally:**
   ```bash
   git clone https://github.com/<your-username>/DSCI-522-group-16-Spam-Email-Classifier.git
   cd DSCI-522-group-16-Spam-Email-Classifier
   ```
3. **Set up the environment:** Ensure you can run the project locally using the environment configuration files provided in the repository root (see [README.md](https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier/blob/main/README.md) for setup instructions).
4. **Create a new branch:** Never commit directly to `main`. Create a descriptive branch for your work:
   ```bash
   git checkout -b fix/typo-in-readme
   # or
   git checkout -b feat/add-roc-curve
   ```
5. **Make your changes:** Write clean, well-documented code. Ensure all existing tests pass and add new unit tests if you introduce new functionality.
6. **Commit your changes:** Write clear, concise commit messages explaining *what* changed and *why*.
   ```bash
   git add .
   git commit -m "Add precision-recall curve plot to evaluation script"
   ```
7. **Push to your fork:**
   ```bash
   git push origin <your-branch-name>
   ```
8. **Open a Pull Request (PR):**
   - Navigate to the [original repository](https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier/pulls) and click **New Pull Request**.
   - Select your fork and branch to compare against our `main` branch.
   - Fill out the PR description with a summary of your changes and link any related issues (e.g., `Closes #12`).
   - A member of the core team will review your PR, provide feedback if needed, and merge it once approved.

---

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