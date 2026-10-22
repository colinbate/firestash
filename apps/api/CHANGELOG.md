# @npflared/api

## 0.2.0

### Minor Changes

- 7ff44da: Add the admin API under `/_/admin/api/*`, guarded by the admin authentication provider: paginated package listing with search, package details with dist-tags and published versions, per-version manifests (readme and dependencies), and token listing, creation, retrieval and revocation without token scopes.
- 6621724: Add admin authentication through Cloudflare Access. Every request to `/_/admin` (and below) must carry a valid Access JWT, which is validated server-side against the team's signing keys (`CF_ACCESS_TEAM_DOMAIN`, `CF_ACCESS_AUD`); the admin area stays closed until these are configured. `GET /_/admin/api/me` returns the authenticated administrator. Registry routes are unaffected and keep using registry tokens.
- 46abf0e: Add the admin UI, a Svelte 5 application served by the worker at `/_/admin` behind admin authentication: browse published packages (versions, dist-tags, readme, dependencies, install command) and manage registry tokens (create with scopes, reveal once, revoke). The UI lives in the same Vite project as the worker, through the Cloudflare Vite plugin: `vite dev` serves both on one origin, `vite build` emits them together and `wrangler deploy` picks up the result. A `local` admin authentication provider, which only trusts requests addressed to `localhost`, makes the admin area usable in development.
- b96e4a2: Make deployments account-agnostic: the worker name, custom domain, D1 database, R2 bucket and Cloudflare Access values are applied to the worker configuration at build time from the environment (Workers Builds variables or a local `.env.local`, see `.env.example`), so the same repository deploys into any Cloudflare account. `pnpm deploy` builds, applies the D1 migrations and deploys; `pnpm release` does the last two for Git-connected builds.
- 9004e6d: Store tokens as SHA-256 hashes instead of plaintext. Tokens are now generated with 256 bits of entropy (prefixed `fst_`), the plaintext is only returned once at creation, and tokens are listed, retrieved and revoked by a stable `id` (`/-/npm/v1/tokens/token/:id`) instead of by their secret. Existing plaintext tokens keep working and are hashed on first use; `pnpm migrate-tokens:prod` hashes any that remain.

## 0.1.0

### Minor Changes

- 4c27e54: Separator logic into dedicated services + rework validator and routing structure + open api documentation generation

## 0.0.5

### Patch Changes

- 9093b40: Bump dependencies

## 0.0.4

### Patch Changes

- f302768: Bump dependencies

## 0.0.3

### Patch Changes

- 171a0f0: Bump dependencies

## 0.0.2

### Patch Changes

- 361fca4: Bump dependencies

## 0.0.1

### Patch Changes

- 316bfd3: Initial release
