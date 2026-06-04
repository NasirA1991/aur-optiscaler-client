# Maintainer: Evilleader evilleader91@gmail.com

pkgname=optiscaler-client-bin
pkgver=1.0.5
pkgrel=4
pkgdesc="Modern desktop client for installing, updating and configuring OptiScaler across game libraries"
arch=('x86_64')
url="https://github.com/Agustinm28/Optiscaler-Client"
license=('MIT')

depends=(
  'glibc'
  'gcc-libs'
)

provides=('optiscaler-client')
conflicts=('optiscaler-client')

source=(
  "optiscaler-client.tar.gz::https://github.com/Agustinm28/Optiscaler-Client/releases/download/OptiscalerClient-${pkgver}/OptiscalerClient-${pkgver}-linux-x64.tar.gz"
  "optiscaler-client.desktop"
)

sha256sums=('SKIP' 'SKIP')

package() {
  mkdir -p "$pkgdir/opt/optiscaler-client"
  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/share/pixmaps"

  # Extract exactly as upstream provides
  bsdtar -xf optiscaler-client.tar.gz -C "$pkgdir/opt/optiscaler-client" --strip-components=1

  # FIXED launcher (NO cd, stable for .NET/Avalonia bundles)
  install -Dm755 /dev/stdin "$pkgdir/usr/bin/optiscaler-client" << 'EOF'
#!/bin/bash
exec /opt/optiscaler-client/OptiscalerClient "$@"
EOF

  # Desktop entry
  install -Dm644 optiscaler-client.desktop \
    "$pkgdir/usr/share/applications/optiscaler-client.desktop"

  # Icon (safe fallback search instead of hardcoded path)
  ICON=""

  for f in \
    "$pkgdir/opt/optiscaler-client/assets/icon.png" \
    "$pkgdir/opt/optiscaler-client/icon.png" \
    "$pkgdir/opt/optiscaler-client/assets/icon.ico"
  do
    if [ -f "$f" ]; then
      ICON="$f"
      break
    fi
  done

  if [ -n "$ICON" ]; then
    install -Dm644 "$ICON" \
      "$pkgdir/usr/share/pixmaps/optiscaler-client.png"
  fi
}
