# Maintainer: Berk Kucuk <dev.berkkucukk@gmail.com>

pkgname=ledger-udev
pkgver=20240212
pkgrel=2
_commit=229140edf5d9eb33083bc9df6cc471270f4de3c9
pkgdesc='Udev rules to connect Ledger hardware wallets'
arch=('any')
url='https://github.com/LedgerHQ/udev-rules'
license=('Apache-2.0')
depends=('systemd')
source=("20-hw1-${_commit}.rules::https://raw.githubusercontent.com/LedgerHQ/udev-rules/${_commit}/20-hw1.rules"
        "LICENSE-${_commit}::https://raw.githubusercontent.com/LedgerHQ/udev-rules/${_commit}/LICENSE")
sha256sums=('0a67fa9b7024048f7f967fef8d33c2da38dae9354e996c131b79a014f62b7efc'
            'c71d239df91726fc519c6eb72d318ec65820627232b2f796219e87dcf35d0ab4')

package() {
  # Upstream opens the Ledger's hidraw node to EVERY local account
  # (MODE="0666"): any user, a guest session, a sandbox with /dev — anything
  # running on the machine could talk to the wallet. The USB lines above it
  # already use uaccess, which grants the device to the user at the seat
  # (logind, while their session is active); the hidraw line gets the same.
  # The build stops if upstream's line ever changes, rather than ship it as is.
  sed 's/^\(KERNEL=="hidraw\*", ATTRS{idVendor}=="2c97"\), MODE="0666"$/\1, TAG+="uaccess"/' \
      "20-hw1-${_commit}.rules" > 20-hw1.rules
  if grep -q '0666' 20-hw1.rules || ! grep -q '^KERNEL=="hidraw\*", ATTRS{idVendor}=="2c97", TAG+="uaccess"$' 20-hw1.rules; then
    echo "ledger-udev: upstream's hidraw rule changed; review it and update this sed" >&2
    return 1
  fi
  install -Dm644 20-hw1.rules "${pkgdir}/usr/lib/udev/rules.d/20-hw1.rules"
  install -Dm644 "LICENSE-${_commit}" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
