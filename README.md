# LockIn support site

A standalone, responsive support page for LockIn. It uses the app’s existing support email, orange and navy branding, and help content. No build, dependencies, analytics, or external fonts.

## Published site

**Support URL:** https://lockin-support.web.app

**Privacy Policy URL:** https://lockin-support.web.app/privacy.html

**Repository:** https://github.com/SenseiBlueBear2/lockin-support

Firebase Hosting publishes the primary support page from the dedicated `lockin-support` site in the existing `lockin-tutor-app` project. This uses Firebase’s included `web.app` subdomain.

To update the primary page, edit the files in this folder, then run:

```sh
cd support-site
npx firebase-tools deploy --only hosting --project lockin-tutor-app
```

The local `firebase.json` explicitly targets `lockin-support`; the app’s existing Hosting site has its own configuration in the project root.

The GitHub Pages mirror remains at https://senseibluebear2.github.io/lockin-support/. To update that mirror, upload changed `index.html`, `styles.css`, or `favicon.svg` files from this folder to the GitHub repository root and commit to `main`. Local changes are not automatically synchronized to that separate repository.

## Preview

Open `index.html` in a browser, or run this from the LockIn project root:

```sh
python3 -m http.server 4173 --directory support-site
```

Then visit http://localhost:4173.

## GitHub Pages setup reference

Use a repository named **lockin-support** to publish this page without publishing the app’s source code.

1. Sign in at https://github.com/new and create a public repository named `lockin-support`. Initialize it with a README.
2. Choose **Add file → Upload files**. Upload only `index.html`, `styles.css`, and `favicon.svg` from this folder to the repository root, then commit. These are all the files the page needs.
3. Open **Settings → Pages**. Under **Build and deployment**, select **Deploy from a branch**, choose **main** and **/ (root)**, and save.
4. Wait for the Pages deployment to finish. GitHub displays the published URL in **Settings → Pages**.
5. Use that published HTTPS address as the app’s **Support URL** in App Store Connect. It will normally be `https://YOUR-USERNAME.github.io/lockin-support/`; use the actual address GitHub shows.

## Alternative: publish from the app repository

The app repository includes `.github/workflows/support-pages.yml`. After connecting this checkout to a GitHub repository, set **Settings → Pages → Source** to **GitHub Actions**. Commit the `support-site` folder and workflow, then push to `main` or run **Deploy LockIn support** manually from the Actions tab. Only `support-site` is included in the published artifact. Your repository does not need to be public if its GitHub plan supports Pages for private repositories.

The workflow publishes to the repository’s Pages root, not a `/support-site/` subpath. Use the URL returned by the deployment. GitHub Pages hosts one site per repository; use the separate repository option if the app repository already hosts another site.

## Content and maintenance

- The contact address is `lockin.customersupport@gmail.com`, matching `app/settings.tsx`.
- Email buttons open a pre-addressed Gmail compose page; the bug report link also supplies a draft template. No information is submitted through this page.
- FAQs use native HTML disclosure controls and work without JavaScript.
- `privacy.html` is the public copy of `privacySections` in `data/appContent.ts`. Keep the web and in-app policy text synchronized when it changes. Use the privacy URL above for App Store Connect’s Privacy Policy URL field.
- Keep the FAQs and response-time estimate aligned with the app when they change.

GitHub’s publishing instructions: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
