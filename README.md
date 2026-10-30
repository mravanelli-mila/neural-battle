# Neural Battle — self-hosted online version

One HTML file. Players open the link and play; nobody logs in. The page signs each
browser in anonymously behind the scenes so a reload keeps your seat.

## One-time setup (about 5 minutes, your account only)

1. Go to https://console.firebase.google.com and **Add project** (any name, Analytics off).
2. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable → Save.**
3. **Build → Firestore Database → Create database → Start in production mode**, pick a region.
4. In Firestore, open the **Rules** tab, replace the contents with `firestore.rules` from this
   folder, and **Publish**.
5. **Project settings (gear icon) → Your apps → Web (</>) → Register app.** Copy the
   `firebaseConfig` values (apiKey, authDomain, projectId, appId) into the block at the top
   of `index.html`.
6. Put `index.html` on any web host (GitHub Pages, Netlify, your own server). It must be
   served over https (every static host does this). Then add your host's domain under
   **Authentication → Settings → Authorized domains** if it isn't there already
   (`localhost` and `*.web.app` are pre-authorized).

## Playing

- Open the site and type your name (remembered by the browser).
- You then see the rooms waiting for an opponent, with the host's name. **Join** one, or
  **Create new room** to host; you get an invite link to send.
- A room nobody joined within 15 minutes is deleted; so is a room both players left, and
  one whose players vanished for 30 minutes. Rooms in progress are not listed.
- The ✕ next to a seat frees it; a seat whose player vanished for 90 s is freed automatically.

## Notes

- The free Firebase tier is far more than enough: a round writes a few hundred small
  documents at most.
- The config block is not a secret (Firebase web keys are meant to be public); access is
  controlled by the rules file.
