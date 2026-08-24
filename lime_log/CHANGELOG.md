# Changelog

## 0.3.0

Een bekende scooter voelt nu ook als een bekende scooter (0.3.0)

## 0.2.0

Log in with an email and a password instead of Cloudflare Access

## 0.1.2

Let an expired Access session recover instead of stranding the app.

## 0.1.1

Fix the image never starting: `tsx` and `drizzle-kit` were missing because `NODE_ENV` was
set before dependencies were installed, so npm skipped every devDependency.

## 0.1.0

First release. Scan and log, vehicle registry, stats, optional ride details.
