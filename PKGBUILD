# Maintainer: Isabell Cowan <izzi@izzette.com>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

_realname='kwin'
pkgname=("$_realname-fallapart-fixes")
pkgver=5.12.5
pkgrel=1
pkgdesc='An easy to use, but flexible, composited Window Manager'
arch=('i686' 'x86_64')
url='https://www.kde.org/workspaces/plasmadesktop/'
license=('LGPL')
provides=("$_realname=$pkgver")
conflicts=("$_realname")
depends=('kscreenlocker' 'xcb-util-cursor' 'plasma-framework'
         'kcmutils' 'breeze' 'kinit' 'qt5-sensors')
makedepends=('extra-cmake-modules' 'qt5-tools' 'kdoctools' 'python')
optdepends=('qt5-virtualkeyboard: virtual keyboard support for kwin-wayland')
source=("http://download.kde.org/stable/plasma/$pkgver/$_realname-$pkgver.tar.xz"{,'.sig'}
        'kwin-fallapart-fixes.patch')
sha256sums=('433a40e8565d260d8ec4259d7ce4ec28ef4e4d37f4273bd60aff127a418275d6' 'SKIP'
            '72863244f38a6f275e6522d4ad518af61ab90c2543bf02c28c3b2decfb7f46e7')
validpgpkeys=('2D1D5B0588357787DE9EE225EC94D18F7F05997E'  # Jonathan Riddell
              '348C8651206633FD983A8FC4DEACEA00075E1D76'  # KDE Neon
              'D07BD8662C56CB291B316EB2F5675605C74E02CF'  # David Edmundson
              '1FA881591C26B276D7A5518EEAAF29B42A678C20') # Marco Martin <notmart@gmail.com>

prepare() {
  cd "$srcdir/$_realname-$pkgver"

  msg2 "Patching the fallapart effect"
  patch -Np1 -i "$srcdir/kwin-fallapart-fixes.patch"

  msg2 "Creating build directory"
  mkdir -p "$srcdir/build"
}

build() {
  cd "$srcdir/build"

  msg2 "Running cmake"
  cmake "../$_realname-$pkgver" \
    -DCMAKE_BUILD_TYPE='Release' \
    -DCMAKE_INSTALL_PREFIX='/usr' \
    -DCMAKE_INSTALL_LIBDIR='lib' \
    -DCMAKE_INSTALL_LIBEXECDIR='lib' \
    -DBUILD_TESTING='OFF'

  msg2 "Making $_realname"
  make
}

package() {
  cd "$srcdir/build"

  msg2 "Installing $_realname"
  make DESTDIR="$pkgdir" install
}

# vim: set ts=2 sw=2 et syn=sh ft=sh:
