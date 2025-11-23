# Klecks Electron App

This document explains how to run and build Klecks as an Electron desktop application.

## What Was Set Up

The following changes were made to convert Klecks to an Electron app:

1. **Installed Electron dependencies** - Added `electron` and `electron-builder` to devDependencies
2. **Created Electron main process** - Added `electron/main.js` with window management and menu
3. **Created Electron package.json** - Added `electron/package.json` to specify the main entry point
4. **Updated scripts** - Added npm scripts for running and building the Electron app
5. **Fixed base href** - Changed from `/` to `./` in `src/index.html` for local file loading
6. **Added electron-builder config** - Configured build settings for macOS, Windows, and Linux
7. **Updated .gitignore** - Added `release/` folder to ignore Electron build outputs

## Prerequisites

- Node.js and npm installed
- All dependencies installed via `npm install` (or `npm ci` from package-lock.json)
- Language files generated via `npm run lang:build`
- Web app built via `npm run build`

## Development

To run Klecks as an Electron app in development mode:

### Option 1: Manual (two terminals)

Terminal 1 - Start the Parcel dev server:
```bash
npm run start
```

Terminal 2 - Start Electron (after dev server is running):
```bash
npm run electron:dev
```

### Option 2: Automatic (single command)

```bash
npm run electron:start
```

This starts both the Parcel dev server and Electron automatically.

## Building for Production

### Build the web app and package as Electron app

```bash
npm run electron:package
```

This will:
1. Generate language files
2. Build the web app with Parcel
3. Package it as an Electron app for your current platform

The built application will be in the `release/` directory.

### Build without language generation

If you've already generated language files:

```bash
npm run electron:build
```

## Platform-Specific Builds

By default, electron-builder builds for your current platform. To build for other platforms:

```bash
# Build for macOS
electron-builder --mac

# Build for Windows
electron-builder --win

# Build for Linux
electron-builder --linux
```

## Distribution Files

After building, you'll find installer/package files in the `release/` directory:

- **macOS**: `.dmg` and `.zip` files
- **Windows**: `.exe` installer
- **Linux**: `.AppImage` and `.deb` packages

## Features

The Electron app includes:

- Native window with menu bar
- Undo/Redo keyboard shortcuts
- Copy/Paste support
- Full WebGL support
- Developer tools (View > Toggle Dev Tools)
- Native file system access (same as browser version)

## Quick Start

To get started quickly with the Electron app:

```bash
# 1. Install dependencies (if not already done)
npm install

# 2. Generate language files
npm run lang:build

# 3. Build the web app
npm run build

# 4. Run in production mode (loads from dist/)
npm run electron:dev
```

Or, for development with hot reload:

```bash
# Terminal 1: Start Parcel dev server
npm run start

# Terminal 2: Start Electron (pointing to dev server)
npm run electron:dev
```

## Notes

- The app uses the same codebase as the web version
- All browser features (IndexedDB, localStorage, WebGL) work identically
- The base href has been changed to `./` to support local file loading
- When running in development mode with `npm run electron:start`, it may take a few seconds for the dev server to start before Electron launches
