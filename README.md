# StreamableUpload (Vencord Userplugin)

Upload files to Streamable from Discord and post the generated link automatically.

Features:
1. Adds an attach-menu action: Upload File Up to 250 MB.
2. Adds /fileupload slash command support.
3. Waits until Streamable processing finishes before posting the link.

## Requirements

1. Vencord source/developer setup (not packaged-only install).
2. Node.js and pnpm installed.
3. Streamable account credentials.

Official docs:
1. Vencord install docs: https://docs.vencord.dev/installing/
2. Custom plugin docs: https://docs.vencord.dev/installing/custom-plugins/

## Install

Place this plugin folder in:
src/userplugins/fileShare

Then build Vencord:

Windows PowerShell
```powershell
Set-Location $HOME/Vencord
& "$env:APPDATA\npm\pnpm.cmd" build
```

macOS/Linux
```bash
cd ~/Vencord
pnpm build
```

If your runtime uses AppData dist sync (common on Windows), copy build output:

```powershell
$src = "$HOME/Vencord/dist"
$dst = "$env:APPDATA/Vencord/dist"
Copy-Item "$src\*" $dst -Recurse -Force
```

Restart Discord fully (close tray too).

## First Run

1. Open plugin settings for StreamableUpload.
2. Enter Streamable Email and Streamable Password.
3. Optional: enable Auto-Send.
4. Upload with attach menu action or /fileupload.

If credentials are missing, upload is blocked until set in settings.

## Security Notes

1. Password input is masked.
2. Plugin attempts to encrypt password with OS-backed secure storage.
3. If secure storage is unavailable on a system, local settings storage is used as fallback.
4. Recommended: use a dedicated Streamable account for this plugin only.

## Optional Test Mode

Setting: Clear Credentials On Disable

1. Off (default): better daily usability.
2. On: useful for repeatedly testing first-run behavior.

## Troubleshooting

1. Settings fields do not appear:
1. fully restart Discord (including tray)
2. confirm plugin name is StreamableUpload

2. Streamable login failed (401):
1. re-check email/password in plugin settings
2. test logging in to Streamable in browser

3. Streamable blocked request (403):
1. account may need verification/permissions
2. retry later or check account status

4. Upload rejected (400):
1. try another file
2. reduce file size or re-encode

5. Processing timeout/failure:
1. wait and retry
2. test with shorter MP4 clip first

6. Build command fails on Windows with script policy:
1. use pnpm.cmd path as shown above

## Share Checklist

When sharing with others, include:
1. This folder at src/userplugins/fileShare.
2. This README.
3. Exact build command for their OS.
4. Reminder to restart Discord fully after build.
5. First-run credential setup steps.
