# np-affiliation-core-public

Mirror public servant le `manifest.json` + les release zips pour le plugin
`np-affiliation-core` (réseau Fleet Manager, plugin-update-checker Yahnis Elsts v5).

**Ne pas push de code ici.** Source = repo privé `alain2907/np-affiliation-core`.

## Endpoint

- Manifest PUC (servi via raw.githubusercontent.com) :
  https://raw.githubusercontent.com/alain2907/np-affiliation-core-public/main/manifest.json
- Releases : zips buildés depuis le repo source + lib PUC fetched via INSTALL.md.

## Workflow release

1. Tag v0.X.Y sur le repo source privé.
2. Build zip : `git clone --branch v0.X.Y` + curl PUC tarball + `zip -r np-affiliation-core.zip np-affiliation-core/`.
3. Bump `version` et `download_url` dans `manifest.json` ici → commit + push main.
4. `gh release create v0.X.Y np-affiliation-core.zip --repo alain2907/np-affiliation-core-public`.

Ne pas modifier la structure (pas de wiki, pas de Pages, juste manifest.json + releases).
