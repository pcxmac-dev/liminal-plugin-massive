# Changelog

## 0.2.0 (2026-11-03)

A class on plugin API 2.0 (liminal-lib 1.3.0; the user: "all the plugins under liminal should basically
follow inheritance/oop paradigm"), versioned 0.2.0 with Liminal's release (every distribution at 0.2.0 on
a `release/0.2.0` branch). The feed is `MassivePlugin`, a `FeedPlugin` subclass (`PLUGIN`, its
instance), its headlines `MassiveHeadlines`, a `PublisherPlugin` subclass (`PUBLISHER`): what each
declares is a class attribute of the record field's name, what it does a method of the callback's
(`settings`, `view`, `build`, `scan`, `has_keys`, `serves`, `markets`, `plan_resolutions`; the
headlines' `read`, once `read_headlines`). The feed declares its plans' publication delays itself
(`MassivePlugin.delays`: the free, Starter, Developer and Advanced rows the library's `freshness.py`
held for it). Nothing it does changed: the same settings, requests, scan, strings and limits.

## 1.4.1 (2026-11-02)

The plugin imports the library as `liminal_lib` and depends on liminal-lib (the app, renamed liminal-app, is no longer needed to run the tests; the user, 2026-11-02: "lets rename the app to liminal-app").

## 1.4.0 (2026-11-01)

- Released as its own package, `liminal-plugin-massive`, registered under the entry point group
  `liminal.providers` (its feed and its headlines publisher); its version is the distribution's.
- Its settings are its own (plugin API 1.11, `Provider.settings`): the key, the plans (`TIERS`, the
  stocks plan and each other class's), `MASSIVE_RPM`, `MASSIVE_BASE_URL` and the request caps, once
  the app's base settings (`Settings.api_key`, `tier`, `base_url`, the caps' defaults), are read from
  the variables the app loads and reached with `settings.plugin("massive")`; the plan probe's
  reading of a plan (`tier_for`) is in the package.

## 1.3.0 (2026-10-31)

- Built into the app (then massive-collate): its headlines publisher declares where it writes (the
  main file's news; plugin API 1.8).

## 1.2.0 and before

- Built into the app (then massive-collate): its client on the app's HTTP client (API 1.6), its
  headlines a part of it (API 1.2); see the app's history.
