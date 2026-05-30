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

## Discipline `last_updated`

**Critique** : à chaque nouvelle release (v0.4.x, v0.5.x, etc.), le champ `last_updated` du `manifest.json` LIVE (sur `main`) doit être incrémenté à la **date réelle de publication**, format ISO `YYYY-MM-DD HH:MM:SS` (UTC recommandé).

Pourquoi : la lib `plugin-update-checker` (Yahnis Elsts v5) compare le `last_updated` distant avec le cache local pour décider si une update doit être re-fetched / proposée. Un `last_updated` non incrémenté = PUC peut sous-évaluer la fraîcheur et retarder la détection de l'update côté sites.

Workflow type lors d'un bump (intégré au release process Fleet Manager) :

1. Tag v0.X.Y sur le repo source privé `alain2907/np-affiliation-core`.
2. Build zip v0.X.Y (cf. `INSTALL.md` côté source).
3. Update `manifest.json` ici sur `main` : bump `version` + bump `last_updated` (`date -u +"%Y-%m-%d %H:%M:%S"`) + bump `download_url` (pointer la nouvelle release) + prepend la section `changelog`.
4. Commit + push `main`.
5. `gh release create v0.X.Y np-affiliation-core.zip --repo alain2907/np-affiliation-core-public`.

Ne pas oublier l'étape 3 : un push de release sans bump de `last_updated` reste invisible aux sites pendant la durée de leur cache local PUC (typiquement 12h).
