# @tummycrypt/tinyland-composables

Svelte 5 rune-based composables: lifecycle cleanup, bulk selection, color
calculations, consent state, draft persistence, an editor operation queue, a
viewport text scanner and Web Worker helpers.

## Install (Bazel only)

This package is distributed as a Bazel module from
[xoxd-ai/bazel-registry](https://github.com/xoxd-ai/bazel-registry). It is not
published to npm.

```starlark
# MODULE.bazel
bazel_dep(name = "tummycrypt_tinyland_composables", version = "1.0.0")
```

Link `@tummycrypt_tinyland_composables//:pkg` into your app's `node_modules`
with rules_js `npm_link_package`, then import it as usual:

```ts
import { useLifecycle, useBulkSelection } from '@tummycrypt/tinyland-composables';
```

Peer dependency: `svelte` 5.57.2. The `.svelte.js` modules keep their runes, so
your app's Svelte compiler (vite-plugin-svelte) must process them.

## Develop

```bash
pnpm install
pnpm typecheck   # tsc 7.0.2 --noEmit
pnpm test        # vitest 5
pnpm build       # tsc -> dist/
bazel build //:pkg && bazel test //...
```

## Release

Signed annotated tag `vX.Y.Z`, a GitHub release, and a registry PR whose
`source.json` integrity is computed from the real tag archive. See
[CHANGELOG.md](CHANGELOG.md).

## License

Zlib AND LicenseRef-Tinyland-Proprietary. See [LICENSE](LICENSE).
