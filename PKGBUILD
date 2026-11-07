# Maintainer: broski606 <204181225+broski606@users.noreply.github.com>
pkgname=epic-games-launcher-bin
pkgver=0.113.0+g2164614
pkgrel=1
pkgdesc="Epic Games Launcher (Linux Preview), repackaged from the official .deb"
arch=('x86_64')
url="https://launcher.epicgames.com"
license=('LicenseRef-custom')
depends=('glibc' 'gcc-libs' 'webkit2gtk-4.1' 'gtk3' 'libayatana-appindicator'
         'libsoup3' 'glib2' 'cairo' 'gdk-pixbuf2' 'libx11' 'dbus')
provides=('epic-games-launcher')
conflicts=('epic-games-launcher')
options=('!strip' '!debug')
noextract=("EpicGamesLauncher-${pkgver}-x86_64.deb")
source=("EpicGamesLauncher-${pkgver}-x86_64.deb::https://launcher-public-service-prod06.ol.epicgames.com/launcher/api/installer/download/EpicGamesLauncher-x86_64.deb")
sha256sums=('884def8de247bc279bea571be6f5dec6c5481ac94cc06af62b577624be56c201')

package() {
    # Extrair o data.tar.* do .deb diretamente para o pkgdir
    bsdtar -xOf "EpicGamesLauncher-${pkgver}-x86_64.deb" 'data.tar.*' \
        | bsdtar -xf - -C "$pkgdir" --no-same-owner

    # Avisos de licenças de terceiros
    install -Dm644 "$pkgdir/usr/lib/epic-games-launcher/resources/ThirdPartyNotices.txt" \
        "$pkgdir/usr/share/licenses/$pkgname/ThirdPartyNotices.txt"
}
