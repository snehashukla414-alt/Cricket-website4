# Cloudflare Worker setup

1. Create a Worker and paste `worker.js`.
2. Add secret `OPENCRICKET_KEY`.
3. Optional: add `OPENAI_API_KEY`, `GEMINI_API_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_CSE_KEY`, `GOOGLE_CSE_CX`.
4. Restrict `ALLOWED_ORIGINS` in source to your GitHub Pages origin and redeploy.
5. Optional persistent cache: create a Workers KV namespace, bind it to the Worker with variable name `CRICKET_CACHE`, then redeploy.
6. Test `https://YOUR-WORKER.workers.dev/api/health`; then paste the Worker base URL ending `/api` into the site's Data Setup panel and click Test Connection.

The Worker proxies OpenCricket API v1 and caches successful JSON responses in KV when configured. Live responses have a short cache window; fixtures, match lists, scorecards and player profiles use longer windows. On upstream errors, cached data is returned with `_cache.stale=true`.

Keep every API key in Worker secrets. Never put keys in GitHub files or browser code. Add rate limiting before sharing a heavily used public site.
