# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/message-simulator.spec.ts >> message simulator — the patient's phone >> a patient called from the console receives the token SMS
- Location: e2e/journeys/message-simulator.spec.ts:16:3

# Error details

```
Test timeout of 30000ms exceeded.
```

```
Error: apiRequestContext.fetch: Target page, context or browser has been closed
```

# Page snapshot

```yaml
- generic [ref=e3]:
  - complementary "About MedBrains" [ref=e4]:
    - generic [ref=e5]:
      - paragraph [ref=e7]: MedBrains
      - generic [ref=e8]:
        - paragraph [ref=e9]: For Indian hospitals · NABH · ABDM
        - heading "The whole hospital. One system." [level=2] [ref=e10]:
          - text: The whole hospital.
          - generic [ref=e11]: One system.
        - paragraph [ref=e12]: From the front desk to the discharge summary — OPD, wards, lab, pharmacy and billing, with every rule built in.
      - list [ref=e13]:
        - listitem [ref=e14]:
          - generic [ref=e20]:
            - paragraph [ref=e21]: One patient, one record
            - paragraph [ref=e22]: A UHID at the front desk and the same chart in OPD, wards, lab, pharmacy and billing.
        - listitem [ref=e23]:
          - generic [ref=e28]:
            - paragraph [ref=e29]: The rules are in the screens
            - paragraph [ref=e30]: NABH workflows, Schedule H and NDPS at the counter, and every access on record.
        - listitem [ref=e31]:
          - generic [ref=e35]:
            - paragraph [ref=e36]: Web and native apps
            - paragraph [ref=e37]: Staff and patient apps for iPhone and Android, token boards for the waiting room.
        - listitem [ref=e38]:
          - generic [ref=e44]:
            - paragraph [ref=e45]: Your hospital's data, sealed
            - paragraph [ref=e46]: Each hospital is isolated in the database itself, and its data is kept in India.
      - region "Health tips" [ref=e48]:
        - generic [ref=e49]:
          - paragraph [ref=e50]: Health tip
          - paragraph [ref=e51]: Wash hands for 20 seconds
          - paragraph [ref=e52]: Hand hygiene is the single most effective way to prevent the spread of infection.
          - paragraph [ref=e53]: "Source: CDC"
        - generic [ref=e54]:
          - generic [ref=e55]:
            - button "Pause health tips" [ref=e56] [cursor=pointer]
            - tablist "Choose a health tip" [ref=e61]:
              - tab "Tip 1 of 6" [ref=e62] [cursor=pointer]
              - tab "Tip 2 of 6" [ref=e63] [cursor=pointer]
              - tab "Tip 3 of 6" [ref=e64] [cursor=pointer]
              - tab "Tip 4 of 6" [selected] [ref=e65] [cursor=pointer]
              - tab "Tip 5 of 6" [ref=e66] [cursor=pointer]
              - tab "Tip 6 of 6" [ref=e67] [cursor=pointer]
          - generic [ref=e68]:
            - button "Previous tip" [ref=e69] [cursor=pointer]
            - button "Next tip" [ref=e73] [cursor=pointer]
  - main [ref=e77]:
    - generic [ref=e78]:
      - generic [ref=e79]:
        - heading "Sign in" [level=1] [ref=e81]
        - paragraph [ref=e82]: Start with your hospital
      - generic [ref=e83]:
        - generic [ref=e84]:
          - generic [ref=e85]: Hospital code *
          - paragraph [ref=e86]: The code your hospital gave you, e.g. CITYHOSP.
          - textbox "Hospital code" [active] [ref=e92]
        - alert [ref=e93]:
          - generic [ref=e94]: Couldn't reach the hospital server. This is a connection problem, not a wrong code — try again in a moment.
        - button "Continue" [disabled] [ref=e101]
      - generic [ref=e104]:
        - button "Dev credentials" [ref=e106] [cursor=pointer]
        - generic [ref=e107]: MedBrains v3.33.2
        - paragraph [ref=e108]:
          - link "Terms" [ref=e109] [cursor=pointer]:
            - /url: /terms
          - text: ·
          - link "Privacy" [ref=e110] [cursor=pointer]:
            - /url: /privacy
```

# Test source

```ts
  213 |   options: ApiCallOptions = {},
  214 | ): Promise<T> {
  215 |   const result = await tryApi<T>(ctx, method, path, body, options);
  216 |   if (result.ok) return result.data;
  217 | 
  218 |   if (options.variants && options.variants.length > 0) {
  219 |     for (const variant of options.variants) {
  220 |       const r = await tryApi<T>(ctx, method, variant, body, options);
  221 |       if (r.ok) {
  222 |         // eslint-disable-next-line no-console
  223 |         console.warn(
  224 |           `[e2e/api] ${method} ${path} failed; variant ${variant} succeeded — update the spec`,
  225 |         );
  226 |         return r.data;
  227 |       }
  228 |     }
  229 |   }
  230 | 
  231 |   throw new Error(
  232 |     `${method} ${path} → ${result.status}\nbody: ${result.bodyText}` +
  233 |       (options.variants
  234 |         ? `\nvariants tried: ${options.variants.join(", ")}`
  235 |         : "") +
  236 |       (result.status === 401 ? `\n${describeSession(ctx)}` : ""),
  237 |   );
  238 | }
  239 | 
  240 | /**
  241 |  * What the refused session was, for a 401: the access token's issue and
  242 |  * expiry times, user and permission version, against the time of the call.
  243 |  * The body only says "unauthorized"; this tells an expired token from a
  244 |  * revoked one.
  245 |  */
  246 | function describeSession(ctx: AuthContext): string {
  247 |   const token = /(?:^|;\s*)access_token=([^;]+)/.exec(ctx.cookieHeader)?.[1];
  248 |   if (!token) return `session: no access_token cookie sent (at ${new Date().toISOString()})`;
  249 |   try {
  250 |     const claims = JSON.parse(Buffer.from(token.split(".")[1] ?? "", "base64url").toString("utf8"));
  251 |     const at = (seconds: number) => new Date(seconds * 1000).toISOString();
  252 |     return `session: iat=${at(claims.iat)} exp=${at(claims.exp)} now=${new Date().toISOString()} sub=${claims.sub} perm_version=${claims.perm_version}`;
  253 |   } catch {
  254 |     return "session: access_token is not a readable JWT";
  255 |   }
  256 | }
  257 | 
  258 | /** Make an unauthenticated public API call. */
  259 | export async function publicApi<T = unknown>(
  260 |   request: APIRequestContext,
  261 |   method: ApiMethod,
  262 |   path: string,
  263 |   body?: unknown,
  264 |   options: PublicApiOptions = {},
  265 | ): Promise<T> {
  266 |   const headers: Record<string, string> = {};
  267 |   if (body !== undefined) headers["content-type"] = "application/json";
  268 | 
  269 |   const resp = await request.fetch(`${E2E_BACKEND_URL}${path}`, {
  270 |     method,
  271 |     headers,
  272 |     data: body !== undefined ? JSON.stringify(body) : undefined,
  273 |   });
  274 | 
  275 |   if (!statusOk(resp.status(), options.expectStatus)) {
  276 |     throw new Error(
  277 |       `${method} ${path} → ${resp.status()}\nbody: ${await resp.text()}`,
  278 |     );
  279 |   }
  280 |   if (resp.status() === 204) return undefined as T;
  281 |   const text = await resp.text();
  282 |   if (!text) return undefined as T;
  283 |   try {
  284 |     return JSON.parse(text) as T;
  285 |   } catch {
  286 |     return text as unknown as T;
  287 |   }
  288 | }
  289 | 
  290 | /** Alias for unauthenticated machine-to-machine integration endpoints. */
  291 | export async function externalApi<T = unknown>(
  292 |   request: APIRequestContext,
  293 |   method: ApiMethod,
  294 |   path: string,
  295 |   body?: unknown,
  296 |   options: PublicApiOptions = {},
  297 | ): Promise<T> {
  298 |   return publicApi<T>(request, method, path, body, options);
  299 | }
  300 | 
  301 | async function tryApi<T>(
  302 |   ctx: AuthContext,
  303 |   method: string,
  304 |   path: string,
  305 |   body: unknown,
  306 |   options: ApiCallOptions,
  307 | ): Promise<ApiResult<T>> {
  308 |   const headers: Record<string, string> = {};
  309 |   if (ctx.cookieHeader) headers.cookie = ctx.cookieHeader;
  310 |   if (!options.skipCsrf) headers["x-csrf-token"] = ctx.csrfToken;
  311 |   if (body !== undefined) headers["content-type"] = "application/json";
  312 | 
> 313 |   const resp = await ctx.request.fetch(`${E2E_BACKEND_URL}${path}`, {
      |                                  ^ Error: apiRequestContext.fetch: Target page, context or browser has been closed
  314 |     method,
  315 |     headers,
  316 |     data: body !== undefined ? JSON.stringify(body) : undefined,
  317 |   });
  318 | 
  319 |   if (!statusOk(resp.status(), options.expectStatus)) {
  320 |     const bodyText = await resp.text();
  321 |     return { ok: false, status: resp.status(), bodyText };
  322 |   }
  323 |   if (resp.status() === 204) return { ok: true, data: undefined as T };
  324 |   const text = await resp.text();
  325 |   if (!text) return { ok: true, data: undefined as T };
  326 |   try {
  327 |     return { ok: true, data: JSON.parse(text) as T };
  328 |   } catch {
  329 |     return { ok: true, data: text as unknown as T };
  330 |   }
  331 | }
  332 | 
  333 | function cookieHeaderFromResponse(resp: {
  334 |   headersArray: () => Array<{ name: string; value: string }>;
  335 | }): string {
  336 |   return resp
  337 |     .headersArray()
  338 |     .filter((h) => h.name.toLowerCase() === "set-cookie")
  339 |     .map((h) => h.value.split(";")[0])
  340 |     .filter(Boolean)
  341 |     .join("; ");
  342 | }
  343 | 
  344 | function cookieHeaderFromStorageState(cookies: Array<{ name: string; value: string }>): string {
  345 |   return cookies
  346 |     .map((cookie) => `${cookie.name}=${cookie.value}`)
  347 |     .filter(Boolean)
  348 |     .join("; ");
  349 | }
  350 | 
  351 | /** Build a query string from an object, dropping undefined/null. */
  352 | export function qs(params: Record<string, unknown>): string {
  353 |   const search = new URLSearchParams();
  354 |   for (const [k, v] of Object.entries(params)) {
  355 |     if (v === undefined || v === null) continue;
  356 |     search.set(k, String(v));
  357 |   }
  358 |   const s = search.toString();
  359 |   return s ? `?${s}` : "";
  360 | }
  361 | 
  362 | // ─── Async effects ───────────────────────────────────────────────────
  363 | //
  364 | // Pipelines run after the request returns: the handler writes an outbox row,
  365 | // the worker polls every 2 s and hands the event to the subscriber, which
  366 | // opens its own transaction. An effect in another module therefore appears
  367 | // 0–3 s later, and a test that reads it immediately learns nothing.
  368 | 
  369 | /**
  370 |  * Re-read until `pred` holds. Throws with the last value when it never does,
  371 |  * and says the one thing worth checking first when nothing ever arrives.
  372 |  */
  373 | export async function pollUntil<T>(
  374 |   fn: () => Promise<T>,
  375 |   pred: (value: T) => boolean,
  376 |   opts: { timeoutMs?: number; everyMs?: number; label?: string } = {},
  377 | ): Promise<T> {
  378 |   const timeoutMs = opts.timeoutMs ?? 20_000;
  379 |   const everyMs = opts.everyMs ?? 1_000;
  380 |   const deadline = Date.now() + timeoutMs;
  381 |   let last: T | undefined;
  382 |   for (;;) {
  383 |     last = await fn();
  384 |     if (pred(last)) return last;
  385 |     if (Date.now() >= deadline) break;
  386 |     await new Promise((r) => setTimeout(r, everyMs));
  387 |   }
  388 |   throw new Error(
  389 |     `${opts.label ?? "effect"}: not observed within ${timeoutMs}ms — if nothing ever arrives, ` +
  390 |       `check the outbox worker is running (MEDBRAINS_DISABLE_OUTBOX_WORKER unset). Last value: ` +
  391 |       JSON.stringify(last).slice(0, 800),
  392 |   );
  393 | }
  394 | 
  395 | /**
  396 |  * The negative half: keep reading for `forMs` (three worker cycles by default)
  397 |  * and pass only if `pred` NEVER held. A negative that reads once proves
  398 |  * nothing about an effect that arrives two seconds later.
  399 |  */
  400 | export async function expectAbsent<T>(
  401 |   fn: () => Promise<T>,
  402 |   pred: (value: T) => boolean,
  403 |   opts: { forMs?: number; everyMs?: number; label?: string } = {},
  404 | ): Promise<void> {
  405 |   const forMs = opts.forMs ?? 6_000;
  406 |   const everyMs = opts.everyMs ?? 1_000;
  407 |   const deadline = Date.now() + forMs;
  408 |   for (;;) {
  409 |     const value = await fn();
  410 |     if (pred(value)) {
  411 |       throw new Error(
  412 |         `${opts.label ?? "effect"}: must not happen, but it did: ${JSON.stringify(value).slice(0, 800)}`,
  413 |       );
```