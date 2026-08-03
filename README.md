# Pagelove AMA template

A single-file "Ask Me Anything" page. No backend, no build step — the whole
app is `index.html`, deployed as one file to a [Pagelove](https://pagelove.com)
host.

Live example: https://ease-snail-7122.onpagelove.com/

## What it does

- Public visitors can submit a question (`POST` into `#questions`).
- The shape of what they can submit is enforced server-side by a
  `ShapeConstraint` — they can't inject an `answer`, a `script` tag, or
  anything outside `<li class="question"><p class="question-text">…</p>
  <p class="question-by">…</p></li>`.
- You answer questions by editing the file directly and redeploying — there's
  no public write path to the "answered" section.

## Make it yours

1. Fork this repo.
2. Edit the block marked `PERSONALIZE THIS` in `index.html` (name, bio, and
   the example Q&A under "Previously answered").
3. Get a Pagelove console API key (`pk_…`) from your console's credentials
   page.
4. Find your host's `webdav-url` on `https://config.onpagelove.com/console/index.html`,
   then deploy:

   ```bash
   curl -X PUT "<your-webdav-url>index.html" \
     -H "Authorization: Bearer pk_..." \
     -H "Content-Type: text/html" \
     --data-binary @index.html
   ```

That's it — no database, no API layer, no server code.
