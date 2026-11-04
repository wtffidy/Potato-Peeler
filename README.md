# 🥔 Potato Peeler

A deliberately over-engineered 3D potato-peeling verification page. Perfectly reasonable security technology.

## GitHub Pages

The site is deployed automatically from `main` by the **Deploy Potato Peeler to GitHub Pages** workflow.

Once the first deployment succeeds:

- **Website:** https://wtffidy.github.io/Potato-Peeler/
- **Direct HTML:** https://wtffidy.github.io/Potato-Peeler/3d_potato_peeling_verification.html

If the first deployment does not start, check **Settings → Pages** and set **Build and deployment → Source** to **GitHub Actions**, then rerun the workflow.

## Embedding / verification callback

When the user reaches 100%, the page sends this message to its parent window:

```js
{ status: "HUMAN_VERIFIED", score: 100 }
```

Listen for it from an embedding page:

```js
window.addEventListener("message", (event) => {
  if (event.origin !== "https://wtffidy.github.io") return;
  if (event.data?.status !== "HUMAN_VERIFIED") return;

  console.log("Potato peeling complete:", event.data.score);
});
```

The page posts to `window.parent`; when opened as a top-level page there is no separate parent application to receive the callback. The completion modal still works normally.

## Notes

- Three.js and Tailwind are loaded from public CDNs.
- No backend, account, or server is required.
- The original `3d_potato_peeling_verification.html` is retained; `index.html` is the Pages entry point.
