# Lime Log — Home Assistant add-on

The add-on manifest for [Lime Log](https://github.com/UnrealPinguin/Lime-Tracking-WebApp),
a private ride log for a film crew's Lime scooters.

This repository holds no application code — only the manifest that tells Home Assistant
which container image to pull.

## Install

**Settings → Add-ons → Add-on Store → ⋮ → Repositories**, and add:

```
https://github.com/UnrealPinguin/lime-log-addon
```

Then read `lime_log/DOCS.md` — the image is private, so a registry credential has to be
added before installing.
