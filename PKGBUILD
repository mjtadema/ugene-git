# Original Maintainer: Jens Staal <staal1978@gmail.com>
# Maintainer Matthijs Tadema
pkgname=ugene-git
pkgver=33.0.r1278.g66df81b73e
pkgrel=1
pkgdesc="A free cross-platform genome analysis suite."
arch=('x86_64')
url="http://ugene.unipro.ru/"
license=('GPL')
depends=('libxtst' 'glu' 'qt5-webkit' 'qt5-websockets' 'qt5-svg' 'qt5-script' 'desktop-file-utils')
provides=('ugene' 'ugene-bin')
conflicts=('ugene' 'ugene-bin')
replaces=('ugene' 'ugene-bin')
source=('ugene::git+https://github.com/ugeneunipro/ugene.git'
        'qpainter.patch')
sha256sums=('SKIP'
            'fef4529c776102017d33ce98378f0f7bebb4b25f2a343c392fe27dfcc8e3e9e9')

build() {
  cd "${srcdir}"/ugene
  #make sure that the wanted branch is active
  git checkout master
  qmake CONFIG+=x64 PREFIX=/usr -r
  make
}

prepare() {
    cd "${srcdir}"/ugene
    patch --forward --strip=1 --input="${srcdir}/qpainter.patch"
}

pkgver() {
  cd "${srcdir}"/ugene
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/; s/-/./g'
}

package() {
  cd "${srcdir}"/ugene
  make INSTALL_ROOT="$pkgdir" install
}

post_install() {
  update-desktop-database -q
}
post_remove() {
  update-desktop-database -q
}
 
