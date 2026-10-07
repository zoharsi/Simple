# Repository notes

- This is a single-file static calculator, not a client/API app. Do not introduce a database or require credentials for setup. History is stored under `calc-tape` in each browser's localStorage (at most 50 entries).
- Base44 Compose serves the read-only checkout directly. Its development-only live-server tool is installed at startup into a separate Docker volume, not into the checkout. There is no application build or package lockfile. Only `index.html` is watched for browser reloads.
- No sandbox-specific application code overrides are needed. The static dev server accepts the proxy host; Google Fonts is optional and falls back to system fonts.
- Check startup with `docker compose -f docker-compose.base44.yml ps` and `curl -fsS http://localhost:3000/`. The served HTML includes the original calculator and live-server's injected reload script.
- No automated test suite is supplied. Browser smoke test: click `2 + 3 × 4 =` and expect `14`; verify the first `calc-tape` record, clear the display, recall that result from history, then try `8 ÷ 0 =` and expect the Hebrew division-by-zero message. Check desktop/mobile overflow. Preserve and restore any preexisting localStorage during tests; never clear another viewer's saved history.
- Setup verification passed arithmetic precedence, persisted history, history recall/clear, division-by-zero handling, display reset, and desktop/mobile rendering without horizontal overflow or console errors.
