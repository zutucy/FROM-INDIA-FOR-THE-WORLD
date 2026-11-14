# GitHub Publishing Guide

This guide helps the maintainer publish the handbook as a public educational repository.

## 1. Recommended repository settings

- **Repository name:** `social-technology-engineering-handbook`
- **Visibility:** Public (so readers can access the learning material)
- **Description:** `A Hinglish-friendly, history-first learning handbook covering computing, software engineering, networking, cybersecurity, AI, distributed systems, product design and global technology operations.`
- **Topics:** `computer-science`, `software-engineering`, `web-development`, `networking`, `cybersecurity`, `artificial-intelligence`, `distributed-systems`, `technology-education`, `hinglish`, `learning-resource`
- **Website:** leave blank until you have a real project page.

## 2. Before publishing

1. Extract the ZIP archive.
2. Open the extracted folder and confirm it contains `README.md`, `QUESTION.md`, `LICENSE`, `COPYRIGHT_AND_ATTRIBUTION.md`, `handbook/` and `MANIFEST_SHA256.txt`.
3. Read the license decision carefully. This is a public, source-available learning resource, **not OSI-approved open source**, because CC BY-NC-ND 4.0 restricts commercial reuse and public distribution of adaptations.
4. Review the creator/AI-assistance wording and ensure you are comfortable publishing it under your name.
5. Review third-party images, diagrams, code, excerpts and trademarks individually. Do not publish material you do not have rights to share.
6. Do not add passwords, API keys, personal data, private files or unpublished business secrets.

## 3. Create the repository on GitHub

1. Sign in to GitHub.
2. Select **New repository**.
3. Enter `social-technology-engineering-handbook` as the repository name.
4. Set visibility to **Public**.
5. Do not initialize another README, license or `.gitignore` because this ZIP already includes them.
6. Create the repository.

## 4. Upload the files using the browser

For a beginner-friendly upload:

1. Open the empty repository.
2. Choose **Add file → Upload files**.
3. Extract the ZIP on your computer first; upload the *contents* of the extracted repository folder, not the ZIP file itself.
4. Preserve the `handbook/` directory and all root files.
5. Use a commit message such as `Publish v1.0.0 educational handbook`.
6. Commit the upload.
7. Open the repository home page and test the README, `QUESTION.md`, several chapter links and the license link.

For large uploads or later updates, Git is more reliable than the browser interface. Install Git, open a terminal in the extracted folder, then use:

```bash
git init
git add .
git commit -m "Publish v1.0.0 educational handbook"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/social-technology-engineering-handbook.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username. Do not paste a personal access token into a command, README, issue or public file. Use Git Credential Manager or GitHub's supported sign-in flow.

## 5. After publication

- Confirm the repository is public and the README renders correctly.
- Confirm `QUESTION.md` links open the expected chapters.
- Confirm GitHub identifies or clearly displays the license notice; if GitHub does not classify the linked CC license automatically, the legal notice and canonical URL still need to remain visible.
- Add release tag `v1.0.0` only after reviewing the published content.
- Use GitHub Issues for corrections and questions; follow `CONTRIBUTING.md`.
- For future editions, update the source register, changelog and SHA-256 manifest.

## 6. Important: public does not mean unrestricted

GitHub documents that public repositories can be viewed and forked by other GitHub users. The repository license still governs the material's permitted reuse. Do not assume that public visibility alone provides a custom copyright license or prevents all copying. Read [GitHub's repository licensing guidance](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository).
