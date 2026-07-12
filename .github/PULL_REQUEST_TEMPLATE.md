---
*** Begin Patch
*** Add File: .github/PULL_REQUEST_TEMPLATE.md
+<!--
+  Pull Request template for quick debugging patches.
+  This template summarizes what changed and how to test.
+-->
+
+# Fix: safe appId + start listener after auth + add delete logging
+
+This PR contains short-term debugging and safety improvements to help identify why Firestore Listen and delete operations were failing in production.
+
+## Summary
+- Add `safeAppId` fallback to prevent empty appId in Firestore paths.
+- Start `onSnapshot` for matches only after authentication completes (`startMatchesListener`).
+- Add `getDoc` and console logging around delete operations to surface `permission-denied` / `not-found` / `unauthenticated` errors.
+- Enable Firestore debug logs (`setLogLevel('debug')`) for development investigation.
+
+## How to test
+1. Open the app from this branch, open DevTools Console.
+2. Confirm `startMatchesListener` log appears with `appId` and `uid`.
+3. Attempt deleting a match and inspect Console for `DB.deleteMatch` logs and any error codes.
+
+## Notes
+- `setLogLevel('debug')` is enabled for debugging; remove or disable it before merging to production.
+
*** End Patch
