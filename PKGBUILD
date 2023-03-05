pkgname=microsoft-edge-stable
_pkgname=microsoft-edge-stable-bin
_pkgshortname=msedge
pkgver=110.0.1587.63
pkgrel=1
pkgdesc="A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier"
arch=('x86_64')
url="https://www.microsoftedgeinsider.com/en-us/download"
license=('custom')
provides=()
conflicts=()
depends=('gtk3' 'libcups' 'nss' 'alsa-lib' 'libxtst' 'libdrm' 'mesa')
makedepends=('imagemagick')
optdepends=(pipewire kdialog kwallet ttf-liberation xdg-utils)
options=(!strip !zipman)
_channel=stable
source=("https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-stable/${pkgname}_${pkgver}-1_amd64.deb"
	"https://raw.githubusercontent.com/KaOS-Community-Packages/microsoft-edge-stable/main/microsoft-edge-stable.sh"
	"https://github.com/KaOS-Community-Packages/microsoft-edge-stable/raw/main/Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf")
sha256sums=('SKIP'
	    'SKIP'
	    'SKIP')

package() {
	bsdtar -xf data.tar.xz -C "$pkgdir/"

	# suid sandbox
	chmod 4755 "${pkgdir}/opt/microsoft/${_pkgshortname}/msedge-sandbox"

	# 256 and 24 are proper colored icons
	for res in 128 64 48 32; do
		convert "${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_256.png" \
			-resize ${res}x${res} \
			"${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png"
	done
	for res in 22 16; do
		convert "${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_24.png" \
			-resize ${res}x${res} \
			"${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png"
	done

	# install icons
	for res in 16 22 24 32 48 64 128 256; do
		install -Dm644 "${pkgdir}/opt/microsoft/${_pkgshortname}/product_logo_${res}.png" \
			"${pkgdir}/usr/share/icons/hicolor/${res}x${res}/apps/${pkgname}.png"
	done
       # User flag aware launcher
       install -m755 microsoft-edge-stable.sh "${pkgdir}/usr/bin/microsoft-edge-stable"

	# License
	install -Dm644 'Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf' "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.pdf"
	rm -r "${pkgdir}/etc/cron.daily/" "${pkgdir}/opt/microsoft/${_pkgshortname}/cron/"
	# Globbing seems not to work inside double parenthesis
	rm "${pkgdir}/opt/microsoft/${_pkgshortname}"/product_logo_*.png
}
