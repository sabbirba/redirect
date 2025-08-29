# redirect

A minimal Firebase Hosting repository that performs a permanent (301) redirect from the site root to a target URL.

This project contains a single `firebase.json` that configures hosting with a redirect from `/` to `<REDIRECT_URL>`. Replace the placeholder with the real destination before deploying.

## What this repo does

- Uses Firebase Hosting to redirect requests for `/` to the configured `destination`.
- The redirect is a 301 (permanent) redirect.

## Files

- `firebase.json` - Firebase Hosting configuration. Key snippet:

```json
{
  "hosting": {
    "public": ".",
    "redirects": [
      {
        "source": "/",
        "destination": "<REDIRECT_URL>",
        "type": 301
      }
    ]
  }
}
```

Replace `<REDIRECT_URL>` with the URL you want users to be redirected to (for example, `https://example.com`).

## Quick start (deploy)

1. Install the Firebase CLI if you don't have it:

```bash
npm install -g firebase-tools
```

2. Login and select or create a Firebase project:

```bash
firebase login
firebase projects:list
firebase use --add
```

3. Edit `firebase.json` and set `destination` to your target URL.

4. Deploy hosting:

```bash
firebase deploy --only hosting
```

5. After deploy, visit the Hosting URL shown by the deploy command to confirm the redirect.

## Local testing (optional)

You can test the redirect locally with the Firebase emulator:

```bash
firebase emulators:start --only hosting
# then visit http://localhost:5000/ (or the port printed by the emulator)
```

Or check the HTTP response headers with curl:

```bash
curl -I https://<your-hosting-site>.web.app/
```

## Notes & security

- `public: "."` means the repository root is used as the public directory. Ensure there are no sensitive files you don't want publicly accessible in this repo when deploying.
- Use a fully-qualified URL (including scheme `https://`) for `destination`.
- 301 is a permanent redirect; browsers may cache this. If you need a temporary redirect, change `type` to `302`.

## Troubleshooting

- If deploy fails with authentication errors, run `firebase login` again.
- If your redirect doesn't work, confirm the `firebase.json` was updated and that you deployed the correct Firebase project.

## License

This repository contains configuration only. Use under the terms you choose.

## Credits

Created and maintained by Sabbir Bin Abbas — https://github.com/sabbirba
