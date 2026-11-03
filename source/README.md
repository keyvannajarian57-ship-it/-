# KARBON source archive

KARBON website source archive exported from the Higgsfield workspace on 2026-11-03.

Reassemble all `KARBON-source.zip.part.*` files in lexical order:
```sh
cat KARBON-source.zip.part.* > KARBON-source.zip
unzip KARBON-source.zip
```

The archive includes the application source, public assets, lockfiles and project configuration. It excludes Git metadata and local secrets/credentials.

The host reports the website as deployed, but public requests have returned HTTP 401 with `{"error":"unauthenticated"}`. This is a source backup, not a fix for the host-side access error. Community-feed listing remains disabled. No paid service was enabled.
