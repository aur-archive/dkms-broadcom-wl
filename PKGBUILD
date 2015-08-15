# Contributor: Jason Melton <jason [dot] melton [at] gmail [dot] com>
# Contributor: Rolando Durán <rozentensai [at] gmail [dot] com>
# Maintainer: Timothy Lee <timothy.ty.lee [at] gmail [dot] com>

pkgname=dkms-broadcom-wl
_pkgname=broadcom-wl
pkgver=5.100.82.112
_vpkgver=5_100_82_112
pkgrel=13
pkgdesc='DKMS-controlled Broadcom 802.11abgn hybrid Linux networking device driver'
url='http://www.broadcom.com/support/802.11/linux_sta.php'
arch=('i686' 'x86_64')
license=('custom')
depends=('dkms')
provides=('broadcom-wl')
conflicts=('broadcom-wl')

[[ $CARCH = x86_64 ]] && ARCH=x86_64 || ARCH=x86_32
source=("http://www.broadcom.com/docs/linux_sta/hybrid-portsrc_${ARCH}-v${_vpkgver}.tar.gz"
	'modprobe.d'
	'license.patch'
	'user-ioctl.patch'
	'linux-recent.patch'
	'uname-r.patch'
	'dkms.conf')
sha1sums=('01aa32f9e85621253a3f15cf4361bb80d41da3e8'
	  '89bf92286ede30dd85304c6c4e42e89cfdc0f60a'
	  'ea7b67982ddc0f56fd3becb9914fd4458fe7d373'
	  'a41f11ffc18dbb126176259e02dd93b6ade04a10'
	  '64f99cde29168e7bd8508af30702c68f907556d9'
	  '5ec2c58f6005f85b36e52297d1c7537100410da0'
	  '4edeafd8fcb41c10f934059503ed6b76f8a432db')
[[ $CARCH = x86_64 ]] && sha1sums[0]='5bd78c20324e6a4aa9f3fafdc6f0155e884d5131'

backup=('etc/modprobe.d/broadcom-wl.conf')
install=install

build() {
	cd "${srcdir}"

	patch -p1 -i uname-r.patch
	patch -p1 -i linux-recent.patch
	patch -p1 -i user-ioctl.patch
	patch -p1 -i license.patch
}

package() {
	cd "${srcdir}"
	
	mkdir -p ${pkgdir}/usr/src/${_pkgname}-${pkgver}

	cp -RL * ${pkgdir}/usr/src/${_pkgname}-${pkgver}
	install -D -m 644 lib/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -D -m 644 modprobe.d "${pkgdir}"/etc/modprobe.d/broadcom-wl.conf
}
