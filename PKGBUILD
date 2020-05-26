# Maintainer: Karthik Chikmagalur
pkgname=st-karthik-git 
_pkgname=st

pkgver=0.8.2.r19.9e41041
pkgrel=1
pkgdesc="Simple Terminal emulator with transparency, xresources and more"
arch=('x86_64' 'i686')
url="https://github.com/karthink/st"
license=('MIT')
groups=()
depends=('libxft', 'nerd-fonts-iosevka')
optdepends=('dmenu: Pipe terminal output to dmenu' 'xclip: Piping terminal output to other programs')
makedepends=('ncurses' 'libxext' 'git') 

provides=(${_pkgname})
conflicts=(${_pkgname})

replaces=()
backup=()
options=('zipman')
install=

source=("${_pkgname}::git+https://github.com/karthink/st.git#branch=extras")
noextract=()
md5sums=('SKIP')
sha1sums=('SKIP')

# Please refer to the 'USING VCS SOURCES' section of the PKGBUILD man page for
# a description of each element in the source array.

pkgver() {
	cd "$srcdir/${_pkgname}"

# The examples below are not absolute and need to be adapted to each repo. The
# primary goal is to generate version numbers that will increase according to
# pacman's version comparisons with later commits to the repo. The format
# VERSION='VER_NUM.rREV_NUM.HASH', or a relevant subset in case VER_NUM or HASH
# are not available, is recommended.

# Git, tags available
	# printf "%s" "$(git describe --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"

# Git, no tags available
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"

}

prepare() {
	cd "$srcdir/${_pkgname}"
	sed -i '/tic /d' Makefile
}

build() {
	cd "$srcdir/${_pkgname}"
	# ./autogen.sh
	# ./configure --prefix=/usr
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

# check() {
# 	cd "$srcdir/${_pkgname}"
# 	make -k check
# }

package() {
	cd "$srcdir/${_pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}/" install
        install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
        # install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
        # install -Dm644 .Xdefaults "${pkgdir}/usr/share/doc/${pkgname}/Xdefaults.example"
}
