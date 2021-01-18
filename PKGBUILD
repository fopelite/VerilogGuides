# Maintainer: Jonas Renk <jonas.renk@stud.tu-darmstadt.de>
pkgname=sv-toolchain-edu
pkgver=1
pkgrel=1
epoch=
pkgdesc="Synthesis and Simulation of SystemVerilog"
arch=('any')
url="https://www.encrypto.cs.tu-darmstadt.de/teaching_theses/digitaltechnik_ws2021/index.en.jsp"
license=('MIT')
groups=()
depends=('yosys'
         'graphviz'
         'iverilog'
         'gtkwave')
makedepends=('dos2unix'
             'unzip')
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("$pkgname-$pkgver.zip")
noextract=("$pkgname-$pkgver.zip")
md5sums=('SKIP')
validpgpkeys=()

prepare() {
    cd $srcdir
    rm -rf SystemVerilog
    unzip "$pkgname-$pkgver.zip" -x '*.exe' '*.bat' '*.mac'

    find SystemVerilog -type f -exec dos2unix '{}' \;
    chmod +x SystemVerilog/bin/*.sh
}

check() {
    cd $srcdir/SystemVerilog/src/comb

    # Testing the synthesis
    ../../bin/synth.sh example example.sv
}

package() {
    mkdir -p $pkgdir/usr/share/$pkgname
    cp -rv $srcdir/SystemVerilog/* $pkgdir/usr/share/$pkgname

    mkdir -p $pkgdir/usr/bin/
    for file in $pkgdir/usr/share/$pkgname/bin/*.sh; do
        ln -s /usr/share/$pkgname/bin/$(basename $file) \
              $pkgdir/usr/bin/sv-$(basename $file .sh)
    done
}
