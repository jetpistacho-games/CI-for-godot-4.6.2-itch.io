# CI for Godot 4.6.2 → itch.io

Automated deployment workflow for Godot 4.6.2 games to itch.io via GitHub Actions.
Supports HTML5, Windows, Linux, macOS and Android.

## Setup

### 1. Add the workflow
Copy `deploy.yml` to `.github/workflows/` in the root of your repository.

### 2. Configure export presets
Add the necessary export presets in Godot (**Project → Export**) and make sure
`export_presets.cfg` is committed to your repository.

### 3. Create repository secrets
Go to **Settings → Secrets and variables → Actions** and add the following secrets:

| Secret | Description |
|---|---|
| `BUTLER_API_KEY` | Your itch.io API key — get it at https://itch.io/user/settings/api-keys |
| `ITCHIO_USER` | Your itch.io username |
| `ITCHIO_GAME` | Your game's slug |

`ITCHIO_USER` and `ITCHIO_GAME` must match your game's URL:
`https://ITCHIO_USER.itch.io/ITCHIO_GAME`

#### Android-only secrets

| Secret | Description |
|---|---|
| `ANDROID_KEYSTORE_BASE64` | Your keystore file encoded in base64 |
| `ANDROID_KEYSTORE_PASSWORD` | Keystore password |
| `ANDROID_KEY_ALIAS` | Key alias |
| `ANDROID_KEY_PASSWORD` | Key password |

## Deploying

Create a git tag starting with `v` to trigger the workflow (you can change this in the line 6 of the script):

```bash
git tag v0.2
git push origin v0.2
```

You can monitor the deployment progress in the **Actions** tab of your repository.

## Skipping platforms

To skip a platform, remove its two corresponding steps from `deploy.yml`:

| Platform | Steps to remove |
|---|---|
| Android | `Setup Android keystore`, `Setup Android editor settings`, `Export Android`, `Push Android to itch.io` |
| Web | `Export Web`, `Push Web to itch.io` |
| Windows | `Export Windows`, `Push Windows to itch.io` |
| Linux | `Export Linux`, `Push Linux to itch.io` |
| macOS | `Export macOS`, `Push macOS to itch.io` |
