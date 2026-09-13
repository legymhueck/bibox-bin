# Maintainer: MicLeh <micleh at proton dot me>
pkgname=bibox-bin
pkgver=8.4.0
pkgrel=1
pkgdesc="Official client for Westermann textbooks"
arch=('x86_64')
url="https://www.bibox.schule"
license=('custom')
# inetutils - prevent /bin/sh: line 1: hostname: command not found
depends=('org.freedesktop.secrets' 'gtk3' 'ffmpeg' 'pango' 'inetutils')
source=("${pkgname}-${pkgver}.deb::https://static.bibox2.westermann.de/apps/linux-deb")
noextract=("${pkgname}-${pkgver}.deb")
b2sums=('b9b862332d4478cd16fdbc06a0c880e1ae0e979dd70b2891172ce07e4109c7f6dc55e44837ddf34e39a260d4bac69a72b09df30876e9730aeb7bafc39357f5d2')

prepare() {
    ar x "${pkgname}-${pkgver}.deb"
    tar -xf data.tar.xz
    
    # normalize upstream install path
    mv opt/BiBox opt/bibox
}

package() {
    mkdir -p "${pkgdir}/opt/bibox"
    cp -a "opt/bibox/." "${pkgdir}/opt/bibox/"

    install -d "${pkgdir}/usr/bin"
    cat > "${pkgdir}/usr/bin/bibox" << 'EOF'
#!/bin/sh

# Upstream checks APPIMAGE and logs a warning when unset.
export APPIMAGE="/opt/bibox/bibox"

exec /opt/bibox/bibox "$@"
EOF
    chmod 755 "${pkgdir}/usr/bin/bibox"

    install -Dm644 usr/share/applications/BiBox.desktop "${pkgdir}/usr/share/applications/bibox.desktop"
    sed -i 's|Icon=/usr/share/icons/hicolor/0x0/apps/bibox2.png|Icon=/usr/share/icons/hicolor/1024x1024/apps/bibox.png|g' "${pkgdir}/usr/share/applications/bibox.desktop"

    # Point desktop launcher to package-managed wrapper.
    sed -i 's|Exec=/opt/BiBox/bibox %U|Exec=/usr/bin/bibox %U|g' "${pkgdir}/usr/share/applications/bibox.desktop"

    install -Dm644 usr/share/icons/hicolor/1024x1024/apps/bibox.png "${pkgdir}/usr/share/icons/hicolor/1024x1024/apps/bibox.png"
}
