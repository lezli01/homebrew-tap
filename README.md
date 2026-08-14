# homebrew-tap

Homebrew tap for [lezli01](https://github.com/lezli01)'s tools.

## vincent

A local-first control plane for AI coding-agent workloads — a background daemon
owns state and execution, and the TUI, CLI and API are thin clients of it.
[Repository](https://github.com/lezli01/vincent).

```sh
brew install lezli01/tap/vincent
```

macOS only. On Linux and Windows, use the
[release archives](https://github.com/lezli01/vincent/releases/latest).

> [!WARNING]
> vincent runs coding agents **full-auto by default** — an agent can run
> arbitrary commands as you. The per-task git worktrees isolate collisions
> between tasks, not privileges. This is a
> [documented design decision](https://github.com/lezli01/vincent/blob/master/docs/security-model.md),
> not an oversight.

### Why a cask and not a formula

vincent ships as a pre-built Go binary, which is what casks are for; formulas
are for software Homebrew builds from source.

The cask also clears `com.apple.quarantine` on install. Releases are signed with
keyless [cosign](https://github.com/sigstore/cosign) and carry GitHub build
attestations, but they are **not Apple-notarized** — that is a recurring
certificate cost the project does not take on — so a hand-downloaded archive
trips Gatekeeper. Installing through this tap does not.

### Removing it

```sh
brew uninstall vincent          # binary; unloads the LaunchAgent if installed
brew uninstall --zap vincent    # also removes config, database and transcripts
```

`--zap` deletes `~/Library/Application Support/vincent`, which holds your task
history.

## About this tap

Casks here are generated and pushed by
[GoReleaser](https://goreleaser.com) from each project's release workflow. Do
not edit `Casks/*.rb` by hand — the next release overwrites it.
