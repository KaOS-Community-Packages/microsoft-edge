pkgname=microsoft-edge
_pkgname=microsoft-edge-stable
__pkgname=msedge
pkgver=123.0.2420.97
pkgrel=1
pkgdesc="A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier"
arch=('x86_64')
url="https://www.microsoft.com/en-us/edge"
license=('custom')
depends=('gtk3' 'libcups' 'nss' 'alsa-lib' 'libxtst' 'libdrm' 'mesa')
makedepends=('imagemagick')
optdepends=('pipewire' 'kdialog' 'kwallet' 'ttf-liberation' 'xdg-utils')
options=('!strip' '!zipman')
install="${pkgname}.install"
source=("${_pkgname}-${pkgver}-${pkgrel}.x86_64.rpm::https://packages.microsoft.com/yumrepos/edge/Packages/m/${_pkgname}-${pkgver}-${pkgrel}.x86_64.rpm"
        "Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf::https://github.com/KaOS-Community-Packages/microsoft-edge-stable/raw/main/Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf")
sha256sums=('SKIP' 'SKIP')

package() {
	msg2 "Unpacking SOURCE files of the downloaded RMP binary package"
	mkdir -p "${pkgdir}/"
	bsdtar -xf "${srcdir}/${_pkgname}-${pkgver}-${pkgrel}.x86_64.rpm" -C "${pkgdir}/"

	install -dm755 "${pkgdir}/usr/bin/"

	msg2 "Removing unnecessary file properties from the RPM binary package"
	rm -vdrf "${pkgdir}/etc/"

	msg2 "Copying thumbnail from SOURCE to the system"
	install -d "${pkgdir}/usr/share/pixmaps/"
	cp -v -a "${pkgdir}/opt/microsoft/${__pkgname}/product_logo_256.png" "${pkgdir}/usr/share/pixmaps/${pkgname}.png"

	msg2 "Installing thumbnails from SOURCE to the system"
	for size in 16x16 32x32 48x48 128x128 256x256; do
		install -Dm644 "${pkgdir}/opt/microsoft/${__pkgname}/product_logo_${size/x*/}.png" \
		"${pkgdir}/usr/share/icons/hicolor/${size}/apps/${pkgname}.png"
	done

	msg2 "Installing Microsoft Edge proprietary LICENSE into the system"
	install -Dm644 "${srcdir}/Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.pdf"

	msg2 "Imposing sandboxing by modifying SUID properties"
	chmod 4755 -v "${pkgdir}/opt/microsoft/${__pkgname}/${__pkgname}-sandbox"

	msg2 "ALL DONE"
}

