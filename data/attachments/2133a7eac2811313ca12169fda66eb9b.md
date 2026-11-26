# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/login-hospital-code.spec.ts >> a nurse names her hospital first, then signs in with its password
- Location: e2e/journeys/login-hospital-code.spec.ts:16:1

# Error details

```
Error: GET /api/auth/sign-in-options?code=default → 429
body: {"error":"too_many_requests","detail":"Too many login attempts. Please try again later."}
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
          - paragraph [ref=e51]: Move 30 minutes a day
          - paragraph [ref=e52]: At least 150 minutes of moderate activity a week lowers heart-disease, diabetes and stroke risk.
          - paragraph [ref=e53]: "Source: World Health Organization"
        - generic [ref=e54]:
          - generic [ref=e55]:
            - button "Pause health tips" [ref=e56] [cursor=pointer]
            - tablist "Choose a health tip" [ref=e61]:
              - tab "Tip 1 of 6" [selected] [ref=e62] [cursor=pointer]
              - tab "Tip 2 of 6" [ref=e63] [cursor=pointer]
              - tab "Tip 3 of 6" [ref=e64] [cursor=pointer]
              - tab "Tip 4 of 6" [ref=e65] [cursor=pointer]
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
          - textbox "Hospital code" [active] [ref=e92]: default
        - alert [ref=e93]:
          - generic [ref=e94]: Couldn't reach the hospital server. This is a connection problem, not a wrong code — try again in a moment.
        - button "Continue" [ref=e101] [cursor=pointer]
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
  131 |   const me = await request.get(`${E2E_BACKEND_URL}/api/auth/me`, {
  132 |     headers: { "x-csrf-token": csrf, cookie: cookieHeader },
  133 |   });
  134 |   if (!me.ok()) return freshSetupAdmin(request);
  135 |   const body = await me.json().catch(() => ({}));
  136 |   const userId = body.user?.id ?? body.id ?? "";
  137 | 
  138 |   // storageState holds the session global-setup logged in with, so the
  139 |   // password is recoverable from the identity manifest — which matters because
  140 |   // high-risk actions need a step-up, and a context that cannot re-prove
  141 |   // identity cannot sign a prescription.
  142 |   //
  143 |   // Only when the recovered user *is* that identity: step-up verifies the
  144 |   // password against the current user, so attaching somebody else's would turn
  145 |   // a working session into a confusing 401.
  146 |   let password: string | undefined;
  147 |   try {
  148 |     const admin = getE2EIdentity("super_admin");
  149 |     if (admin.id && admin.id === userId) password = admin.password;
  150 |   } catch {
  151 |     // No manifest (a spec run outside the usual setup). Leave it unset and let
  152 |     // any step-up refusal surface honestly.
  153 |   }
  154 | 
  155 |   return {
  156 |     csrfToken: csrf,
  157 |     cookieHeader,
  158 |     request,
  159 |     userId,
  160 |     tenantId: body.user?.tenant_id ?? body.tenant_id ?? "",
  161 |     password,
  162 |   };
  163 | }
  164 | 
  165 | /** A test needs at least this much session left, or it signs in again. */
  166 | const SESSION_MARGIN_MS = 6 * 60_000;
  167 | /** The server's access-token lifetime (`medbrains-auth`, 15 minutes). */
  168 | const ACCESS_TOKEN_LIFETIME_MS = 15 * 60_000;
  169 | 
  170 | /** When global setup saved the stored session; long ago when there is none. */
  171 | function storedSessionWrittenAt(): number {
  172 |   try {
  173 |     return statSync(authStatePath).mtimeMs;
  174 |   } catch {
  175 |     return 0;
  176 |   }
  177 | }
  178 | 
  179 | /** The setup admin, signed in again for a full session. */
  180 | async function freshSetupAdmin(request: APIRequestContext): Promise<AuthContext> {
  181 |   let identity: ReturnType<typeof getE2EIdentity>;
  182 |   try {
  183 |     identity = getE2EIdentity("super_admin");
  184 |   } catch {
  185 |     return loginAsAdmin(request);
  186 |   }
  187 |   const session = await login(request, identity.username, identity.password);
  188 |   return {
  189 |     csrfToken: session.csrf,
  190 |     cookieHeader: session.cookieHeader,
  191 |     request,
  192 |     userId: session.user?.id ?? "",
  193 |     tenantId: session.user?.tenant_id ?? "",
  194 |     password: identity.password,
  195 |   };
  196 | }
  197 | 
  198 | function statusOk(status: number, expected?: number | number[]): boolean {
  199 |   if (expected === undefined) return status >= 200 && status < 300;
  200 |   if (Array.isArray(expected)) return expected.includes(status);
  201 |   return status === expected;
  202 | }
  203 | 
  204 | /**
  205 |  * Make an authenticated REST call. On non-OK status, log diagnostics
  206 |  * and throw an Error with method + path + status + body.
  207 |  */
  208 | export async function api<T = unknown>(
  209 |   ctx: AuthContext,
  210 |   method: ApiMethod,
  211 |   path: string,
  212 |   body?: unknown,
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
> 231 |   throw new Error(
      |         ^ Error: GET /api/auth/sign-in-options?code=default → 429
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
  313 |   const resp = await ctx.request.fetch(`${E2E_BACKEND_URL}${path}`, {
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
```