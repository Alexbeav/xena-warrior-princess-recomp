# Release candidate builds

The release workflow accepts one explicit version already recorded in source.
It creates Windows x64, Linux x64, macOS ARM64, and macOS x64 build artifacts.
It has read-only repository access and cannot create a tag or publish a release.

The source gate binds dependency commits, executable names, and the game recipe.
The final ZIP gate checks payload, architecture, permissions, and dependencies.
Each native runner executes the two generators from a fresh directory containing spaces.
Those checks do not claim complete setup or gameplay.

The macOS target applies to every executable needed for setup.
The setup host links pinned static SDL source instead of a Homebrew SDL library.
The emitter cache includes the runner, architecture, minimum OS, framework, and workflow recipe.

The current branch is a build-only canary at version 0.1.2.
It leaves the existing release and its Windows gameplay evidence unchanged.
A public replacement needs a new version, matching platform evidence, and exact-manifest authorization.
