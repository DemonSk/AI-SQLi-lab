# Verification Log

## Status
✅ App runs and endpoints respond as expected.

## Environment
- Node: v20.20.0 (via nvm)
- npm: v10.8.2

## Commands
```
nvm use 20
npm install
node app/server.js
```

## Runtime checks
- POST /login with payload `' OR 1=1 --` returns `{ ok: true, user: "admin" }`
- POST /assistant returns secret output as expected (vulnerable demo)

## Notes
Node v24 failed to build `better-sqlite3`. Use Node 20 (see `.nvmrc`).
