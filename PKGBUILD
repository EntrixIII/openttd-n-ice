# Maintainer: entrix <invalid@invalid.org>
# Contributor: HeyCitizen <4637290+InTheMorning@users.noreply.github.com>
# Contributers: Vesa Kaihlavirta <vegai@iki.fi>, Hal Gentz <zegentzy@protonmail.com>
 
pkgname=openttd-nice
_pkgname=openttd
_nice_release=122A
pkgver=12.2
pkgrel=1
pkgdesc='OpenTTD with n-ice patches.'
arch=('x86_64')
url='http://www.n-ice.org/openttd/forum/index.php?topic=609.msg3555'
license=('GPL')
depends=(fluidsynth fontconfig hicolor-icon-theme libpng)
optdepends=('openttd-opengfx: free graphics' 
            'openttd-openmsx: free musicset'
            'openttd-opensfx: free soundset')
makedepends=('cmake' 'ninja')

source=("https://cdn.$_pkgname.org/$_pkgname-releases/$pkgver/$_pkgname-$pkgver-source.tar.xz"
        "OpenTTD_patches.zip::https://www.dropbox.com/s/pn8vepuxi26hj9x/OpenTTD_12.2_122A_patch.zip?dl=1")
sha256sums=(
            '81508f0de93a0c264b216ef56a05f8381fff7bffa6d010121a21490b4dace95c'
            '6efe936b6ef605e60372ba565cf91c977eced7096bf4fdbd569af5607adfa56a')
conflicts=('openttd')
 
prepare() {
  cd $_pkgname-$pkgver
  sed -i '/sse/d;/SSE/d' CMakeLists.txt
  patch -p1 < "../OpenTTD_${pkgver}_${_nice_release}_patch/public_${_nice_release}.diff" || true
}
 
build() {
#   -D GLOBAL_DATA_DIR=/usr/share/openttd \
  cmake \
    -B build \
    -D CMAKE_BUILD_TYPE=Release \
    -D CMAKE_INSTALL_PREFIX=/usr \
    -D CMAKE_INSTALL_BINDIR=bin \
    -D CMAKE_INSTALL_DATADIR=/usr/share \
    -G Ninja \
    -S $_pkgname-$pkgver
  ninja -C build
}
 
package() {
  DESTDIR="$pkgdir" ninja -C build install
  mkdir -p "${pkgdir}/usr/share/openttd/baseset/newgrf/"
  install -m644 -D "OpenTTD_${pkgver}_${_nice_release}_patch/newgrf/innerhighlight.grf" "${pkgdir}/usr/share/openttd/baseset/newgrf/innerhighlight.grf"
}

