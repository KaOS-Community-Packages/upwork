pkgname=upwork
pkgver=5.3.3.883
_rawver=${pkgver//./_}
_hashver='1f817bc1fefd44e7'
_pkgupname='Upwork'
pkgrel=1
pkgdesc='Desktop Application'
arch=(x86_64)
url='https://www.upwork.com/downloads/'
license=(custom)
depends=(alsa-lib gtk3 p11-kit libxss nss)
source=(https://updates-desktopapp.upwork.com/binaries/v${_rawver}_${_hashver}/upwork_${pkgver}_amd64.deb
	LICENSE
	upwork)
sha256sums=('9d2778f3ac9171c8e0f8c0677406154e8b1051de7908b9f63204129e8eb65f1c'
            '793d8d7bc0f088c48798bda3d5483972636c6b8c5dcd9aeaf85411f7d4547b38'
            '53bbbd18d7dbbcc27a1405ce9745d95f08be64a234b8fb3312cc2e6ef70e3e9b')

prepare() {
    tar -xJf data.tar.xz
}

package() {
    # Base
    install -dm755 $pkgdir/opt/${_pkgupname}
    cp -dr --no-preserve=ownership opt/Upwork/* $pkgdir/opt/${_pkgupname}/

    # Code ref: https://github.com/electron-userland/electron-builder/blob/master/packages/app-builder-lib/templates/linux/after-install.tpl
    # SUID chrome-sandbox for Electron 5+
    test -e $pkgdir/opt/${_pkgupname}/chrome-sandbox && chmod 4755 $pkgdir/opt/${_pkgupname}/chrome-sandbox || true

    # Exec
    install -dm755 $pkgdir/usr/bin/
    install -Dm755 upwork $pkgdir/usr/bin/

    # Menu
    install -Dm644 usr/share/applications/upwork.desktop $pkgdir/usr/share/applications/$pkgname.desktop

    # Icons
    for size in 16 32 48 64 128 256 512 1024; do
	install -Dm644 "usr/share/icons/hicolor/${size}x${size}/apps/upwork.png" \
		"${pkgdir}/usr/share/icons/hicolor/${size}x${size}/apps/${pkgname}.png"
    done

    # License
    install -Dm644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}