# Small Group website

The website for the Small Group app, at https://smallgroupapp.com. It's plain HTML and CSS, served by GitHub Pages from the `main` branch of `JakeDev8/smallgroup-site`. The app itself lives in the SmallGroup repo.

| Page | What it's for |
| --- | --- |
| `/` | What the app is |
| `/support/` | Help. The App Store listing's support link. |
| `/privacy/` | The privacy policy. The app's sign-in screen and You tab link here, and so does the App Store listing. |
| `/terms/` | The terms of use, which people agree to when they sign in |
| `/join/?invite=<id>` | Where invite links go when the app isn't installed |
| `/.well-known/apple-app-site-association` | Tells iPhones that `/join/` links belong to the app |

## Things to know

- **Keep `.nojekyll`.** Without it, GitHub Pages runs Jekyll, which skips folders whose names start with a dot, like `.well-known`.
- **The link file has to stay reachable over HTTPS, with no redirects.** Apple's servers fetch it, not the phone, and keep a copy for a while. To see the copy they have, open https://app-site-association.cdn-apple.com/a/v1/smallgroupapp.com
- **The app only opens links for domains listed under `associatedDomains`** in the app's `mobile/app.json`. That list is part of the native build, so changing it needs a new build.
- **Colors come from the app** (`mobile/src/constants/colors.ts`). Like the app, the site follows the phone's light or dark setting.
- **After editing `style.css`,** bump the `?v=` number where every page loads it, so browsers don't keep the old copy.
- **Once the app is on the App Store,** swap the home page's "Coming soon" badge for an App Store link, and point the join page's "Don't have it yet?" there too.

## Domain

The domain is registered at Porkbun, which also hosts its DNS:

- **Website:** `A` records at the root pointing to GitHub Pages (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`), plus `www` as a `CNAME` to `jakedev8.github.io`.
- **Domain verification:** a `TXT` record at `_github-pages-challenge-JakeDev8`. It proves to GitHub that the domain is Jake's, so nobody else's Pages site can claim it.
- **Email in:** `support@` forwards to Jake's inbox through Porkbun's email forwarding, which adds its own `MX` records.
- **Email out:** sign-in codes and report emails are sent through Resend from `mail.smallgroupapp.com`. Resend's records sit at `send.mail`, `rsend.mail` and `resend._domainkey.mail`, with a DMARC record at `_dmarc`.
