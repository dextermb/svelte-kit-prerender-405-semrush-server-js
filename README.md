# Pre-render blocking cURL when using `+server.js`

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
* Execute cURL command

#### Preparing the website

```
echo 'export const prerender = true' > 'src/routes/+server.js'
pnpm build
pnpm preview
```

#### Testing the website

```
curl http://localhost:4173
```
