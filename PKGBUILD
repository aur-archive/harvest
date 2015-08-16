# Maintainer: Magnus Bjerke Vik <mbvett at gmail dot com>
pkgname=harvest
pkgver=1.18
pkgrel=2
pkgdesc="Harvest: Massive Encounter is an rts game with battles of epic proportions."
arch=('i686' 'x86_64')
url="http://www.oxeyegames.com/harvest/"
license=('custom')
depends=('sfml' 'luajit' 'nvidia-cg-toolkit' 'freealut' 'libvorbis' 'gtk2' 'libjpeg6')
makedepends=('tar')
source=('harvest'
	'harvest.desktop'
	'harvest.png')
md5sums=('8424951b7f63697364bf5d744ec4d76d'
         '3157bf55bf86865e93560f6cb9c42bf1'
         'f9ab1cb5466cbf1738581443463c5d52')

_source_arch="i386"
[ "$CARCH" = "x86_64" ] && _source_arch="amd64"

_gamepkg="Harvest-${pkgver}_${_source_arch}.tar.gz"

package() {
	if [ ! -f ${startdir}/${_gamepkg} ]; then
		error "Could not find \"$_gamepkg\". Place the package or a symlink in \"$startdir/\", or specify the absolute path to the package here:"
		read _pkgpath
		if [ -f "${startdir}/${_gamepkg}" ]; then
			ln -sf "${startdir}/${_gamepkg}" $_gamepkg
		elif [ -f "${_pkgpath}${_gamepkg}" ]; then
			ln -sf "${_pkgpath}${_gamepkg}" $_gamepkg
		else
			error "Could not find ${_pkgpath}${_gamepkg}"
			return 1
		fi
	else
		ln -sf "${startdir}/${_gamepkg}" $_gamepkg
	fi

	tar -zxf $_gamepkg -C $srcdir

	install -D -m755 harvest $pkgdir/usr/bin/harvest

	install -d $pkgdir/opt/harvest/
	rm -R Harvest/run_harvest Harvest/bin/
	cp -r Harvest/* $pkgdir/opt/harvest/

	install -D -m644 harvest.png $pkgdir/usr/share/pixmaps/harvest.png

	install -D -m644 harvest.desktop $pkgdir/usr/share/applications/harvest.desktop
}
