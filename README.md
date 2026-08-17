# mercurygram.org

Source for [mercurygram.org](https://mercurygram.org), the landing page for
the [Mercurygram](https://github.com/Mercurygram) project: privacy and security focused forks of
Telegram for Android ([Mercurygram](https://github.com/Mercurygram/Mercurygram)) and Desktop
([mdesktop](https://github.com/Mercurygram/mdesktop)).

Static site built with [Zola](https://www.getzola.org/) 0.23 or later, which needs Tera v2
templates (components, no macros). No JavaScript, self-hosted fonts.

## Build

```sh
zola serve   # live preview at http://127.0.0.1:1111
zola build   # output to ./public
zola check   # validate links
```

## Deploy

Pushing to `master` triggers `.github/workflows/build-action.yaml`, which builds with the Zola
release binary and publishes through the official GitHub Pages actions (Pages source: GitHub
Actions). Org policy allows only github-owned actions plus a small allowlist, all SHA-pinned, so
no third-party deploy action is used.

`bump-version.yaml` receives `repository_dispatch` events from the Android and Desktop release CIs,
updates the version in `config.toml`, and re-runs the deploy.

## Layout

- `config.toml` — site config and all download URLs / version strings (`[extra]`)
- `templates/`: Tera templates. `index.html` (landing page), `page.html` (content pages) and
  `section.html` (section index pages) are built from the components in `components.html`
  (head, mark, nav, footer) and `content.html` (the landing page sections). Components are
  hygienic, so each one takes the site config as a `cfg` argument.
- `content/`: Markdown. `features/` is a section whose `_index.md` renders through
  `section.html` and lists its pages as cards, one per client (`android.md`, `desktop.md`),
  each rendered through `page.html`. Adding a client is one more file, no template change.
- `sass/` — styles, compiled natively by Zola to `/main.css`
- `static/` — fonts, logo, `CNAME`

## License

Site code is MIT. The applications themselves are licensed separately (Android GPLv2, Desktop
GPLv3 with OpenSSL exception).
