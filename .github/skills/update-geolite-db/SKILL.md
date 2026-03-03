---
name: update-geolite-db
description: "Download and add the latest GeoLite2-City database to the repository. Use this when asked to update the GeoLite2 database or when a newer version is needed."
---

# Update GeoLite2-City Database

Follow these steps to update the GeoLite2-City MMDB database in this repository.

## Step 1: Check existing database versions

List the current database files to identify the latest version already present:

```bash
ls -lh *.mmdb
```

## Step 2: Find the latest available release

Fetch the latest release tag from the P3TERX/GeoLite.mmdb GitHub mirror:

```bash
curl -sI "https://github.com/P3TERX/GeoLite.mmdb/releases/latest" | grep -i location | sed 's/.*tag\///' | tr -d '\r'
```

If the latest release is already present in the repo, stop and inform the user that the database is up to date.

## Step 3: Download the database

Download the latest GeoLite2-City.mmdb. Replace `TAG` with the value from step 2 (e.g., `2026.02.16`). Convert dots to hyphens for the filename (e.g., `2026.02.16` → `GeoLite2-City-2026-02-16.mmdb`):

```bash
curl -L -o "GeoLite2-City-YYYY-MM-DD.mmdb" "https://github.com/P3TERX/GeoLite.mmdb/releases/download/TAG/GeoLite2-City.mmdb"
```

## Step 4: Verify the download

Check that the file is a valid MMDB and has a reasonable size (should be ~50MB+):

```bash
file GeoLite2-City-*.mmdb
ls -lh GeoLite2-City-*.mmdb
```

All files should report as "data" or similar binary format. If a file reports as HTML or is suspiciously small, the download failed — retry or report the error.

Also verify the SHA256 checksum against the published value from the mirror:

```bash
curl -L -o "GeoLite2-City.mmdb.sha256sum" "https://github.com/P3TERX/GeoLite.mmdb/releases/download/TAG/GeoLite2-City.mmdb.sha256sum"
sha256sum -c GeoLite2-City.mmdb.sha256sum
rm GeoLite2-City.mmdb.sha256sum
```

If the checksum does not match, delete the downloaded file and retry. Do **not** commit an unverified database.

## Step 5: Ensure git-lfs is tracking

Confirm git-lfs is installed and tracking `.mmdb` files:

```bash
git lfs install
cat .gitattributes
git lfs status
```

The `.gitattributes` file must contain: `*.mmdb filter=lfs diff=lfs merge=lfs -text`

## Step 6: Update the README

Update the database table in `README.md`:
- Add the new database entry with the date and mark it as "Current database"
- Change previous "Current database" entries to "Legacy database"

## Step 7: Create a branch and commit

```bash
git checkout -b task/update-geolite2-db-YYYY-MM-DD
git add *.mmdb .gitattributes README.md
git commit -m "chore: update GeoLite2-City database to YYYY-MM-DD"
git push origin task/update-geolite2-db-YYYY-MM-DD
```

## Step 8: Open a pull request

Open a PR targeting the default branch for the Chaos Monkeys team (`@fulcrumapp/chaos-monkeys`) to review.

## Important notes

- All `*.mmdb` files are tracked by git-lfs. Never commit them without git-lfs enabled.
- Do **not** remove old database files unless explicitly asked.
- Use the naming convention `GeoLite2-City-YYYY-MM-DD.mmdb` with hyphens, not dots.
- The source mirror is [P3TERX/GeoLite.mmdb](https://github.com/P3TERX/GeoLite.mmdb). The upstream source is [MaxMind GeoLite2](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data).
