# mDict Android v1.2.18 — Publication gate (26/10/2026)

**Status: BLOCKED — DO NOT PUBLISH AS LATEST**

The two uploaded APK files are byte-identical and match the shipped `SHA256SUMS.txt`:

`a8b5288acb4c206a584d4ff70db8b9ed0e6de173fa5ad6da0506b0dc245e503f`

The embedded metadata checked by Android SDK Build Tools 35 is:
- Package: `com.medipharm.mdict`
- `versionCode=12018`; `versionName=1.2.18`
- Target SDK 35

**Blocking finding:** `apksigner verify --verbose --print-certs` failed with:

`ERROR: Target SDK version 35 requires a minimum of signature scheme v2; the APK is not signed with this or a later signature scheme`.

GitHub Actions release workflow run `40288409513` rejected the uploaded APK before publishing. Earlier run `40288149939` was blocked by runner SDK setup before the signature check; both failures are now diagnosed. No public Release v1.2.18 has been published.

The repository `lesangmd/mdict` is **private**. Its Release asset URL is not an anonymous/public distribution link. The public `lesangmd/mdict-releases` repository is the intended distribution channel.

The canonical production Android signing certificate required for in-place updates from v1.2.17 is:

`CA:BE:20:B2:F3:50:B0:45:0F:58:8E:C7:19:D2:E0:9A:6A:4F:8C:89:05:F8:9D:9A:A8:6C:3A:93:AA:BD:8E:73`

Do not substitute the rejected new-signing candidate (`SIGNING-BASELINE-v1.2.18.md` in the private source repository) because users of v1.2.17 cannot install it over their existing app.

## Requirements to unblock

1. Recover the original private production keystore securely (prefer private GitHub Actions secrets or secure offline backup; never commit or publish it). The earlier private GitHub Actions signing backup artifact is no longer available from run `36215680529`.
2. Sign the v1.2.18 runtime APK with that exact signing key, enable APK Signature Scheme v2/v3, and verify using `apksigner` against API 31+/target 35.
3. Confirm matching package `com.medipharm.mdict`, version code 12018 and canonical certificate.
4. Replace **both** uploaded APKs and their `SHA256SUMS.txt`, then run the public publish workflow and validate an anonymous download.
5. Only **after the public download and signature verification succeed**, promote the public `mdict-update.json` to v1.2.18 and correct WordPress/WebApp links to the public Releases URL.

This gate intentionally preserves v1.2.17 production until a safely installable v1.2.18 is available.
