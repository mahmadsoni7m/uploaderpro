# RepoPilot — GitHub Manager v3.0

A mobile-first, Tajik-language GitHub workspace that runs entirely in the browser.

## Features
- Connect to GitHub with a Personal Access Token.
- Search/filter repositories, multi-select, download ZIP backups, and safely confirm deletion of owned repositories.
- **Create repositories** with a name, description, Public/Private visibility, and optional README.
- **View commit history** for the selected repository and branch, open commits on GitHub, and copy commit SHAs.
- Upload a ZIP, multiple files, or a folder to a selected repository/branch with progress and a commit message.
- Enable GitHub Pages for a selected repository.
- Read recent GitHub Actions runs and failed job/step logs, then run local rule-based diagnostics.
- Responsive mobile layout; no app backend.

## Deploy
1. Upload the contents of this folder to the root of a GitHub repository.
2. Open **Settings → Pages** and select **GitHub Actions** as the deployment source.
3. Push to `main`; `.github/workflows/pages.yml` publishes the static site. In repository Settings → Pages, choose **GitHub Actions** if GitHub asks for a source.

## Token permissions
Use a fine-grained token restricted to the repositories you need. Select the minimum permissions required for the features you intend to use:
- **Metadata: Read** and **Contents: Read/Write** for repository listing, commits and uploads.
- **Actions: Read** for workflow runs and logs.
- **Administration: Write** may be required to create/delete repositories; repository creation via `/user/repos` can require account-level token authorization.
- **Pages: Write** for GitHub Pages setup.

GitHub can require organization approval or SSO authorization. Exact permissions can vary by endpoint and account type.

## Security
- Never share or publish your token in source code, commits, screenshots, or logs.
- The optional “remember” checkbox stores the token in `localStorage`, which can be read by scripts running on this site origin. Leave it unchecked on shared devices and clear browser site data after use.
- This static client makes GitHub API requests directly from the browser. Deploy only to a trusted site; a production multi-user service should use a server-side OAuth flow.
- Repository deletion is permanent. RepoPilot asks for confirmation twice and limits bulk deletion to repositories owned by the connected account.
- The log analyzer uses local matching rules, not an AI model.

## Limits
- ZIP support depends on JSZip from jsDelivr and requires internet access.
- Browser memory and GitHub API limits apply. Upload is limited to 500 files per batch and 90 MiB per file in this UI.
- Browser download settings may ask permission when downloading multiple archives.
