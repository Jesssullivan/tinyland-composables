# Changelog

## 1.0.0 (2026-10-09)

Breaking: the package moves to the estate RU1 stack and to Bazel-only
distribution. The runtime API is unchanged: the same exports, with the same
signatures, as 0.2.4.

### Changed

- Peer `svelte` is now exactly `5.57.2` (was `>=5.0.0`), the estate pin.
- The optional `runed` peer is removed. No module in this package imports it.
- Built with TypeScript 7.0.2 (`tsc`) instead of `svelte-package`.
  `foo.svelte.ts` still emits `foo.svelte.js` with its runes left for your
  Svelte compiler, plus `foo.svelte.d.ts` and a declaration map. Type checking
  is `tsc --noEmit` with the svelte rune types; there are no `.svelte`
  components, so `svelte-check` adds nothing here.
- Toolchain: typescript 7.0.2, vite 8.3.3 and vitest 5.0.3 (exact); happy-dom
  20; node >= 22.12; aspect_rules_ts 3.10.1 with TypeScript 7.0.2 in Bazel.
- Distribution is Bazel only. The package is `private` and is no longer
  published to npmjs or GitHub Packages; the publish workflow is removed.
  Releases are signed git tags plus an entry in xoxd-ai/bazel-registry.

### Migration

1. Replace any npm dependency on `@tummycrypt/tinyland-composables` with the
   Bazel module:

   ```starlark
   bazel_dep(name = "tummycrypt_tinyland_composables", version = "1.0.0")
   ```

   and link `@tummycrypt_tinyland_composables//:pkg` into your app's
   `node_modules` with `npm_link_package`.
2. Use Svelte 5.57.2 in the consuming app.
3. If you relied on the `runed` optional peer being declared here, add `runed`
   to your own dependencies.
4. Refresh `MODULE.bazel.lock`. Root modules that take this version get
   aspect_rules_ts 3.10.1 through MVS and should pin TypeScript 7.0.2.

## 0.2.4 and earlier

Published to npm as `@tummycrypt/tinyland-composables`. Those versions stay
available but are superseded by the Bazel module.
