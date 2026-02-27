# GeoLite2 City Database

MaxMind GeoLite2 City databases used for IP geolocation.

## Ownership

This repository is owned by the **Chaos Monkeys** team (`@fulcrumapp/chaos-monkeys`).

## Contents

| File | Date | Description |
|------|------|-------------|
| `GeoLite2-City-2026-02-16.mmdb` | 2026-02-16 | Current database |
| `GeoLite2-City-2022-12-06.mmdb` | 2022-12-06 | Legacy database |
| `GeoLite2-City-2020-11-10.mmdb` | 2020-11-10 | Legacy database |

## Updating the Database

GeoLite2 databases are updated regularly by MaxMind. You can update this repository in one of two ways:

1. **Manual update from MaxMind**
   - Download the latest GeoLite2-City MMDB directly from [MaxMind](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data).
   - Add the file with the naming convention `GeoLite2-City-YYYY-MM-DD.mmdb`.
2. **Automated update via Copilot (GitHub mirror)**
   - Use the Copilot skill described below, which fetches the latest GeoLite2-City MMDB from the [`P3TERX/GeoLite.mmdb` GitHub mirror](https://github.com/P3TERX/GeoLite.mmdb) that republishes the unmodified MaxMind GeoLite2 City database.
3. **For either method**, open a PR for review by the Chaos Monkeys team.

### Using Copilot

This repo includes a Copilot [agent skill](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills) to automate the update. The skill downloads the latest GeoLite2-City MMDB from the [`P3TERX/GeoLite.mmdb` GitHub mirror](https://github.com/P3TERX/GeoLite.mmdb), which distributes the unmodified MaxMind GeoLite2 City database.

Copilot will automatically use this skill when you ask it to update the GeoLite2 database — for example:

> "Update the GeoLite2 database to the latest version"

This works in VS Code agent mode, the Copilot CLI, and the Copilot coding agent (e.g., by assigning Copilot to a GitHub issue).

## License

The GeoLite2 databases are distributed under the [MaxMind GeoLite2 End User License Agreement](https://www.maxmind.com/en/geolite2/eula).
