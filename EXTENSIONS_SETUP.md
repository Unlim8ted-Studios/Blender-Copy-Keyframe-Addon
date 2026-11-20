# Blender Extensions review draft

Configuration is prepared for GitHub. No extension has been released or uploaded. Uploading and artifact builds remain disabled pending licensing approval and initial listing setup.

## Licensing blocks submission

The existing LICENCE.md prohibits commercial redistribution. Blender Extensions requires GPL-3.0-or-later for add-ons. The manifest proposes that license for review; it does not relicense the code. Do not submit the package until the owner approves and replaces LICENCE.md with the GPL v3 text and an or-later grant. The upload workflow also checks for GPL text.

## Review and install

The original single-file add-on is preserved. __init__.py provides an extension entry point. Build with `blender --command extension build --output-dir dist`, then install the ZIP through Preferences > Get Extensions > Install from Disk.

Extension ID: `copy_keyframe_to_selected`. Version: `1.0.0`. Minimum Blender: 4.2.0.

Copy Keyframe uses legacy Action.fcurves, removed in Blender 5.0. The manifest excludes Blender 5.0 and later. Modern animation support needs a separate implementation and functional testing.

## Enable GitHub to Blender updates after review

1. Approve and apply GPL licensing, review the diff, then push the reviewed changes. Set repository Actions variable `BLENDER_EXTENSIONS_LICENSE_APPROVED` = `true` only after the license is actually changed. Until then, builds are skipped.
2. Build and manually submit the initial extension at https://extensions.blender.org/submit/. Complete the listing, screenshots, and moderation process. This workflow updates an existing listing; it does not create one.
3. Generate an API token from your Blender Extensions profile. Never commit or paste it into chat.
4. In each GitHub repo, create the `blender-extensions` environment. Add its secret `BLENDER_EXTENSIONS_TOKEN` and its variable `BLENDER_EXTENSION_ID` using the identifier of the actual Blender listing. Restrict the environment to trusted release tags and optionally require a reviewer.
5. Add repository Actions variable `BLENDER_EXTENSIONS_SYNC_ENABLED` = `true` only when ready. It is disabled by default.
6. For updates, increment the manifest version and publish a matching GitHub release such as `v1.0.1`. Stable published releases trigger validation, ZIP building, and uploading. Prereleases do not upload. Pushes and pull requests only build artifacts. A manual workflow run only builds. Builds require the licensing approval variable described above.
7. Check Actions and the Blender listing for the resulting upload/moderation status. A new version can still require platform review. Do not reuse an existing version.

This is release-driven synchronization of packaged versions, not a mirror of every Git commit. The build uses Blender 4.2.0; UI behavior and minimum-version functional compatibility still need verification before submission.

References: https://developer.blender.org/docs/features/extensions/ci_cd/ and https://docs.blender.org/manual/en/latest/advanced/extensions/licenses.html
