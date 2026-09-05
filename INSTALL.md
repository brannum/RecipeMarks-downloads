# Install RecipeMarks 2.0.1 on Linux

## Choose a package

Use one distribution format for your normal installation. All files in this release target **x86-64 / amd64** Linux desktops. A graphical desktop and the usual Electron runtime libraries are required; minimal/server-only Linux installations may not include them. DEB installation resolves the package's declared dependencies through APT.

Download an installer and `SHA256SUMS` from the [same release](https://github.com/brannum/RecipeMarks-downloads/releases/tag/v2.0.1). Keep them in the same directory.

The desktop runtime is bundled; you do not need to install Python or Node.js.

## Verify your download

In the directory containing the downloaded files, run:

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

The installer you downloaded must report `OK`. The `--ignore-missing` option allows you to download just one package format. A missing-file/no-file-verified result is not a successful verification. If a checksum fails, download the file again before installing it.

## AppImage

Make the file executable, then launch it as your normal desktop user:

```sh
chmod +x RecipeMarks-2.0.1-linux-x86_64.AppImage
./RecipeMarks-2.0.1-linux-x86_64.AppImage
```

You can also use the file manager's permission settings to allow execution and then open the AppImage. Keep it in a permanent folder if you create a desktop shortcut.

### If the AppImage reports missing FUSE

This AppImage needs the **FUSE 2 compatibility library** (`libfuse.so.2`). Ubuntu 24.04 calls this package `libfuse2t64`:

```sh
sudo apt install libfuse2t64
```

Other distributions use different package names. Follow the [official AppImage FUSE instructions](https://docs.appimage.org/user-guide/troubleshooting/fuse.html) for your distribution; installing the compatibility library does not require removing FUSE 3. On Ubuntu/Debian, you can instead use the DEB package.

## DEB: Ubuntu/Debian-based desktops

In the download directory:

```sh
sudo apt install ./RecipeMarks-2.0.1-linux-amd64.deb
```

Then open **RecipeMarks** from your application menu. Run the application as your normal user, not with `sudo`.

## Snap Store

Install the stable release from the [Snap Store](https://snapcraft.io/recipemarks):

```sh
sudo snap install recipemarks
```

Launch RecipeMarks from your application menu as your normal user. Optional removable-media access is disconnected by default; connect it only if you want RecipeMarks to access files on external drives:

```sh
sudo snap connect recipemarks:removable-media
```

## Updates and backups

Before an update, export a backup from RecipeMarks and keep it outside the application's installation folder.

- **AppImage:** download the new version and its checksums, verify them, close the app, and launch the new file. Update any desktop shortcut to point at the new filename. There is no in-app AppImage update promise.
- **DEB:** install the newer DEB with `sudo apt install ./<downloaded-file>.deb`. This installs a local package; this repository does not add an APT repository or promise unattended APT updates.
- **Snap:** keep Store updates enabled. To request an update, use `sudo snap refresh recipemarks`.

Do not clear the app's data to update it. Keep a portable backup before switching formats, uninstalling, or moving to another computer.

## Troubleshooting

If Linux blocks the AppImage's Chromium sandbox, use the DEB package on Ubuntu/Debian and contact support for other distributions. The AppImage does not silently disable its sandbox to work around a host restriction. Do not run the app as root or disable system-wide security settings to make it launch.

Email support@recipemarks.com with the app version, Linux distribution/version, CPU architecture, package format, and error text. Leave out passwords and private note/recipe content.
