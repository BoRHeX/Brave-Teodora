![Teodora Browser](./docs/source/_static/Teodora.svg)

## Overview

Teodora is a decentralized, AI-driven browser built upon the Brave framework. It integrates the Lightweb AI interface for seamless interaction with Web3 applications, delivering a secure, private, and intuitive browsing experience. Teodora extends Brave's core principles with advanced AI tools, decentralized technologies, and a minimalist design.

Key features include:
  - **Lightweb AI Interface**: Real-time data analysis, personalized suggestions, and automated blockchain interactions.
  - **Web3 Wallet Integration**: Seamless compatibility with Brave Wallet and MetaMask for blockchain interactions.
  - **Minimalist UI**: A modern, responsive design optimized for quick onboarding and intuitive navigation.
  - **Enhanced Privacy and Security**: Advanced encryption and decentralized interaction safeguards.

## Downloads

Visit [teodora.com/download](https://teodora.com/download) to get the latest stable release.

## Contributing

See the [contributing guidelines](./CONTRIBUTING.md) for details on how to contribute to Teodora.

Our [Wiki](https://github.com/teodora/teodora-browser/wiki) contains additional technical information.

## Community

[Join the Teodora community](https://community.teodora.com/) to get involved. You can [ask for help](https://community.teodora.com/c/support-and-troubleshooting), [suggest features](https://community.teodora.com/c/teodora-feature-requests), and more.

Help us translate Teodora by submitting translations at [Transifex](https://explore.transifex.com/teodora/teodora_en/).

Follow [@teodora](https://x.com/teodora) on X for updates and announcements.

## Install prerequisites

Follow the instructions for your platform:

- [macOS](https://github.com/teodora/teodora-browser/wiki/macOS-Development-Environment)
- [iOS](https://github.com/teodora/teodora-browser/wiki/iOS-Development-Environment)
- [Windows](https://github.com/teodora/teodora-browser/wiki/Windows-Development-Environment)
- [Linux](https://github.com/teodora/teodora-browser/wiki/Linux-Development-Environment)
- [Android](https://github.com/teodora/teodora-browser/wiki/Android-Development-Environment)

## Clone and initialize the repo

```bash
git clone git@github.com:teodora/teodora-core.git path-to-your-project-folder/src/teodora
cd path-to-your-project-folder/src/teodora
npm install
npm run init
```

Teodora-based Android builds should use `npm run init -- --target_os=android --target_arch=arm`. For iOS, use `npm run init -- --target_os=ios`.

## Build Teodora

```bash
npm run build
```

To do a release build:

```bash
npm run build Release
```

For Android builds, use `npm run build -- --target_os=android --target_arch=arm`. For iOS, use the Xcode project in `ios/teodora-ios/App`.

## Run Teodora

```bash
npm start [Release|Component|Static|Debug]
```

## Update Teodora

```bash
npm run sync -- [--force] [--init] [--create] [teodora_core_ref]
```

## Development

- [Security rules](https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/security/rules.md)
- [Teodora's internal security guidelines](https://github.com/teodora/internal/wiki/Pull-request-security-audit-checklist)
- [Rust usage](https://github.com/teodora/teodora-core/blob/master/docs/rust.md)

## Troubleshooting

See [Troubleshooting](https://github.com/teodora/teodora-browser/wiki/Troubleshooting) for solutions to common problems.
