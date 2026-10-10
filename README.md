# VoltLab Academy — full-stack starter

A responsive electrical-engineering learning platform with:
- Email + password accounts and server-side sessions
- SQLite database for accounts and progress
- Cross-device progress sync when deployed with the same persistent database/session setup
- Course lessons and completion tracking
- Circuit diagrams (SVG), concept-level motor simulation, practical lab worksheets
- Single-phase, three-phase and motor-sizing educational calculators
- Quiz with feedback, formula reference, safety reminders

## Run locally

Requirements: Node.js 20+ and npm.

```bash
npm install
cp .env.example .env
# Edit .env and set SESSION_SECRET to a long random secret.
npm start
```

Open http://localhost:3000.

On Windows PowerShell, copy the environment template with:
```powershell
Copy-Item .env.example .env
```

## Database and synchronization

The SQLite database is created automatically at `./data/voltlab.sqlite`. For cloud sync, deploy this app to a host that supports Node.js and attach a **persistent disk** for the database. Configure `DB_FILE` to a path on that disk. Use the same live deployment URL across devices. The current SQLite approach is suitable for a small learning project; for larger multi-instance deployments use a managed PostgreSQL database and a shared session store.

## Production checklist — do not skip

- Set a long random `SESSION_SECRET`; never deploy with the development fallback.
- Set `NODE_ENV=production` and `COOKIE_SECURE=true` when served through HTTPS.
- Use HTTPS only; configure trusted proxy settings according to your host if needed.
- Replace Express's default in-memory session store with a persistent production session store (e.g. a compatible SQLite/PostgreSQL/Redis store). The built-in MemoryStore is not production-ready and sessions may be lost on restart.
- Add database backups, monitoring, account deletion/export, privacy policy, terms and age-appropriate account handling before public launch.
- Consider email verification, password reset, CSRF defenses appropriate to your deployment, and stronger abuse controls before opening registration publicly.
- Never commit `.env` or the live database file to source control.

## Safety scope

The motor panel is a **conceptual, low-voltage virtual simulation** for learning about start/stop logic and overload trips. It does not show mains wiring terminals, does not control real equipment, and is not a substitute for supervised electrical training. Never use the site to guide live work.

## Important limitation

This ZIP is an application source project, not a published website. Cloud synchronization works only after the server is deployed and reachable by your devices. A production launch requires hosting, HTTPS, a persistent database, and the checklist above.
