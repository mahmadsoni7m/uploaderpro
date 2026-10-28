# RepoPilot — GitHub Manager

A mobile-friendly, browser-based GitHub repository utility with Tajik UI.

## Features
- Connect to GitHub using a Personal Access Token.
- Search, filter, and multi-select repositories.
- Download repository ZIP archives (one ZIP per selected repository).
- Delete multiple owned repositories with two explicit confirmation prompts.
- Upload ZIP contents, multiple files, or a directory to a selected repository/branch.
- Enable GitHub Pages for a selected repository.
- Local rule-based log diagnosis for common GitHub API, Gradle, Android SDK, and build errors.
- No application backend; token/API requests run in the browser.

## Deploy to GitHub Pages
1. Create a GitHub repository and upload the contents of this folder to its root.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, choose **GitHub Actions**.
4. Push to `main`; the workflow deploys `index.html`.

Alternatively, use **Settings → Pages → Deploy from a branch**, select `main` and `/ (root)`.

## Token permissions
Use the minimum permissions necessary. A fine-grained token should be restricted to selected repositories. Typical permissions:
- **Contents: Read and write** for uploading and downloading private repository archives.
- **Administration: Read and write** for repository deletion (and repository administration actions).
- **Pages: Read and write** to configure Pages, if supported by your token setup.

A classic token commonly needs the `repo` scope for private repositories and repository writes. GitHub may require organization approval or SSO authorization.

## Security notes
- Never publish a token in source code, a public repository, screenshots, or logs.
- The optional “remember” checkbox stores the token in browser `localStorage`, which is accessible to scripts running on this origin. Prefer leaving it unchecked on shared devices and clear site data after use.
- This is a static client-side tool. Use it only on a trusted device and trusted deployment. For a production multi-user service, use a server-side OAuth flow rather than collecting personal tokens in a static page.
- Repository deletion is permanent. The app restricts bulk deletion to repositories owned by the connected account and asks for confirmation twice, but always verify the list before confirming.
- The log analyzer uses local matching rules, not an AI model. It provides likely fixes and can miss novel errors. Remove tokens, passwords, private URLs, and secrets before pasting logs.

## Limitations
- Browser download behavior may ask permission when downloading multiple ZIPs.
- GitHub API and browser memory limits apply. Uploads are capped at 500 files per batch and 90 MiB per file in this UI; Git is recommended for larger projects.
- ZIP parsing uses JSZip from jsDelivr CDN, so ZIP upload requires an internet connection.
- GitHub Pages activation may need repository/organization settings to allow Pages.
