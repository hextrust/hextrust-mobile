# hextrust-mobile
a wrapper to share public packages


**How to Publish/Update the App Redirect Page**
Repo: hextrust/hextrust-mobile — hosted at https://app-redirect.hexsafe.hextech.io/

Environments (via URL param)
URL	Env
.../?env=uat	UAT
.../?env=sandbox	Sandbox
.../	Defaults to UAT


To update download links (the common task)
1) Clone + branch:
git clone git@github.com:hextrust/hextrust-mobile.git && cd hextrust-mobile
git checkout -b fix/update-uat-apk 

2) Edit docs/redirects.json — update the APK/TestFlight/store URLs.
      APK pattern: <env>-<version>+<build>.apk, e.g. uat-2.0.4+68.apk / sandbox-2.0.4+68.apk (must match a real release in hexsafe-2-android-client)
3) Validate: python3 -m json.tool docs/redirects.json
4) Commit, push, open a PR to main, get it reviewed, merge.
5) Done — the deploy-redirect.yaml workflow auto-deploys any docs/** change to main (~1 min).

To Verify
curl -s "https://app-redirect.hexsafe.hextech.io/?env=uat"
curl -s "https://app-redirect.hexsafe.hextech.io/?env=sandbox"

Or browser-test: Android → APK download, iOS/Desktop on sandbox → TestFlight.
