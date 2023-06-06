# Pre-render blocking SEMRush when using `+server.js`

### Description

This project was created using `pnpm create svelte`.

When using `prerender` within a `+server.js` file and attempting to execute a SEMRush cURL command a `405 Method not allowed` is returned, however when using `prerender` with a `+page.server.js` file a `200 OK` is returned (which is expected).

#### Expected

A `200 OK` response should be returned even with `+server.js`.

#### Actual

A `405 Method not allowed` is currently returned when using `+server.js`.

---

### Set up

Reproducing the bug seems to be fairly easy:
* Write `export const prerender = true` to `src/routes/+server.js`
* Build website
* Preview website
* Tunnel website
* Execute SEMRush cURL command

#### Preparing the website

```
echo 'export const prerender = true' > 'src/routes/+server.js'
pnpm build
pnpm preview
```

#### Testing the website

1. Create a tunnel `ngrok http 4173`
2. Execute cURL command (replace `$NGROK_URL`)
```
curl -i -sS -L --proto-redir -all,http,https --max-time 5 -A 'Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; SiteAuditBot/0.97; +http://www.semrush.com/bot.html)' $NGROK_URL
```
