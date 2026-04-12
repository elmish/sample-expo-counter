# Expo counter sample

An [Elmish](https://elmish.github.io/elmish/) counter app running on [Expo](https://expo.dev/), using [Fable](https://fable.io/) to compile F# to JavaScript.

## Pre-requisites

1. [.NET SDK](https://dotnet.microsoft.com/download) (8.0+)
2. [Node.js](https://nodejs.org/) (>= 22.11.0)
3. For device/simulator testing:
   - **iOS**: Xcode
   - **Android**: Android Studio, Android SDK

## Setup

```sh
npm install
dotnet tool restore
```

## Build & Run

1. `npm run watch` — starts Fable in watch mode, recompiling F# to JS on save
2. In a separate terminal: `npm start` — starts Expo dev server

Scan the QR code with Expo Go (Android) or Camera app (iOS) to run on a device, or press `i` for iOS simulator / `a` for Android emulator.

## Scripts

| Script | Command |
|--------|---------|
| `build` | One-shot Fable compile (release) |
| `watch` | Fable watch mode (debug) |
| `start` | Start Expo dev server |
| `ios` | Build and run on iOS |
| `android` | Build and run on Android |

## Tooling

| Tool | Version |
|------|---------|
| Expo SDK | 55 |
| React Native | 0.83.4 |
| Fable | 4.29.0 (local tool via `dotnet-tools.json`) |
| Fable.Elmish | 5.0.2 |
| Fable.React.Native | 4.0.0 |

## Project structure

- `src/App.fs` — Elmish model, update, and view (uses `Program.withExpo`)
- `src/Styles.fs` — React Native styles
- `src/app.fsproj` — F# project with NuGet package references
- `out/` — Fable-compiled JavaScript output (gitignored)
- `assets/` — App icons and splash screen images
- `shims/empty.js` — Stub for unused optional Fable.ReactNative dependencies
- `app.json` — Expo configuration
- `metro.config.js` — Metro bundler configuration (includes shims for unused RN packages)

## Key difference from bare React Native

This sample uses `Elmish.Expo.Program.withExpo` instead of `Elmish.ReactNative.Program.withReactNative`. This integrates with Expo's `registerRootComponent` which provides:

- Expo dev tools overlay
- Proper web platform rendering support
- `Expo.fx` side-effect initialization

No `index.js` entry point is needed — Expo reads the `"main"` field from `package.json` which points directly to the Fable-compiled output.
