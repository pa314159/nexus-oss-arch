# Maintainer: PAPPY <pappy _AT_ a s c e l i o n _DOT_ com>

_version=3.25.1
_patch=02

pkgname=nexus-oss
pkgver=${_version}.${_patch}
pkgrel=1
pkgdesc='Nexus 3 Repository OSS'
arch=('any')
url='http://nexus.sonatype.org'
license=("custom:$pkgname")
depends=('jre8-openjdk-headless')
replaces=('nexus3')
provides=($pkgname)
backup=("var/lib/$pkgname/etc/nexus.properties"
		"usr/lib/$pkgname/bin/nexus.vmoptions"
		)
#source=("https://sonatype-download.global.ssl.fastly.net/repository/repositoryManager/3/nexus-$_version-$_patch-unix.tar.gz"
source=("https://download.sonatype.com/nexus/3/nexus-$_version-$_patch-unix.tar.gz"
		"$pkgname"
		"$pkgname.install"
		"$pkgname.properties"
		"$pkgname.service"
		"$pkgname.sysusers"
		"$pkgname.tmpfiles"
		"$pkgname.vmoptions"
		"pref_jre.cfg"
		)
sha256sums=('d3a49905e2bac421b7b7d6299312a9c65e194a8c17d994ee83b06c58eafe43e5'
            '3d2ebc2a796dbdc7e7e3b97e4c3272292169c898776e111f503f0517e434caff'
            'f03a4a2a454ab15bbe7b6d479ec4b6a86055a4ffb77704dc44fe11a19382278b'
            'dcdef5614db12f38b3da0b9de1b52fb7fa402af6621a825981c6168a34a6ad9b'
            '3670748854d3f05623c9a8826605c3e2a97c7b3955104e74b5eed00ed17299c1'
            '77d699b5ccf6387fa2f69df2cd71cdb75b4ffbf46a10110dd6c0e2802783dbef'
            '939994095f0c5de005a1e36a295bea791a70dadfa32af23b400cbd87be57af9c'
            '62da3195207e23e6945082cd7898ca1e1f22eb52d0538977ab2caf4d1186d8d8'
            '55fb2aeb4eb3f54c59963870cf43bf5a898a014826d530bf37729fc5e2bc2463')

install=$pkgname.install

package() {
	install -dm755 $pkgdir/usr/lib
	install -dm750 $pkgdir/var/lib/$pkgname

	cp -a $srcdir/nexus-$_version-$_patch $pkgdir/usr/lib/$pkgname
	cp -a $srcdir/sonatype-work/nexus3/orient $pkgdir/var/lib/$pkgname

	pushd $pkgdir/usr/lib/$pkgname
	rm -rf bin/nexus.rc \
		bin/contrib \
		LICENSE.txt
	popd

	install -Dm640 $srcdir/$pkgname.properties $pkgdir/var/lib/$pkgname/etc/nexus.properties

	install -Dm644 $srcdir/nexus-$_version-$_patch/OSS-LICENSE.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
	install -Dm755 $srcdir/$pkgname $pkgdir/usr/bin/$pkgname
	install -Dm644 $srcdir/$pkgname.vmoptions $pkgdir/usr/lib/$pkgname/bin/nexus.vmoptions
	install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
	install -Dm644 $pkgname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
	install -Dm644 $pkgname.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
	install -m644 pref_jre.cfg $pkgdir/usr/lib/$pkgname/.install4j

	chmod -R o-rwx $pkgdir/var/lib/$pkgname
}

