# Jamie's Homebrew tap

Personal maintenance of the SeKey Homebrew cask.

## Install

```sh
brew tap jvsteiner/tap
brew install --cask jvsteiner/tap/sekey
```

Follow the installation caveat to configure `SSH_AUTH_SOCK`, or set
`IdentityAgent ~/.sekey/ssh-agent.ssh` in your SSH configuration.

The fully qualified cask name selects this tap instead of Homebrew's disabled cask.
If SeKey 0.1 is already installed, keep using it; adding this tap does not replace
the running agent. An intentional reinstall can use
`brew reinstall --cask jvsteiner/tap/sekey`, but will restart/replace the agent.
Do not use `--zap` during migration: it removes `~/.sekey`.

## Release provenance

Version 0.1 is a byte-for-byte mirror of the original
[SeKey package](https://github.com/sekey/sekey/releases/tag/0.1), hosted on
[the personal fork](https://github.com/jvsteiner/sekey/releases/tag/0.1).
It is not a new build. It retains Nicolas Trippar's original signing identity
and the original Intel binary; Apple Silicon requires Rosetta.

SHA-256: `8d473f7214ba76b70ca30905e2ebd07d7c421f1cff320285bd8ec8d2a7a5b083`.

The cask is adapted from [Homebrew/homebrew-cask](https://github.com/Homebrew/homebrew-cask),
under its BSD 2-Clause license. SeKey itself is MIT-licensed.
Maintenance of this tap does not imply new upstream application development.

## Maintenance

For a new release, upload the signed package to `jvsteiner/sekey`, update
`version` and `sha256` in `Casks/sekey.rb`, then run:

```sh
brew style --cask jvsteiner/tap/sekey
brew audit --cask jvsteiner/tap/sekey
brew fetch --cask jvsteiner/tap/sekey
brew install --cask --dry-run jvsteiner/tap/sekey
```

Test actual install/uninstall on a separate macOS account or machine before
changing packaging behavior. Preserve the app's signing identity and entitlements
when building updates, and verify access to existing Secure Enclave keys.
Commit and push cask updates; Homebrew picks them up through `brew update`.
