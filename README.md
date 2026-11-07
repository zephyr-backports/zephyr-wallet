## Security backports (this fork)

This is **not** a new Zephyr wallet. It is `ZephyrProtocol/zephyr-wallet` at its base commit
(`a63147fd`, "Fix price history graph", the state of the v2.3.0 web and desktop wallets) plus a
small number of security changes. Tags mirror the zephyr fork: `vX.Y.Z-sec.N`.
Full policy: https://github.com/zephyr-backports/zephyr-backports (docs/POLICY.md).

**This fork receives rebuilt artefacts and dependency pins only** (POLICY §3 and §5):
- **Artefact rebuilds:** the WASM and worker files in `client/public/`, taken from a named tag of
  the zephyr-javascript security fork, which is itself rebuilt from the zephyr and zephyr-cpp
  security forks. Each such commit names its sources (`Built-From: <repo> <tag> <sha>`) and comes
  with a signed build manifest.
- **Dependency pins:** `package.json` and `package-lock.json` (in `client/` and
  `zephyr-desktop-app/`) moved to the version of a dependency that fixes a named advisory
  (`Advisory: <GHSA or CVE id>`). A dependency without a fixed version, or a fix that needs
  application code, stays out: that is upstream's work.

**No platform code signing** (POLICY §7). The web build and the desktop builds are not notarized
by Apple or Authenticode-signed for Windows, like upstream's own releases. Verify a build by the
GPG-signed `SHA256SUMS`, the signed build manifest and the public CI run that produced it.

Rules, in short:
- Only clear security issues: memory safety on untrusted input, key/secret exposure, funds at
  risk in transaction construction, privacy, remote DoS, or a dependency with a current advisory.
  No features, no refactors, no correctness-only fixes, no "newer dependency" bumps.
- No application code of our own. Nothing of our own except this section,
  `SECURITY-BACKPORTS.md`, CI, and the two commit types above.
- Never breaks compatibility with upstream: same wallet files, same nodes, same behaviour. A
  wallet from this fork and one from upstream open each other's data.
- Every change has an advisory in `SECURITY-BACKPORTS.md`: what, origin, impact,
  compatibility statement, test evidence. CI verifies that every commit above the upstream
  base is one of the allowed types (`.github/workflows/provenance.yml`).
- This fork is archived as soon as upstream carries these fixes itself.

Reporting a security issue in Zephyr: report it to the ZephyrProtocol team. We do not fix
issues ourselves; we only bring in fixes that upstream projects have published.

# Zephyr Frontend for Web and Desktop

Official Zephyr Frontend Monorepository for Zephyr Desktop and Zephyr Web Version.
Originally forked from: https://github.com/haven-protocol-org/haven-web-app

**Main Libraries:** React, Redux, Electron, Styled Components

**Languages:** Typescript, Javascript

## Web

#### Environments

- mainnet
- stagenet
- testnet

#### Build & Develop

1. Navigate to client folder
2. Build the app for given environment
3. Start the app for given environment

```bash
cd client
npm run build:web
npm run start:web
```

## Desktop

#### Build

1. Navigate to client folder
2. Build the app for the environment

```bash
cd client
npm run build:desktop
```

To build the final desktop build

```bash
sh ./sh/make.sh
```

#### Develop

1. Run start script to prepare client
2. Start the build by executing shell script

```bash
npm run start:desktop
cd ../
sh ./sh/develop.sh
```
