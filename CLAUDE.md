Read AGENTS.md before changing anything.

## Merging

Merge your own pull requests without asking. Once every CI check on the
PR's current head is green and it has no merge conflict, mark it ready
for review and merge it with a merge commit (never squash or rebase: an
app repository is often synced to Lovable, and rewritten history loses
its project history). If CI is red, fix it first; never merge a failing
PR. Then tell the user it was merged.

## Website

Every Mac app gets its own download website, made the same way each time:

- **Its own Lovable project and GitHub repo**, never inside the app's repo.
  Create it in the Lovable workspace "006", named `<app>-site` (for
  example `captainapp-site`). The user connects it to GitHub from the
  Lovable editor.
- **When Lovable can't do the work** (the workspace is out of credits, or
  any other refusal): don't wait for credits. Edit the site through its
  GitHub repo instead: clone it, make the change, check it locally (build,
  tests, a look at the page), open a PR, merge it per the merging rule, then
  republish with Lovable's deploy (publishing needs no credits) and confirm
  the live page. If the site isn't connected to GitHub yet, ask the user
  once to connect it from the Lovable editor (Project settings, GitHub),
  then carry on as above.
- **Same shape as the Camu website** (Lovable project
  `2795037d-c483-4c5c-954c-ab2fbbe5d56f`, camu.cc): fixed nav that blurs on
  scroll, hero with Download and "How to install", a features grid, two
  showcase rows, numbered install steps, a final call to action, footer.
- **The app's own brand:** its logo and app icon (favicon, share image), its
  palette and copy.
- **Real screenshots of the app**, never drawn imitations of its window.
  Capture them from the app's interface at 2x (2560x1600 for a 1280x800
  window), e.g. `npm run dev:web` with `?demo` sample data, with the macOS
  window buttons drawn in. Retake them whenever the app's look changes.
- **A `/download` route** that streams the first `.dmg` of the app repo's
  latest GitHub release. No analytics or tracking unless the user asks.
- **One `SITE_URL` constant** for the domain (canonical, share tags,
  robots.txt, sitemap.xml). Ask the user for the domain; never guess one.
- **The Camu website's footer** (`SiteFooter` in its
  `src/components/site/chrome.tsx`): the app's wordmark and a one-line
  description, a few columns of links to the site's own pages, and a
  bottom bar reading "© <current year, computed> <App name>".
- **Never mention or visibly link to GitHub, and never say who made the
  app**: no "Source", "Releases" or "Made by" anywhere. The GitHub address
  lives only inside the `/download` server handler. If no `.dmg` is found,
  it answers "Download unavailable, please try again shortly." instead of
  sending people to GitHub.

Once the site exists, note its Lovable project id at the end of this
section in the app's own CLAUDE.md.
