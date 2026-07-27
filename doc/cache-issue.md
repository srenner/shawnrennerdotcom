## Astro: stale content-collection cache showing deleted posts

**Symptom:** You deleted content files, but `astro build` or `astro dev` still generates pages for them, often failing with `UnknownContentCollectionError`.

**Cause:** Astro caches collection data in two separate places. Clearing only one isn't enough.

**Fix:**
```bash
rm -rf .astro dist node_modules/.astro node_modules/.vite
npx astro build
```

**If that's not enough**, full reinstall:
```bash
rm -rf node_modules package-lock.json .astro dist
npm install
npx astro build
```

**Quick sanity checks if the problem persists:**
```bash
# confirm no stray dev server is running and re-writing cache
ps aux | grep astro

# confirm the content directory is actually empty
find src/content -type f

# confirm only one collection config exists (not both old + new style)
find . -not -path "./node_modules/*" -iname "content.config.ts"
find . -not -path "./node_modules/*" -path "*/content/config.ts"
```

**Key takeaway:** `.astro/data-store.json` and `node_modules/.astro/data-store.json` are both caches of your content collections. Deleting content files doesn't auto-clear them — you have to wipe both directories manually.