# Releasing New Versions (for Maintainers)

This document outlines the process for releasing new versions of the `agencyswarm-mcp` package using Changesets.

## Pre-Release Workflow (During Development)

For every pull request or logical set of changes that should be noted in the changelog (new features, bug fixes, breaking changes, significant refactors, user-facing doc updates), follow these steps **before** merging/pushing the final commit:

1.  **Make Changes**: Implement your code or relevant documentation updates.
2.  **Stage Changes**: Stage all relevant changes.
    ```bash
    git add .
    ```
3.  **Run Changeset**: Execute the changeset command.
    ```bash
    npm run changeset
    # or
    npx changeset add
    ```
4.  **Select Package(s)**: Use the arrow keys and spacebar to select the package(s) affected (usually just the main package). Press Enter.
5.  **Select Bump Type**: Choose the appropriate semantic version bump type (`Patch`, `Minor`, or `Major`) for the changes.
6.  **Enter Summary**: Write a concise, user-facing summary of the changes for the `CHANGELOG.md`. Use the imperative mood (e.g., "Add support for X", "Fix bug in Y"). This is *different* from your detailed Git commit message.
7.  **Stage Changeset File**: Stage the newly created markdown file in the `.changeset/` directory.
    ```bash
    git add .changeset/*.md
    ```
8.  **Commit**: Commit both your code changes and the changeset file together with a detailed Git commit message.
    ```bash
    git commit -m "feat(scope): Describe the change in detail..."
    ```

## Creating a Release

Once all desired changesets have been merged into the main branch:

1.  **Version Bump & Changelog**: Run the `changeset version` command. This consumes all `.changeset/*.md` files, updates the `package.json` version(s), updates the `CHANGELOG.md`, and deletes the changeset files.
    ```bash
    npx changeset version
    # or potentially integrated into a release script
    ```
2.  **Review Changes**: Check the updated `package.json` and `CHANGELOG.md` for correctness.
3.  **Commit Version Bump**: Stage and commit the changes made by `changeset version`.
    ```bash
    git add package.json CHANGELOG.md
    git commit -m "chore: Release vX.Y.Z" 
    ```
4.  **Tag Release**: Create a Git tag for the new version.
    ```bash
    git tag vX.Y.Z
    ```
5.  **Push Changes & Tag**: Push the commit and the new tag to the remote repository.
    ```bash
    git push origin main --tags
    ```
6.  **Publish to npm**: Publish the new version to the npm registry.
    ```bash
    npm publish
    # or
    npx changeset publish 
    ```

Following this process ensures accurate versioning and automated changelog generation. 