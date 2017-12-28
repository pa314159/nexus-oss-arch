# Maintainer: PAPPY <pappy _AT_ a s c e l i o n _DOT_ com>

_version=3.7.0
_patch=04

pkgname=nexus-oss
pkgver=${_version}.${_patch}
pkgrel=1
pkgdesc='Nexus 3 Repository OSS'
arch=('any')
url='http://nexus.sonatype.org'
depends=('jre8-openjdk-headless')
provides=('nexus-oss')
source=("http://download.sonatype.com/nexus/3/nexus-$_version-$_patch-unix.tar.gz"
		"$pkgname"
		"$pkgname.install"
		"$pkgname.service"
		"$pkgname.sysusers"
		"$pkgname.tmpfiles"
		"$pkgname.vmoptions"
		"pref_jre.cfg"
		)
sha256sums=(
		"542912830cb804bc2cad1dc247d28440ecd14edd36684bf8bd55d6999b5e083f"
		"3d2ebc2a796dbdc7e7e3b97e4c3272292169c898776e111f503f0517e434caff"
		"1b5628130205db11429fc26527e38d3cd613f6c00d08cc19d49a6fe9c1a43d06"
		"0fa963f12b4f2d7da4b25cf7027ced34dc73a361e4c8ddc9b939c00faaeb531e"
		"77d699b5ccf6387fa2f69df2cd71cdb75b4ffbf46a10110dd6c0e2802783dbef"
		"32bfa3f82038f89d2f7140eada1faadf416ae835d5e5cb0573c528398249a63e"
		"70ea18f8567b7368c5799141e5f1cd0ca7658d6e4a4d29c52a9288446c7cf341"
		"c55ed8e395f54d2374fd8e5fd3be90a044bd33701ad128e7516e905331b1adcc"
		)

install=$pkgname.install

package() {
	install -dm755 $pkgdir/usr/lib
	install -dm750 $pkgdir/var/lib/$pkgname
	install -dm750 $pkgdir/var/lib/$pkgname/log

	cp -a $srcdir/nexus-$_version-$_patch $pkgdir/usr/lib/$pkgname
	cp -a $srcdir/sonatype-work/nexus3/orient $pkgdir/var/lib/$pkgname

	pushd $pkgdir/usr/lib/$pkgname
	rm -rf bin/nexus.rc \
		bin/contrib \
		LICENSE.txt
	popd

	install -Dm644 $srcdir/nexus-$_version-$_patch/LICENSE.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
	install -Dm755 $srcdir/$pkgname $pkgdir/usr/bin/$pkgname
	install -Dm644 $srcdir/$pkgname.vmoptions $pkgdir/usr/lib/$pkgname/bin/nexus.vmoptions
	install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
	install -Dm644 $pkgname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
	install -Dm644 $pkgname.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
	install -m644 pref_jre.cfg $pkgdir/usr/lib/$pkgname/.install4j
}

