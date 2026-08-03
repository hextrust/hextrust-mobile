# hextrust-mobile
a wrapper to share public packages


How to Publish/Update the App Redirect Page
Repo: hextrust/hextrust-mobile — hosted at https://app-redirect.hexsafe.hextech.io/

Environments (via URL param)
URL	Env
.../?env=uat	UAT
.../?env=sandbox	Sandbox
.../	Defaults to UAT
To update download links (the common task)
Clone + branch:
Edit docs/redirects.json — update the APK/TestFlight/store URLs.
APK pattern: <env>-<version>+<build>.apk, e.g. uat-2.0.4+68.apk / sandbox-2.0.4+68.apk (must match a real release in hexsafe-2-android-client)
Validate: python3 -m json.tool docs/redirects.json
Commit, push, open a PR to main, get it reviewed, merge.
Done — the deploy-redirect.yaml workflow auto-deploys any docs/** change to main (~1 min).
To verify
Or browser-test: Android → APK download, iOS/Desktop on sandbox → TestFlight.

Guardrails
Only edit URLs in redirects.json — index.html logic rarely changes.
Don't remove docs/.nojekyll or modify the workflow.
No secrets in docs/ (public site).
This page is UAT & Sandbox only — prod is not served from it.
