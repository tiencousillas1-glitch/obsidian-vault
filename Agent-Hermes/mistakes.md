# Mistakes Log

## 2026-04-23

### Forgot Veotres/Fiber/Nova context
**Mistake:** Tien asked about topics I had supposedly discussed before, but I couldn't recall them.
**Cause:** Never saved to MEMORY.md or Obsidian
**Fix:** Now implemented complete 4-layer system. Always write pending topics to vault immediately.
**Lesson:** If Tien mentions a project/topic for the first time, write it to project-state.md before ending the session.

## Pre-2026-04-23 (retrospective)

### Auth cookie debugging
**Issue:** AUTH_COOKIE truncation showed `hermes...auth` — looked for wrong cookie name
**Fix:** Use charCodes to verify exact string match
**Lesson:** Terminal display truncation lies. Always verify with code.

### HCI decodeURIComponent corruption
**Issue:** parseCookies() used decodeURIComponent() which corrupts HMAC tokens with % chars
**Fix:** Don't decode URI components in cookie parsing
**Lesson:** Token/HMAC data must never be URI-decoded

### Ollama service path
**Issue:** Systemd pointed to ~/.local/bin/ollama which didn't exist
**Fix:** Use official install.sh instead
**Lesson:** Always verify binary paths match where package manager installs

