<div align="center">
  <br/>
  <img 
    src="android/app/src/main/res/mipmap-xxxhdpi/ic_launcher_round.webp" width="140" 
  />

  <h3>GitSync Unlocked</h3>
  <h4>Mobile git client for syncing a repository between remote and a local directory</h4>

  <p align="center">
    <a href="#"><img src="https://img.shields.io/github/license/shubham-sharma-1994/GitSync-Unlocked?v=1" alt="license"></a>
    <a href="#"><img src="https://img.shields.io/github/last-commit/shubham-sharma-1994/GitSync-Unlocked?v=1" alt="last commit"></a>
    <a href="#"><img src="https://img.shields.io/github/stars/shubham-sharma-1994/GitSync-Unlocked?v=1" alt="stars"></a>
    <a href="https://github.com/sponsors/ViscousPot"><img src="https://img.shields.io/static/v1?label=Sponsor%20the%20original%20dev&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86" alt="sponsor"></a>
  <br>
    <a href="https://gitsync.viscouspotenti.al/wiki"><img alt="Wiki" src="https://img.shields.io/badge/wiki-white?style=for-the-badge"></a>
 </p>

  <br />

</div>

> **This is an unofficial fork of [ViscousPot/GitSync](https://github.com/ViscousPot/GitSync).** The upstream app requires a GitHub-sponsor "Premium" unlock to manage more than one repository container, add discovered submodules automatically, or import a settings backup covering multiple repositories. This fork removes that gate entirely — along with the paywall screen and every button that led to it — so those are available immediately, no sponsorship required. (The premium page also advertised Git LFS, git-crypt filters and pre-commit hooks as upcoming; those were never built in either version, so this fork doesn't change anything there.)
>
> This fork is **not published on the Play Store, App Store, F-Droid, or IzzyOnDroid** — those listings are the official app, which still has the premium tier. To get the unlocked build, [build it yourself](#build-instructions) from this repository. It carries the same GPLv3 license as upstream and is not affiliated with or endorsed by the original developer; if you find the underlying app useful, consider supporting them directly via the sponsor link above.

GitSync is a cross-platform git client for Android and iOS that aims to simplify the process of syncing a folder between a git remote and a local directory. It works in the background to keep your files synced with a simple one-time setup and a range of options for activating manual syncs.

| ![Seamless Git File Sync](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/01.png) | ![Resolve Merge Conflicts on Mobile](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/02.png) | ![Connect any Git Provider](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/03.png) | ![Sync in the Background](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/04.png) | ![Manage it All](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/05.png) | ![Trusted by Developers](https://github.com/ViscousPot/GitSync/blob/main/fastlane/metadata/android/en-GB/images/phoneScreenshots/06.png) |
|---|---|---|---|---|---|

- **Supports Android 5+ & iOS 13+**
- Authenticate with
  - **HTTP/S**
  - **SSH**
  - **OAuth** (GitHub, GitLab, Gitea)
- Clone a remote repository
- Sync repository
  - Fetch, pull, stage, commit, push
  - Resolve merge conflicts
  - Retry automatically when the network returns
- Sync mechanisms
  - When an app is opened or closed (Android)
  - On a recurring schedule
  - From a quick tile (Android)
  - From a home screen widget
  - From an iOS shortcut or automation
  - From a custom intent (advanced)
- Browse and edit in-app
  - File explorer with code editor and image viewer
  - Recent commits, plus file, line and commit diffs
  - Branch management (create, rename, delete, checkout)
  - Multiple remotes (add, rename, delete, set URL)
- GitHub and GitLab integration (when signed in via OAuth)
  - View, comment on and create issues
  - View, comment on and create pull requests
  - View workflow runs (GitHub Actions)
- AI features
  - Chat about your repository
  - Wand auto-complete on text fields like commit messages
  - Agent that can run repo actions for you
  - Separate model selection for chat, tools and the wand
  - A global toggle to hide all AI features
- **Manage unlimited repositories with containers** (no cap — upstream limits non-sponsors to one)
- Repository settings
  - Signed commits
  - Customisable sync commit messages
  - Author details
  - Edit `.gitignore` and `.git/info/exclude`
  - Disable SSL verification per repo
- **No sponsor unlock required** for any of the above, including managing more than one repository container

More information can be found at the [wiki](https://gitsync.viscouspotenti.al/wiki)
<br>
If you find this fork useful, a ⭐ here is appreciated — and if you like GitSync itself, consider starring [the original project](https://github.com/ViscousPot/GitSync) too.

## Support

This is an unofficial fork; for issues with building or running this fork specifically, open an issue in this repository. For bugs in the underlying GitSync app itself, email bugs.viscouspotential@gmail.com or use the [upstream repository](https://github.com/ViscousPot/GitSync).

## Build Instructions

This fork isn't distributed as a prebuilt release, so building it is the only way to run it. If you'd rather just try GitSync without building anything, the [official app](https://github.com/ViscousPot/GitSync#readme) is available on the Play Store, App Store, F-Droid and IzzyOnDroid — note that it still has the premium tier this fork removes.

You don't need a local toolchain to get an APK, though — the [**Build APK**](.github/workflows/build-apk.yml) GitHub Actions workflow builds one on every push to `main`, and can also be run on demand from this repo's Actions tab (`Run workflow`). Grab the signed APKs from the finished run's Artifacts section. It works with no configuration, though installs from consecutive runs won't be able to update over each other until you add `RELEASE_KEYSTORE_BASE64`, `RELEASE_SIGNING_ALIAS` and `RELEASE_SIGNING_PASSWORD` repo secrets — the same ones [`generate-apk-release.yml`](.github/workflows/generate-apk-release.yml) uses for tagged releases — at which point it signs with that key instead.

To build locally instead:

GitSync is a Flutter app with a Rust core (via [`flutter_rust_bridge`](https://github.com/fzyzcjy/flutter_rust_bridge)).

### 1. Prerequisites

- **Flutter**: version pinned in [`.fvmrc`](.fvmrc) (currently 3.35.2). The repo is set up for [FVM](https://fvm.app/); install with `dart pub global activate fvm` and then `fvm install`.
- **Rust**: stable toolchain via [rustup](https://rustup.rs/). The Rust crate lives in [`rust/`](rust/).
- **Android**: Android Studio with a recent SDK (compileSdk follows Flutter, minSdk 21). The Rust crate cross-compiles to `aarch64`, `armv7`, `x86_64` and `i686` targets, which you can add via `rustup target add`.
- **iOS**: Xcode 15+ on macOS, the `aarch64-apple-ios`, `aarch64-apple-ios-sim` and `x86_64-apple-ios` Rust targets, and CocoaPods.

### 2. Clone & install

```bash
git clone https://github.com/shubham-sharma-1994/GitSync-Unlocked.git
cd GitSync-Unlocked
fvm flutter pub get
```

### 3. OAuth secrets

OAuth providers (GitHub, GitLab, Gitea) need client IDs/secrets. The repo ships a template:

```bash
cp lib/constant/secrets.dart.template lib/constant/secrets.dart
```

Set `oauthRedirectUrl = "gitsync://auth"`. Without these the OAuth sign-in flows won't work, but HTTPS Basic and SSH still do.

### 4. Generate the Rust ↔ Dart bindings

The bridge is regenerated when the Rust API changes:

```bash
cargo install flutter_rust_bridge_codegen --version 2.12.0
flutter_rust_bridge_codegen generate
```

### 5. Run

```bash
fvm flutter run
```

## Contributing

This fork exists mainly for personal/self-built use, so contributions here are informal. If you find GitSync itself useful:

- Star the [original repo](https://github.com/ViscousPot/GitSync) to help others discover it
- Share it with friends or communities that might benefit
- Consider becoming a [GitHub Sponsor](https://github.com/sponsors/ViscousPot) of the original developer

<br>
At this time, code contributions aren’t needed anywhere in particular, but I’d love your help improving <strong><a href="#localization-contributions">localization</a></strong>

<details>
<summary><h3 style="display:inline-block;">Localization Contributions</h3></summary>

If you’d like to contribute translations:

1. Locate the **English strings** in `lib/l10n/app_en.arb`
2. Find the corresponding language file (e.g. `lib/l10n/app_es.arb` for Spanish)
3. Add or refine translations in the appropriate file
4. Submit a pull request or open an issue with your suggestions

Currently supported languages:

- English (`app_en.arb`, the source file)
- Arabic (`app_ar.arb`)
- Chinese, Simplified (`app_zh.arb`)
- Chinese, Traditional (`app_zh_Hant.arb`, early stage)
- French (`app_fr.arb`)
- German (`app.de.arb`)
- Japanese (`app_ja.arb`)
- Russian (`app_ru.arb`)
- Spanish (`app_es.arb`)

If you'd like to know what's still untranslated for a given locale, see [`untranslated.txt`](untranslated.txt). Even small improvements to wording or grammar are welcome.

</details>

## Acknowledgements

- [ViscousPot/GitSync](https://github.com/ViscousPot/GitSync) — the original app this fork is based on
- [flutter_rust_bridge](https://github.com/fzyzcjy/flutter_rust_bridge)
- [git2-rs](https://github.com/rust-lang/git2-rs)
