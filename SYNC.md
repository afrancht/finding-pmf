# Sync notes

## Source of truth to track for audits

The canonical published version of `README.md` lives on Substack:

**https://alexfranchtapia.substack.com/p/a-guide-to-find-product-market-fit**

`README.md` in this repo mirrors that post. Every time the post is edited, the change
should be pulled back into `README.md` and committed, so git history is the audit trail
of how the guide evolved.

## How to check for changes

The public page URL can serve a cached version. Use the JSON API instead, which returns
the current content:

```bash
curl -sL "https://alexfranchtapia.substack.com/api/v1/posts/a-guide-to-find-product-market-fit" -o post.json
```

Useful fields: `title`, `subtitle`, `updated_at`, `body_html`. Convert the body to
markdown to diff it against `README.md`:

```bash
python3 -c "import json;open('body.html','w').write(json.load(open('post.json'))['body_html'])"
pandoc body.html -f html -t gfm --wrap=none -o body.md
```

## Known differences from the Substack version

These are deliberate, do not treat them as drift:

- The subscribe widget at the end of the post is dropped.
- YouTube embeds become clickable thumbnail links, since GitHub cannot render iframes.
- Images point at the Substack CDN rather than files committed here.
- Post ID for reference: 214007030.

## Sync history

- 2026-09-03: synced with the published version (subtitle updated, second image removed).
