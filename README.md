![Teodora Browser](./docs/source/_static/Teodora.svg)

## Overview

This repository holds the build tools needed to build the Teodora desktop browser for macOS, Windows, and Linux. Teodora is a decentralized, AI-driven browser that integrates the Lightweb AI interface for seamless interaction with Web3 applications. It builds upon Brave's robust privacy and security architecture while introducing a minimalist, responsive UI for intuitive navigation.

Key features include:
  - **Lightweb AI Interface**: A decentralized AI-driven interface for enhanced browsing and interaction.
  - **Web3 Wallet Integration**: Seamless compatibility with Brave Wallet and MetaMask for blockchain interactions.
  - **Minimalist UI**: Optimized for quick onboarding and intuitive navigation across desktop and mobile platforms.
  - **Privacy and Security**: Extended privacy practices consistent with Brave’s architecture, tailored for decentralized AI interactions.

## Downloads

You can [visit our website](https://teodora.com/download) to get the latest stable release.

## Contributing

Please see the [contributing guidelines](./CONTRIBUTING.md).

Our [Wiki](https://github.com/teodora/teodora-browser/wiki) also has some useful technical information.

## Community

[Join the Q&A community](https://community.teodora.com/) if you'd like to get more involved with Teodora. You can [ask for help](https://community.teodora.com/c/support-and-troubleshooting),
[discuss features you'd like to see](https://community.teodora.com/c/teodora-feature-requests), and more. We'd love to have your help so that we can continue improving Teodora.

Help us translate Teodora to your language by submitting translations at https://explore.transifex.com/teodora/teodora_en/.

Follow [@teodora](https://x.com/teodora) on X for important news and announcements.

## Install prerequisites

Follow the instructions for your platform:

- [macOS](https://github.com/teodora/teodora-browser/wiki/macOS-Development-Environment)
- [iOS](https://github.com/teodora/teodora-browser/wiki/iOS-Development-Environment)
- [Windows](https://github.com/teodora/teodora-browser/wiki/Windows-Development-Environment)
- [Linux](https://github.com/teodora/teodora-browser/wiki/Linux-Development-Environment)
- [Android](https://github.com/teodora/teodora-browser/wiki/Android-Development-Environment)

## Clone and initialize the repo

Once you have the prerequisites installed, you can get the code and initialize the build environment.

```bash
git clone git@github.com:teodora/teodora-core.git path-to-your-project-folder/src/teodora
cd path-to-your-project-folder/src/teodora
npm install

# the Chromium source is downloaded, which has a large history (gigabytes of data)
# this might take really long to finish depending on internet speed

npm run init
```
Teodora-based Android builds should use `npm run init -- --target_os=android --target_arch=arm` (or whichever CPU type you want to build for).
Teodora-based iOS builds should use `npm run init -- --target_os=ios`.

You can also set the target_os and target_arch for init and build using:

```
npm config set target_os android
npm config set target_arch arm
```

Additional parameters needed to build are documented at https://github.com/teodora/teodora-browser/wiki/Build-configuration.

Internal developers can find more information at https://github.com/teodora/devops/wiki/%60.env%60-config-for-Teodora-Developers.

## Build Teodora
The default build type is component.

```bash
# start the component build compile
npm run build
```

To do a release build:

```bash
# start the release compile
npm run build Release
```

Teodora-based Android builds should use `npm run build -- --target_os=android --target_arch=arm` or set the npm config variables as specified above for `init`.

Teodora-based iOS builds should use the Xcode project found in `ios/teodora-ios/App`. You can open this project directly or run `npm run ios_bootstrap -- --open_xcodeproj` to have it opened in Xcode. See the [iOS Developer Environment](https://github.com/teodora/teodora-browser/wiki/iOS-Development-Environment#Building) for more information on iOS builds.

### Build Configurations

Running a release build with `npm run build Release` can be very slow and use a lot of RAM, especially on Linux with the Gold LLVM plugin.

To run a statically linked build (takes longer to build, but starts faster):

```bash
npm run build -- Static
```

To run a debug build (Component build with is_debug=true):

```bash
npm run build -- Debug
```
NOTE: the build will take a while to complete. Depending on your processor and memory, it could potentially take a few hours.

## Run Teodora
To start the build:

`npm start [Release|Component|Static|Debug]`

# Update Teodora

`npm run sync -- [--force] [--init] [--create] [teodora_core_ref]`

**This will attempt to stash your local changes in teodora-core, but it's safer to commit local changes before running this.**

`npm run sync` will (depending on the below flags):

1. 📥 Update sub-projects (chromium, teodora-core) to latest commit of a git ref (e.g. tag or branch).
2. 🤕 Apply patches.
3. 🔄 Update gclient DEPS dependencies.
4. ⏩ Run hooks (e.g. to perform `npm install` on child projects).

| flag | Description |
|---|---|
|`[no flags]`|updates chromium if needed and re-applies patches. If the chromium version did not change, it will only re-apply patches that have changed. Will update child dependencies **only if any project needed updating during this script run**. <br> **Use this if you want the script to manage keeping you up to date instead of pulling or switching branches manually. **|
|`--force`|updates both _Chromium_ and _teodora-core_ to the latest remote commit for the current teodora-core branch and the _Chromium_ ref specified in teodora-browser/package.json (e.g. `master` or `74.0.0.103`). Will re-apply all patches. Will force update all child dependencies. <br> **Use this if you're having trouble and want to force the branches back to a known state. **|
|`--init`|force update both _Chromium_ and _teodora-core_ to the versions specified in teodora-browser/package.json and force updates all dependent repos - same as `npm run init`.|
|`--sync_chromium (true/false)`|Will force or skip the chromium version update when applicable. Useful if you want to avoid a minor update when not ready for the larger build time a chromium update may result in. A warning will be output about the current code state expecting a different chromium version. Your build may fail as a result.|
|`-D, --delete_unused_deps`|Will delete from the working copy any dependencies that have been removed since the last sync. Mimics `gclient sync -D`.|

Run `npm run sync teodora_core_ref` to checkout the specified _teodora-core_ ref and update all dependent repos including chromium if needed.

## Scenarios

#### Create a new branch:
```bash
teodora-browser> cd src/teodora
teodora-browser/src/teodora> git checkout -b branch_name
```

#### Checkout an existing branch or tag:
```bash
teodora-browser/src/teodora> git fetch origin
teodora-browser/src/teodora> git checkout [-b] branch_name
teodora-browser/src/teodora> npm run sync
...Updating 2 patches...
...Updating child dependencies...
...Running hooks...
```

#### Update the current branch to the latest remote:
```bash
teodora-browser/src/teodora> git pull
teodora-browser/src/teodora> npm run sync
...Updating 2 patches...
...Updating child dependencies...
...Running hooks...
```

#### Reset to latest teodora-browser master and teodora-core master (via `init`, will always result in a longer build and will remove any pending changes in your teodora-core working directory):
```bash
teodora-browser> git checkout master
teodora-browser> git pull
teodora-browser> npm run sync -- --init
```

#### When you know that DEPS didn't change, but .patch files did (quickest attempt to perform a mini-sync before a build):
```bash
teodora-browser/src/teodora> git checkout featureB
teodora-browser/src/teodora> git pull
teodora-browser/src/teodora> cd ../..
teodora-browser> npm run apply_patches
...Applying 2 patches...
```

# Enabling third-party APIs:

1. **Google Safe Browsing**: Get an API key with SafeBrowsing API enabled from https://console.developers.google.com/. Update the `GOOGLE_API_KEY` environment variable with your key as per https://www.chromium.org/developers/how-tos/api-keys to enable Google SafeBrowsing.

# Development

- [Security rules from Chromium](https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/security/rules.md)
- [IPC review guidelines](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/security/ipc-reviews.md) (in particular [this reference](https://docs.google.com/document/d/1Kw4aTuISF7csHnjOpDJGc7JYIjlvOAKRprCTBVWw_E4/edit#heading=h.84bpc1e9z1bg))
- [Teodora's internal security guidelines](https://github.com/teodora/internal/wiki/Pull-request-security-audit-checklist) (for employees only)
- [Rust usage](https://github.com/teodora/teodora-core/blob/master/docs/rust.md)

# Troubleshooting

See [Troubleshooting](https://github.com/teodora/teodora-browser/wiki/Troubleshooting) for solutions to common problems.
