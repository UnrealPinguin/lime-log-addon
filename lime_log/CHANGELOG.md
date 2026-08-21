# Changelog

## 0.1.1

Fix the image never starting: `tsx` and `drizzle-kit` were missing because `NODE_ENV` was
set before dependencies were installed, so npm skipped every devDependency.

## 0.1.0

First release. Scan and log, vehicle registry, stats, optional ride details.
