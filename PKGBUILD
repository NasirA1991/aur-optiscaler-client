# Maintainer: Evilleader evilleader91@gmail.com
pkgname=optiscaler-client-bin
pkgver=1.0.6.1
pkgrel=1
pkgdesc="A modern manager for OptiScaler"
arch=('x86_64')
url="https://github.com/Optiscaler-Client/Optiscaler-Client"
license=('GPL3')
depends=('fontconfig' 'libx11' 'libice' 'libsm')
provides=('optiscaler-client')
conflicts=('optiscaler-client')
options=(!strip)
source=(
  "optiscaler-client-${pkgver}.zip::https://github.com/Optiscaler-Client/Optiscaler-Client/releases/download/OptiscalerClient-${pkgver}/OptiscalerClient-${pkgver}-linux-x64.zip"
  "optiscaler-client-${pkgver}.png::https://raw.githubusercontent.com/Optiscaler-Client/Optiscaler-Client/OptiscalerClient-${pkgver}/assets/icon.png"
  "optiscaler-client.desktop"
)
# These are placeholders only. They are overwritten automatically every
# deploy by `updpkgsums: true` in deploy.yml (KSXGitHub/github-actions-deploy-aur).
# Do NOT use 'SKIP' here -- 'SKIP' tells updpkgsums to leave that entry
# untouched, which is exactly the "skipped verification" behavior that got
# flagged. Any non-SKIP placeholder works since it's always replaced.
sha256sums=('PLACEHOLDER'
            'PLACEHOLDER'
            'PLACEHOLDER')

package() {
  mkdir -p "$pkgdir/opt/optiscaler-client"
  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/share/icons/hicolor/256x256/apps"
  bsdtar -xf "optiscaler-client-${pkgver}.zip" -C "$pkgdir/opt/optiscaler-client"
  chmod +x "$pkgdir/opt/optiscaler-client/OptiscalerClient"
  install -Dm755 /dev/stdin "$pkgdir/usr/bin/optiscaler-client" << 'EOF'
#!/bin/bash
exec /opt/optiscaler-client/OptiscalerClient "$@"
EOF
  install -Dm644 optiscaler-client.desktop \
    "$pkgdir/usr/share/applications/optiscaler-client.desktop"
  install -Dm644 "optiscaler-client-${pkgver}.png" \
    "$pkgdir/usr/share/icons/hicolor/256x256/apps/optiscaler-client.png"
}
