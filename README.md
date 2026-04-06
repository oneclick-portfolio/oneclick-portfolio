# OneClick Portfolio

OneClick Portfolio is a static frontend for importing an `rxresu.me` JSON resume, selecting a theme, and deploying through a separate backend API.

This repository contains the frontend only. The deployment, GitHub auth, and resume validation flows depend on a backend that must be running separately.

## Local Setup

1. Start your backend locally.
2. Set the backend base URL in [config.js](config.js).
3. Serve this frontend locally.

Example local frontend run:

```bash
make dev
```

Default URL:

```text
http://localhost:4173
```

Custom port:

```bash
make dev PORT=3000
```

You can also use any static file server, for example:

```bash
npx serve
```

## API Base URL

The frontend reads the backend URL from [config.js](config.js):

```js
const CONFIG = {
	apiBase: 'http://localhost:8080'
};
```

Use this value based on your environment:

- Local backend: set `apiBase` to your local server, for example `http://localhost:8080`
- Production backend: set `apiBase` to your deployed API, for example `https://op-bot-mauve.vercel.app`

The `Authorize GitHub` flow, auth status checks, resume validation, logout, and deploy actions all use this base URL.

## Backend Endpoints Expected By The Frontend

The frontend expects the backend to expose these routes:

- `GET /auth/github/start`
- `GET /api/github/me`
- `POST /api/github/logout`
- `POST /api/resume/validate`
- `POST /api/github/deploy`

If the backend is not running or `apiBase` is wrong, the UI will load but GitHub connect, validation, and deployment actions will fail.

## Local Workflow

1. Run your backend locally.
2. Set `apiBase` in [config.js](config.js) to that backend URL.
3. Start the frontend with `make dev` or `npx serve`.
4. Open the frontend in the browser.
5. Click `Authorize GitHub` and continue the flow.

## Structure

- [index.html](index.html)
- [config.js](config.js)
- [src/rxresume.js](src/rxresume.js)
- [resume/Reactive Resume.json](resume/Reactive%20Resume.json)
- [themes](themes)
- [Makefile](Makefile)
