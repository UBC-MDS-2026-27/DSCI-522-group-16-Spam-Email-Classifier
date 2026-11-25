# Spam Email Classifier 

## Authors 
Audrey Tsung, Ethan Liang, Karn Nijjar

## Summary 
This report investigates whether an email can be accurately classified as spam or non-spam using pre-extracted word frequencies, special character frequencies, and capitalization patterns. Using the UCI Spambase dataset of 4,601 emails, we trained a logistic regression classifier and found that the model's test accuracy was 92.7% (F1 score of 0.906). Dollar signs, large strings of capitalized characters, and words like "free" and "remove" emerged as the strongest predictors of spam. Automated spam detection is critical because unsolicited email drains productivity and drives phishing and fraud, while overly aggressive filters risk blocking important legitimate messages. The main limitations are that the data was collected in 1999—meaning modern spam tactics have evolved—and that the non-spam emails come primarily from a single corporate environment (Hewlett-Packard Labs), limiting generalizability to broader, contemporary inboxes.

## Usage
The analysis runs in a Docker container, so everyone uses the same software and package versions. You do **not** need to install Python, Quarto, or any Python packages on your own computer. Run all commands below from the root of this repository, in a terminal (Terminal on Mac, PowerShell on Windows).

## How To Run The Analysis 
### 1. Install the tools (if not already installed)
- [Docker Desktop](https://docs.docker.com/get-started/get-docker/) (open it and make sure it is running before the steps below)
- [Git](https://git-scm.com/downloads)

### 2. Clone this repository and go to it
 
```
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-group-16-Spam-Email-Classifier.git
cd DSCI-522-group-16-Spam-Email-Classifier
```
 
### 3. Make an ssh key (if you don't have one)
 
```
ssh-keygen -t ed25519
```

Press Enter at each question. Without this key, Docker makes a *folder* named `~/.ssh/id_ed25519.pub`, and ssh into the container fails until you delete that folder and make the key. (If you already have `~/.ssh/id_ed25519.pub` as a file, skip this step.)

To check that the key exists as a file, run:
 
```
cat ~/.ssh/id_ed25519.pub
```
It should print one line starting with `ssh-ed25519`. This is your *public* key, so it is safe to display. If you get "No such file" or "Is a directory", the key is missing or Docker made a folder there.

### 4. Download the image
 
```
docker compose pull
```
 
### 5. Render the report in the container
 
```
docker compose run --rm analysis-env uv run quarto render analysis/spam-email-classifier-report.qmd
```
 
The rendered report is saved as `analysis/spam-email-classifier-report.html`. Open it in your browser.
 
### 6. How the container stops
 
The command above uses `--rm`, so the container is removed automatically when the render finishes. There is nothing to stop.
 
If you instead start the container in the background with `docker compose up -d` (for example, to work in it with Positron; see [CONTRIBUTING.md](CONTRIBUTING.md)), stop and remove it when you are done with:
 
```
docker compose down
```


## Licenses
The code is licensed under the MIT License, and the report is licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License (CC BY-NC-ND 4.0). See [LICENSE.md](LICENSE.md) for details.

## AI Usage Statement 
Our team used generative AI (Claude) as an assistant during this project. All AI-assisted output was edited and verified by team members. All issues, pull requests, and code reviews were initiated and completed by team members. 

We used AI to:
- plan the order of work 
- check the report against the rubric 
- receive feedback on the work 
- suggest and troubleshoot code 
- explore potential references (each suggestion verified by a team member)

Example prompts:
- "What is a logical structure to follow?"
- "Does this paragraph cover the rubric points?"
- "What plot details would most effectively convey the information in the analysis?"

No AI instruction files were used. 

## Link to Report 
The rendered report is available at: [Spam Email Classifier Report](https://ubc-mds-2026-27.github.io/DSCI-522-group-16-Spam-Email-Classifier/analysis/spam-email-classifier-report.html)