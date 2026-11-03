# liminal-plugin-massive

Massive (massive.com, formerly Polygon.io) for [Liminal](https://github.com/pcxmac-dev/liminal-app):
stocks, indices, currencies, crypto and futures on its REST API, one plan per asset class, with
1-second and minute bars, reference data (exchanges, listings, trade conditions, market holidays)
and its headlines (a publisher in this plugin, `massive-news`, read every 30 minutes on the same key
and limits). Its scan finds the stocks plan from what the key may ask for.

A Liminal provider plugin released on its own. The app finds it through the entry point group
`liminal.providers` and lists it on the Plugins view and in `liminal plugins`
as `package: liminal-plugin-massive`, with this package's version.

## Settings

User environment variables, saved with the app's `tools/set-key.ps1` or on the Plugins view; the key
is only ever read from the environment and never written to a file. They are the plugin's own
settings (plugin API 1.11), read when the app's settings load:

| Variable | Meaning |
| --- | --- |
| `MASSIVE_API_KEY` | required for any request (your dashboard's API key) |
| `MASSIVE_TIER` | `free` (default), `starter`, `developer` or `advanced`: your Stocks plan; sets how far back the collector reaches; the scan finds it where you set none |
| `MASSIVE_TIER_INDICES`, `MASSIVE_TIER_CURRENCIES`, `MASSIVE_TIER_CRYPTO`, `MASSIVE_TIER_FUTURES` | the plan of each other asset class (default `free`); a free class is held to 5 requests a minute |
| `MASSIVE_RPM` | override the plan's requests a minute (0 = unlimited) |
| `MASSIVE_BASE_URL` | the API's base URL (default: Massive's own) |
| `MASSIVE_MAX_REQUESTS_PER_RUN`, `MASSIVE_MAX_REQUESTS_PER_DAY` | hard caps (default 250 / 2000) |

## Install

Into the app's environment, from the app's folder:

```powershell
.venv\Scripts\python.exe -m pip install "liminal-plugin-massive @ git+https://github.com/pcxmac-dev/liminal-plugin-massive@v1.4.1"
```

or with the app's plugins (`pip install -e ".[plugins]"` in liminal-app). The app loads it on its next
start.

## Compatibility

It is written for plugin API 1.11 (`PLUGIN.api`: a plugin's own settings; the app's HTTP client;
the databases a plugin writes). An app offering 1.11 or a later 1.x loads it; an app of another
major, or one older than 1.11, leaves it out and says why on the Plugins view.

## Develop

```powershell
python -m venv .venv
.venv\Scripts\python.exe -m pip install "liminal-lib @ git+https://github.com/pcxmac-dev/liminal-lib@main"
.venv\Scripts\python.exe -m pip install -e ".[dev]"
.venv\Scripts\python.exe -m pytest -q
```

Tests never send requests (a fake session answers) and never read your key.
