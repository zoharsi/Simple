# Development notes

- The Base44 preview serves the bind-mounted HTML directly with Python's static server; there are no dependencies, build output, backend, or required secrets.
- Start with `docker compose -f docker-compose.base44.yml up -d`. Check `/` on port 3000 and the Compose health status.
- The static server reads changed source on each request but does not inject browser live reload. Refresh the preview after edits.
- The first `:root` palette is for light mode. Two later dark-mode overrides deliberately retain their own `--eq` values; do not replace all occurrences for light-only changes.
- Calculation history persists in the browser under `calc-tape`; preserve existing history during tests.
- For the green-theme change, verify the title, history heading, and first `--eq` declaration. `git diff --check` checks patch whitespace.
