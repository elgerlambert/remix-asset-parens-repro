# Remix asset server: `(` or `)` in the project path breaks `allowFiles`

Minimal reproduction for `@remix-run/assets@1.0.0` (via `remix@3.0.0`).

`app (copy)/` is an unmodified app generated with:

```sh
pnpm dlx remix@3.0.0 new "./app (copy)"
```

The only change after generating is `pnpm approve-builds esbuild`, which records the approval in `pnpm-workspace.yaml`.

## Steps

```sh
cd "app (copy)"
pnpm install
pnpm dev
```

### Expected

`Server listening on http://localhost:44100`, with the starter page and `/assets/app/actions/public/entry.ts` served.

### Actual

The server fails during startup:

```
AssetServerCompilationError: File ".../app (copy)/app/actions/public/entry.ts" is not allowed by the asset server access configuration. Add a matching allowFiles or allowPackages rule, or remove a conflicting denyFiles rule.
  code: 'FILE_NOT_ALLOWED'
```

### Control

Copy the same app to a folder without parentheses and it works:

```sh
cp -R "app (copy)" app-copy
cd app-copy
pnpm dev
```
