# ledger-udev

The [udev rules](https://github.com/LedgerHQ/udev-rules) from Ledger that let
Ledger hardware wallets be accessed over USB without root, packaged for the
`[mazelinux]` repository. `ledger-live` depends on it.

The package installs `20-hw1.rules` to `/usr/lib/udev/rules.d/`. The rules
file is pinned to an upstream commit and verified by SHA-256; pacman's systemd
hook reloads udev after install, so no reboot is needed. Unplug and reconnect
the device after installing.

> This is an unofficial package. It is not affiliated with or endorsed by
> Ledger SAS.

## Installation

### From the Maze repository

**On Maze Linux** the repository is already configured:

```bash
sudo pacman -S ledger-udev
```

**On Arch Linux and Arch-based distributions**, add the repository once:

1. Import and trust the Maze signing key:

   ```bash
   curl -O https://mazerepo.berkkucukk.com.tr/packages/mazelinux.gpg
   gpg --show-keys --with-fingerprint mazelinux.gpg
   sudo pacman-key --add mazelinux.gpg
   sudo pacman-key --lsign-key 7C4D515A6B930CB04794CEF6147C8159B3E2EE5F
   ```

   The fingerprint `gpg` prints must be `7C4D 515A 6B93 0CB0 4794  CEF6 147C 8159 B3E2 EE5F`.

2. Add the repository to the end of `/etc/pacman.conf`:

   ```ini
   [mazelinux]
   SigLevel = Required DatabaseOptional
   Server = https://mazerepo.berkkucukk.com.tr/packages
   ```

3. Sync and install:

   ```bash
   sudo pacman -Syu ledger-udev
   ```

Optionally install `mazelinux-keyring` as well; it keeps the signing key up to date through pacman.

Remove with `sudo pacman -Rns ledger-udev`.

### Build from source

```bash
sudo pacman -S --needed base-devel git
git clone https://github.com/berk-kucuk/ledger-udev.git
cd ledger-udev
makepkg -si
```

## Updating

`.nvchecker.toml` tracks the latest commit of `LedgerHQ/udev-rules`. To bump
the package, set `_commit` to the new commit, `pkgver` to its date
(`YYYYMMDD`), reset `pkgrel=1`, update the checksums and regenerate
`.SRCINFO`.

## License

The udev rules are © Ledger SAS and released under the Apache License 2.0.
The package installs the license text to
`/usr/share/licenses/ledger-udev/LICENSE`.
