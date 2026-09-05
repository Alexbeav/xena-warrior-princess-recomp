# Development log

## 2026-09-05 native canary: Linux source audit

The same run builds and packages the Linux setup host successfully.
The final gate then fails because Git rejects the container checkout's ownership.
The checkout action adds `safe.directory` under its temporary HOME.
The later shell gate does not inherit that configuration.
The workflow now adds the five explicit owned checkout paths in the container's shell environment.
No wildcard trust or local machine configuration change is required.

Corpus consulted: shared release findings and failure/ regression ledgers contain no matching ownership record.
The [Actions runner issue](https://github.com/actions/runner/issues/2033) documents the container/HOME mismatch.
The [Git configuration reference](https://git-scm.com/docs/git-config) defines the per-directory trust setting.
Compilation, package-copy, and payload failure are rejected diagnoses for this observed Git error.
The next native run must pass the complete archive and generator gate.

## 2026-09-05 native canary: SDL extraction

Run 33967561747 passes the frozen-source gate but both native Mac jobs fail during SDL extraction.
The pinned framework helper expands an empty `force` array under `set -u` at line 77.
The Mac shell reports `force[@]: unbound variable` before either compilation starts.
The shared workflow now uses its existing hash-checked inline recipe on every platform.
Its explicit GNU/BSD tar branches avoid the empty array and preserve the pinned SDL hash.
The framework, UI, game recipe, and version remain unchanged.

Corpus consulted: PSX-PUB-023 and PSX-PUB-032 through PSX-PUB-034; no existing empty-array finding.
The [GNU Bash maintainer discussion](https://lists.gnu.org/archive/html/bug-bash/2019-05/msg00024.html)
confirms that Bash 4.4 changed this behavior; a modern Linux shell is not a Mac shell control.
The regeneration regression preserves the source hash and extraction paths.
The next native CI run is the decisive extraction check.

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
