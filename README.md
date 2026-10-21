# ioncodex.org

The website of IONCODEX LTD. Plain HTML with no build step, hosted for free on GitHub
Pages from the `main` branch of this repository.

## What's here

| File | What it is |
| --- | --- |
| `index.html` | The home page: what we do, our apps, about, contact. Styles are at the top of the file. |
| `privacy.html` | The privacy notice for the website. |
| `favicon.svg` | The browser-tab icon, the same orbit mark as in the header. |
| `assets/` | Images. `mooncycle.png` is the MoonCycle artwork. |
| `CNAME` | Tells GitHub Pages to serve the site on `ioncodex.org`. Don't delete it. |
| `.nojekyll` | Tells GitHub Pages to publish the files as they are, without running Jekyll. |

Every file in this repository is public, on GitHub and on the website. Never put
anything private here.

## Updating the site

1. Edit `index.html` or `privacy.html`. Colours are the `--` variables at the top of each
   page's `<style>`; the two pages each have their own copy.
2. Check it by opening the file in a browser (double-click it). Try a narrow window too:
   the layout is meant to work on phones.
3. Commit and push:

   ```
   git add .
   git commit -m "Describe the change"
   git push
   ```

4. GitHub publishes it within a minute or two. The repository's **Actions** tab shows
   the "pages build and deployment" run; when it's green, the change is live.

Rules worth keeping:

- If you change how the site handles personal information (adding analytics, a contact
  form, embedded videos, web fonts from Google, anything loaded from another company),
  update `privacy.html` and its "Last updated" date first. Most of those would also need
  a cookie banner.
- The company details in the footer (name, number, place of registration, registered
  office) are required by UK law on a company website. If the registered office moves,
  update both pages.
- To add an app, copy the `<article class="app">` block in `index.html` and add its
  artwork to `assets/`.

## Publishing for the first time

Done once. Order matters: verify the domain first, and set the custom domain on GitHub
before pointing DNS at it, so nobody else can claim it in between.

### 1. Verify ioncodex.org with GitHub

1. On GitHub: profile picture → **Settings** → **Pages** (under "Code, planning, and
   automation") → **Add a domain** → `ioncodex.org` → **Add domain**.
2. GitHub shows a TXT record. Add it in GoDaddy's DNS: name
   `_github-pages-challenge-alexandruavram01-spec`, value as shown.
3. Back on GitHub, click **Verify**. If it fails, DNS may not have updated yet; wait and
   use **⋯ → Continue verifying**.
4. Keep that TXT record for good. Removing it un-verifies the domain.

### 2. Create the repository and push

1. Create a new repository under `alexandruavram01-spec`, **public** (GitHub Pages on the
   free plan needs a public repository), with no README, licence or .gitignore, so it
   starts empty.
2. In this folder:

   ```
   git init -b main
   git config user.name "Alex Avram"
   git config user.email alexandru.avram01@gmail.com
   git config core.sshCommand "ssh -i C:/src/RSA_Git -o IdentitiesOnly=yes"
   git add .
   git commit -m "First version of the IONCODEX website"
   git remote add origin git@github.com:alexandruavram01-spec/<repository>.git
   git push -u origin main
   ```

### 3. Turn on GitHub Pages

1. In the repository: **Settings** → **Pages**.
2. Source: **Deploy from a branch**. Branch: `main`, folder `/ (root)`. **Save**.
3. Custom domain: `ioncodex.org` (it may already be filled in from the `CNAME` file).
   **Save**.

### 4. DNS records at GoDaddy

The domain's DNS is managed at GoDaddy: Domain Portfolio → `ioncodex.org` → **DNS**.
Change only the records for `@` (the bare domain) and `www`. **Leave everything else
alone**, in particular the MX record, the TXT records (`NETORGFT…onmicrosoft.com` and
`v=spf1 …`) and any CNAMEs such as `autodiscover`: they belong to the Microsoft 365 email
set up through GoDaddy.

1. Remove the existing A records on `@` and `www` (in October 2026 both pointed to
   `170.130.165.132`). GoDaddy can't change a record's type, so `www` has to be deleted
   before its CNAME can be added.
2. Add four A records on `@`:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
3. Optional, for IPv6: four AAAA records on `@`:
   `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`,
   `2606:50c0:8003::153`.
4. Add a CNAME record: `www` → `alexandruavram01-spec.github.io` (no repository name).
5. Never add a wildcard record (`*`); it lets others take over subdomains.

DNS can take up to 24 hours, usually much less.

### 5. HTTPS

1. Back in the repository's **Settings** → **Pages**, wait until the DNS check passes and
   the certificate is issued (can take up to an hour after DNS works).
2. Tick **Enforce HTTPS**.
3. Check `https://ioncodex.org` opens the site, and `https://www.ioncodex.org` redirects
   to it.

If the site is ever taken down, remove the `@` and `www` DNS records at the same time, so
the domain doesn't keep pointing at GitHub with nothing behind it.
