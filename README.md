# PositionLab production deployment

## Included
- `PositionLab-production.html` — updated application
- `privacy.html` — privacy policy
- `terms.html` — terms of use
- `disclaimer.html` — trading risk disclaimer
- `about.html` — about/creator page
- `manifest.json` — PWA metadata
- `_headers` — Netlify security headers
- `netlify.toml` — Netlify publish configuration
- `robots.txt`
- `.well-known/security.txt`

Keep your existing `icon.svg` and `icon-192.png` assets beside the HTML file because the app and manifest reference them.

## Google Drive / OAuth
The OAuth client ID remains in the frontend. A browser OAuth client ID is not a password or API secret and cannot be hidden from a site visitor. The important change is that access tokens are now memory-only rather than being saved in `localStorage`.

In Google Cloud Console, configure your production site's exact HTTPS origin as an authorized JavaScript origin and configure the appropriate OAuth consent-screen settings.

## Netlify
Upload the contents of this package to the site's publish directory. `_headers` will apply the security headers automatically on Netlify.

## Important production improvement
The original site uses Tailwind's browser CDN. Tailwind documents that the Play CDN is intended for development, not production. For a stricter production setup, move Tailwind to a build step and serve compiled CSS as a static file. The rest of this package is designed so that change can be made without changing the application's data model.

## Data model / privacy
PositionLab remains browser-first. User-entered data is stored in browser storage, with optional sync to the user's Google Drive. Access tokens are held in memory during the session.

## Release checklist
1. Deploy over HTTPS.
2. Verify Google OAuth redirect/origin configuration.
3. Test Drive Sync in an incognito window and on mobile.
4. Verify deleting records and disconnecting Drive behave as expected.
5. Verify legal pages and social links load from the production domain.
6. Keep the Google OAuth client ID restricted to the domains/origins you actually use.
