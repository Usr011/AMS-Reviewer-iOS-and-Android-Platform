# AMS Reviewer (iOS)

The app is a thin wrapper around your live site. It loads
`https://wenwenamstheoreviewer.orellabac-mniwrehs.workers.dev/`
directly (see `capacitor.config.json`'s `server.url`), so the
theoretical reviewer, the `/theoretical` page, the practical
reviewer at `wenwenamsreviewer.orellabac-mniwrehs.workers.dev`, and
your Google sign-in gate all come straight from Cloudflare — nothing
is bundled into the app itself anymore. `www/index.html` is only an
offline fallback shown if the app can't reach the internet.

Because the content lives on your server instead of inside the
`.ipa`, there's nothing for someone to extract from the app file —
they still have to sign in with Google on your site to see anything.

## Get the .ipa (no Mac needed)
1. Create a free GitHub account and a **new private repository**.
2. Upload everything in this folder, including the hidden `.github`
   folder — on GitHub's web uploader, hidden folders can get skipped,
   so if "Build IPA" doesn't show up under the Actions tab afterward,
   use "Add file → Create new file" and type the path
   `.github/workflows/build-ipa.yml` directly into the filename box,
   then paste that file's contents in.
3. Open the **Actions** tab → **Build IPA** → **Run workflow**. Wait ~5–10 min.
4. Open the finished run → download the **AMSReviewer-ipa** artifact → unzip → `AMSReviewer.ipa`.

## Sideload
Use Sideloadly or AltStore with your Apple ID. It signs the unsigned IPA for you.
Free Apple IDs expire after 7 days; just re-sign/refresh.

## Android (.apk)
Same repo also has a **Build APK** workflow — run it from the Actions
tab the same way as Build IPA. It's much simpler on Android: no
signing service needed. Download the **AMSReviewer-apk** artifact,
unzip it to get `app-debug.apk`, and send that file straight to a
friend's phone (Drive, Telegram, whatever). To install it, they just
need to allow "Install unknown apps" for whichever app they downloaded
it through (Settings → Apps → Special access → Install unknown apps),
then tap the file. No re-signing, no expiry, no extra tool.

This APK is signed with Android's generic debug key rather than a
real release key, which is fine for installing yourself or sharing
with friends, but Android will show a plain "unverified app" notice
rather than a verified developer name.

## If you change the site's URL later
Edit `server.url` (and the matching entries in `allowNavigation`) in
`capacitor.config.json`, then re-run both workflows.
