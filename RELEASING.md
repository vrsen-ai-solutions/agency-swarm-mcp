# Releasing New Versions (for Maintainers)

This document outlines the process for releasing new versions of the `agencyswarm-mcp` package. This project uses a combination of `npm publish` automation and Changesets for changelog generation.

## Pre-Release Workflow (For Changelog Entries)

For every pull request or logical set of changes that should be noted in the changelog (new features, bug fixes, breaking changes, etc.), follow these steps **before** merging/pushing the final commit **if you want these changes documented in the CHANGELOG.md**:

1.  **Make Changes**: Implement your code or documentation updates.
2.  **Stage Changes**: Stage all relevant changes (`git add .`).
3.  **Run Changeset**: Execute `npx changeset add`.
4.  **Select Package(s)**: Select the affected package(s) (usually just `agencyswarm-mcp`).
5.  **Select Bump Type**: Choose the semantic version bump type (`Patch`, `Minor`, or `Major`) that *logically* corresponds to your changes. **Note:** This choice currently only affects the `CHANGELOG.md` generation. The actual version bump during publish is handled separately (see below).
6.  **Enter Summary**: Write a concise summary for the `CHANGELOG.md`.
7.  **Stage Changeset File**: Stage the new `.changeset/*.md` file (`git add .changeset/*.md`).
8.  **Commit**: Commit your code changes and the changeset file together (`git commit -m "feat: Describe change..."`).

## Creating a Release

Releasing involves publishing to npm, which automatically handles the version bump.

1.  **Ensure Changesets Added (Optional):** Make sure any changes intended for the changelog have had corresponding changeset files added and committed as described above.
2.  **Publish**: Run the standard npm publish command:
    ```bash
    npm publish
    ```
    *   This triggers the `prepublishOnly` script in `package.json`.
    *   The `prepublishOnly` script executes `scripts/prepare-package.js`.
    *   `prepare-package.js` **automatically increments the patch version** in `package.json` (e.g., `0.1.2` becomes `0.1.3`). **Note:** Minor or Major version bumps currently require manually editing `package.json` *before* running `npm publish`.
    *   `npm publish` then packages and uploads the new version to the npm registry.
3.  **Update Changelog (If Changesets were added):** If you added changesets in the pre-release workflow, run `changeset version` now. This consumes the `.changeset/*.md` files and updates `CHANGELOG.md` based on the summaries you provided. It should not affect the version in `package.json` as it was already updated by `prepare-package.js`.
    ```bash
    npx changeset version
    ```
4.  **Review Changes**: Check the updated `package.json` (version bumped by script) and `CHANGELOG.md` (updated by `changeset version`, if applicable) for correctness.
5.  **Commit Version Bump & Changelog**: Stage `package.json` and `CHANGELOG.md`. Commit them.
    ```bash
    git add package.json CHANGELOG.md
    git commit -m "chore: Release vX.Y.Z" 
    ```
    *(Replace X.Y.Z with the new version number)*
6.  **Tag Release**: Create a Git tag for the new version.
    ```bash
    git tag vX.Y.Z
    ```
    *(Replace X.Y.Z with the new version number)*
7.  **Push Changes & Tag**: Push the commit and the new tag to the remote repository.
    ```bash
    git push origin main --tags
    ```

Following this process ensures the package is published with an automatic patch bump, and the changelog is accurately generated if changesets are used.
