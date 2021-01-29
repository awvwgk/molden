# Maintainer: Billy Wayne McCann <thebillywayne ~et~ gmail.com>
# Former Maintainer: Thorsten Bonck <thorsten at bonck.net>
# Former Maintainer: Hector Mtz-Seara <hseara__*a*t*__gmail*.*com>
# Contributor: Anton Bazhenov <anton.bazhenov at gmail>
# Contributor: Michal Bozon <michal.bozon__at__gmail.com>

pkgname=molden
pkgver=5.8
pkgrel=1
pkgdesc="Molecular builder and viewer of quantum chemistry calculations"
arch=('i686' 'x86_64')
url="http://www.cmbi.ru.nl/molden/molden.html"
license=('custom')
install=${pkgname}.install
groups=('science' 'chemistry')
depends=('glu' 'libxmu' 'mesa')
makedepends=('gcc-fortran' 'makedepend')
provides=('molden' 'gmolden' 'ambfor' 'ambmd')
source=(ftp://ftp.cmbi.umcn.nl/pub/molgraph/$pkgname/$pkgname$pkgver.tar.gz
        gcc-10-allow-argument-mismatch.patch)

sha512sums=('8ba16e14f8144f2f829efe01a7ad6570f43b038e47675362b445580b0eed9b533680ba8d62b54c3b5e00215b2d1227211801462e229f038d70ace6c61a04c61a'
            '22c7b925db2e0df05a1f1a7a36d848efd72f13d3e12605143ec52e78768df10756486389b3355df201761ba476376280da78845db56f0899fb4d1c1363c2a620')

# contatenated $pkgname and $pkgver
_pkgnv=${pkgname}${pkgver}


prepare() {
    cd "$srcdir"/$_pkgnv
    patch --forward --strip=1 --input="${srcdir}/gcc-10-allow-argument-mismatch.patch"
}


build() {
    cd "$srcdir"/$_pkgnv
  
    # rename the CopyRight file
    mv -f CopyRight LICENSE
  
    # make
    make molden gmolden ambfor/ambfor ambfor/ambmd || return 1
}

package() {
    # install binaries
    install -m755 -d "$pkgdir"/usr/bin
    install -m755 -t "$pkgdir"/usr/bin "$srcdir"/$_pkgnv/molden
    install -m755 -t "$pkgdir"/usr/bin "$srcdir"/$_pkgnv/gmolden
    install -m755 -t "$pkgdir"/usr/bin "$srcdir"/$_pkgnv/ambfor/{ambfor,ambmd}

    # install licenses 
    install -m755 -d "$pkgdir"/usr/share/licenses/$pkgname
    install -m644 -t "$pkgdir"/usr/share/licenses/$pkgname "$srcdir"/$_pkgnv/COMMERCIAL_LICENSE
    
    # install desktop file and icon
    install -m755 -d "$pkgdir"/usr/share/applications
    install -m644 -t "$pkgdir"/usr/share/applications/ ../$pkgname.desktop
    install -m755 -d "$pkgdir"/usr/share/pixmaps
    install -m644 -t "$pkgdir"/usr/share/pixmaps/ ../$pkgname.png 
}
