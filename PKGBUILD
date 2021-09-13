# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname=pintos-git
pkgver=r1297.f685123
pkgrel=1
epoch=0
pkgdesc="A simple operating system framework for the 80x86 architecture"
arch=('any')
url="https://web.stanford.edu/class/cs140/projects/$pkgname/"
license=('MIT')
groups=()
depends=('perl>=5.8.0' 'gdb')
makedepends=('musl')
checkdepends=()
optdepends=('qemu' 'texinfo')
provides=('pintos')
conflicts=('pintos')
replaces=()
backup=()
options=()
source=("${pkgname}-${pkgver}::git://pintos-os.org/pintos-anon" 'no-stropts.patch')
noextract=()
sha256sums=('SKIP'
            'a9498160806346b53fcf39d0d6b6bcf7f7836cfae91dd8b7887cae6b61360e07')
validpgpkeys=()

pkgver() {
  cd "$pkgname-$pkgver"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$pkgname-$pkgver"
	sed -i 's#^GDBMACROS=.*$#GDBMACROS=/etc/pintos/gdb-macros#g' 'src/utils/pintos-gdb'
	git apply "${srcdir}/no-stropts.patch"
}

build() {
	cd "$pkgname-$pkgver"
	pushd src/utils
	make
}

package() {
	cd "$pkgname-$pkgver"
	
	install -D -m755 src/utils/backtrace "${pkgdir}/usr/bin/backtrace"
	install -D -m755 src/utils/pintos "${pkgdir}/usr/bin/pintos"
	install -D -m755 src/utils/pintos-gdb "${pkgdir}/usr/bin/pintos-gdb"
	install -D -m755 src/utils/pintos-mkdisk "${pkgdir}/usr/bin/pintos-mkdisk"
	install -D -m644 src/utils/pintos-set-cmdline "${pkgdir}/usr/bin/pintos-set-cmdline"
	install -D -m644 src/utils/Pintos.pm "${pkgdir}/usr/bin/Pintos.pm"
	install -D -m755 src/misc/gdb-macros "${pkgdir}/etc/pintos/gdb-macros"
	
	install -D -m755 src/utils/squish-pty "${pkgdir}/usr/bin/squish-pty"
	install -D -m755 src/utils/squish-unix "${pkgdir}/usr/bin/squish-unix"

	install -D -m644 src/LICENSE "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
}
