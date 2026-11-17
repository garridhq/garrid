# Garrid

**The delivery queue for AI coding agents.**

Agents stop committing to main. Each agent hands an exact set of changed files
to the queue. The Garrid worker rebuilds the change on the latest main, runs
your checks, and lands it atomically. Garrid asks for you only when a change
needs a decision or a repair.

Garrid Software LLC · https://garrid.dev

## Install

macOS (signed and notarized):

```sh
brew install --cask garridhq/tap/garrid
```

Linux (amd64 or arm64): download `garrid_<version>_linux_<arch>.tar.gz` from
the release, check it, and put `garrid` on your `PATH`:

```sh
shasum -a 256 -c checksums.txt --ignore-missing
tar -xzf garrid_<version>_linux_<arch>.tar.gz
install -m 0755 garrid ~/.local/bin/garrid
```

## Verify

Every release has one `checksums.txt` that lists every archive. On macOS,
`codesign --verify --strict "$(command -v garrid)"` and
`spctl --assess --type execute "$(command -v garrid)"` check the signature
and the notarization.

## Start

In a repository your agents work in:

```sh
garrid init       # enroll the repository and start the worker
garrid status     # is anything waiting on me?
garrid console    # open the operator console
```

Agents hand over a change with `garrid deliver --paths <files> -m "<subject>"`
and can wait for it with `garrid wait <id>`. `garrid help` lists every
command.

## Where it runs

The worker is the only thing that lands on your branch, and it runs on a
machine you control. Checks run there or on runners you add over SSH. You
choose how much is hosted:

- Local: no account; nothing leaves your machines.
- Hybrid: connect the optional hosted control plane for the phone app,
  alerts and team views. It receives typed events (states, counts and codes,
  never file content, paths or commit text), and the worker re-checks every
  action sent from it.

## Documentation

https://garrid.dev/docs

## Licence

Garrid is proprietary software. Your use is governed by the end-user terms
in `LICENSE.md`. The free tier (one repository, no licence file) may be used
for any purpose. Third-party components and their licences are listed in
`THIRD_PARTY_NOTICES`.

## Support

Run `garrid support` for a support bundle (counts and codes only), or open an
issue at https://github.com/garridhq/garrid/issues. Report a security issue
to security@garrid.com, not in a public issue.

## This repository

This repository holds Garrid's releases, release notes (`CHANGELOG.md`) and
issue tracker. Garrid's source is not public. Each release attaches the macOS
and Linux archives and one `checksums.txt`.
