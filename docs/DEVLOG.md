# Development log

## 2026-09-05 release pipeline candidate

This isolated branch replaces the invalid workflow with the shared build-only recipe.
It preserves the title CMake flags, configuration, framework/UI pins, and existing version.
The change adds source identity, archive, platform copy, dependency, and native generator checks.
It applies the macOS deployment target to every build step and selects pinned static SDL.

Corpus consulted: PSX-PUB-021 through PSX-PUB-023, PSX-PUB-028, and PSX-PUB-031 through PSX-PUB-033.
The whole-job deployment target follows CMake's documented `MACOSX_DEPLOYMENT_TARGET` behavior.
Static SDL follows the existing framework FetchContent path and SDL's static-library options.
The workflow passes Actionlint 1.7.12.
Shared generator tests also cover repeat preparation, stale evidence, corrupt downloads, and platform mismatches.

The existing public Windows package passes the new native generator gate.
The existing Linux package passes after its documented OpenGL dependency is present.
The existing Mac packages fail the new minimum-OS and external-library gates.
The corrected Mac build still needs the native CI run.
No new public asset, tag, or RetComM submission is part of this source change.
