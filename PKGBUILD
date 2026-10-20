# Maintainer: Berk Kucuk <dev.berkkucukk@gmail.com>

pkgname=ledger-udev
pkgver=20240212
pkgrel=1
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
  install -Dm644 "20-hw1-${_commit}.rules" "${pkgdir}/usr/lib/udev/rules.d/20-hw1.rules"
  install -Dm644 "LICENSE-${_commit}" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
