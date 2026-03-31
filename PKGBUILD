# Maintainer: MicLeh <micleh at proton dot me>
pkgname=bibox2
pkgver=3.0.4
pkgrel=1
pkgdesc="Official client for Westermann textbooks"
arch=('x86_64')
url="https://www.bibox.schule"
license=('custom')
depends=('org.freedesktop.secrets' 'gtk3' 'ffmpeg' 'pango')
source=("${pkgname}-${pkgver}.deb::https://static.bibox2.westermann.de/apps/linux-deb")
noextract=("${pkgname}-${pkgver}.deb")
b2sums=('c0420801f884beb62fc28f80592ff307fec2d9aa5a331771d6fb44ab65faf928eccce0d4f1a9c172944bc7397e3131fe235b7fa679cfbd2e00654baf06245462')

prepare() {
    ar x "${pkgname}-${pkgver}.deb"
    tar -xf data.tar.xz
}

package() {
    mkdir -p "${pkgdir}/opt/BiBox 2.0"
    cp -a "opt/BiBox 2.0/." "${pkgdir}/opt/BiBox 2.0/"

    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/opt/BiBox 2.0/bibox" "${pkgdir}/usr/bin/bibox"

    install -Dm644 usr/share/applications/bibox.desktop "${pkgdir}/usr/share/applications/bibox.desktop"
    sed -i 's|Icon=/usr/share/icons/hicolor/0x0/apps/bibox2.png|Icon=/usr/share/icons/hicolor/scalable/apps/bibox.png|g' "${pkgdir}/usr/share/applications/bibox.desktop"

    install -Dm644 usr/share/icons/hicolor/0x0/apps/bibox.png "${pkgdir}/usr/share/icons/hicolor/scalable/apps/bibox.png"
}
