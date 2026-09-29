# R2 dependency validation

Verified by Codex on 2026-09-29. R0 means the resolved version in the 2026-09-28 audit; R2 means that audit's candidate version. R1 is not used. Versions below are lockfile versions, not manifest lower bounds. Only direct dependencies are listed.

## Updates retained at R0

| Package | Retained R0 | R2 candidate | Reason |
|---|---|---|---|
| `@vitest/browser-playwright` | 4.0.16 | 5.0.2 | Vitest 5 is outside Storybook addon-vitest 10.6.0 peer support; retain the shared Vitest 4 family. |
| `typescript` | 5.9.3 | 7.0.2 | TypeScript 7 removes createLanguageService used by prettier-plugin-organize-imports 4.3.0, silently disabling import organization. |
| `vitest` | 4.0.16 | 5.0.2 | Vitest 5 is outside Storybook addon-vitest 10.6.0 peer support; retain the shared Vitest 4 family. |

## Unchanged because R0 already equals R2

These entries are not deferred upgrades.

| Package or crate | R0 | R2 target | Reason |
|---|---|---|---|
| `prettier-plugin-organize-imports` | 4.3.0 | 4.3.0 | Already at the R2 target; this version is the TypeScript 7 compatibility blocker. |
| `vite-plugin-top-level-await` | 1.6.0 | 1.6.0 | R0 already equals the R2 target; no version update was required. |

## Validation

- Library build and Vitest: 6 files, 19 tests passed, including historical v0/v1 project files, WebP buffers, sliced buffers, and synchronous/asynchronous compression interoperability.
- The updated local Core was linked into UI, Frasco, and Sledge. Frasco's Deflate history passed visible drawing, undo, and redo checks with pixel-identical restoration, exercising Core's pako 3 integration.
- Core has no development page: its `dev` script is empty. Consumer pages provide the browser integration checks. There is no Cargo project in this repository.
- Validation used Windows, pnpm 11.5.2, and Node 26.10.0. The machine's default Node remains 22.14.0; it does not satisfy lint-staged 17.6.0 used by the related repositories.
