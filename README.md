# 🃏 Joker-XD v2.0.5 Multi-Tenant (wolfsocket)

WhatsApp Multi-Device bot powered by **wolfsocket** (Baileys fork with Group Status support) — one server, multiple accounts, **isolated settings per number**.

### Changes in this build
- Switched from `@whiskeysockets/baileys` → `wolfsocket`
- Added `.gstatus` / `.togroupstatus` / `.togstatus` (reply to image/video/text to post Group Status)
- Pairing, multi-session, and all previous features work the same way

## Multi-tenant
- Each paired number has its own folder: `sessions/<number>/auth` + `sessions/<number>/data`
- Owner of a session = that paired number (separate control)
- Settings isolated: mode, prefix, antilink, warns, sudo, ban, autoreact, welcome, etc.
- Server restart → sessions auto-restore from disk

## Limits (2GB RAM)
- Default max concurrent sessions: **5**
- Override: `MAX_SESSIONS=5` env

## Developer-only session commands
Only hardcoded developer (`923354853202` / LID) can use:
- `.sessions` — active + saved list
- `.stopsession <number>` — stop session (auth kept)
- `.startsession <number>` — restore saved session
- `.delsession <number>` — delete auth + data permanently

## Pairing
Open the portal → enter number → get pairing code  
Or: `GET /pair?number=923XXXXXXXXX`

## Run
```bash
OWNER_NUMBER=923xxxxxxxxx PREFIX=. PORT=3000 MAX_SESSIONS=5 npm start
```

## Notes
- Antilink / anti tools: single mode (warn | delete | kick | off) — modes do not stack
- Welcome message once per session (not on every reconnect)
- Download engine: Keith-style multi-API (no yt-dlp)

## FFmpeg
Bot ships with **@ffmpeg-installer/ffmpeg** (bundled binary).  
No system install needed on most hosts. On first run you will see:
```
[ffmpeg] using: /path/to/node_modules/@ffmpeg-installer/.../ffmpeg
```
If conversion fails, install system ffmpeg as fallback:
```bash
# Debian/Ubuntu
sudo apt update && sudo apt install -y ffmpeg
```
