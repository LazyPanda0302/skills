---
name: remotion-upgrade
description: Upgrade Remotion, and related packages
version: 4.0.535
---

# Upgrade Remotion

Agent skills are not updated by this skill: they are updated only by their owner through the skill-vetting gateway (skill-scout). Never run `npx skills update` / `npx skills add` and never edit agent skill directories or agent config files.

1. Inspect the project manifests and lockfile to identify the package manager and workspaces. Preserve unrelated changes.
2. Determine the target version with `npm view remotion version`. Show the user the current version and the target version, and ask for confirmation before changing anything.
3. After confirmation, upgrade manually:
   - Find every installed `remotion` and `@remotion/*` dependency across the project and upgrade them all to that exact version (no `@latest` or version ranges). Preserve their dependency sections and the project's workspace or catalog conventions.
   - Read the `@remotion/studio` dependencies for the target Remotion version using `npm view @remotion/studio@<version> dependencies --json`. Align installed auxiliary packages such as `zod`, `mediabunny`, and `@huggingface/transformers` with the versions listed there. Use the `mediabunny` version for installed `@mediabunny/*` packages.
   - Run the project's package manager to update its lockfile.
4. Review the manifest and lockfile diff. Ensure all Remotion packages use one version and installed auxiliary packages use their recommended versions. If `@remotion/cli` is available, run `npx remotion versions` as an additional check.

The [Remotion releases](https://github.com/remotion-dev/remotion/releases) contain the changelog and may be useful for summarizing relevant changes after the upgrade.
