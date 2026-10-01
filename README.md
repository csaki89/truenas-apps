# TrueNAS apps catalog (csaki89)

Custom TrueNAS SCALE (Docker-based, 24.10+) app catalog.

| App | Image | Description |
|---|---|---|
| `amd-game-stream` | [csaki89/amd-game-stream](https://github.com/csaki89/amd-game-stream) | Headless game streaming (Sunshine/Moonlight) on an AMD GPU |

## Telepítés

1. TrueNAS: **Apps → Discover → Manage Catalogs → Add Catalog**
2. Töltsd ki:
   - Name: `csaki89`
   - Repository: `https://github.com/csaki89/truenas-apps`
   - Preferred Trains: `community`
   - Branch: `main`
3. **Apps → Discover** → keresd az *AMD Game Stream* appot → Install.

## Felépítés

```
ix-dev/<train>/<app>/    forrás (ezt szerkeszd)
library/<verzió>/        a truenas/apps renderelő könyvtára
trains/<train>/<app>/    GENERÁLT, a TrueNAS ezt olvassa – ne szerkeszd
catalog.json             GENERÁLT
```

A `trains/` és a `catalog.json` a `.github/workflows/update-catalog.yaml`-ben
épül a hivatalos `apps_catalog_update` eszközzel, minden `ix-dev/` változásnál.

## Verziók

- `app_version` (`app.yaml`): az image verziója (`amd-game-stream:X.Y.Z`).
- `version` (`app.yaml`): a chart (telepítési leírás) verziója.

Bármilyen `ix-dev/` változásnál emeld a `version`-t (semver). A generátor új
verziómappát hoz létre a `trains/<train>/<app>/` alatt, a régiek megmaradnak,
így a TrueNAS-ban vissza lehet lépni. Új image esetén az `app_version` és az
`ix_values.yaml` `images.image.tag` is változik.

## Helyi ellenőrzés

Docker kell hozzá:

```
docker run --rm -e FAKE_ENV=1 -v "$PWD:/workspace" ghcr.io/truenas/apps_validation:latest apps_catalog_hash_generate --path /workspace
# (a validátor a master-hez képest változott appokat nézi; lásd a workflow-t)
```
