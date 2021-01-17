# Maintainer: Jonas Renk <jonas.renk@stud.tu-darmstadt.de>
pkgname=systemverilog
pkgver=20210116
pkgrel=1
epoch=
pkgdesc="Synthese und Simulation"
arch=('any')
url="https://moodle.informatik.tu-darmstadt.de/mod/folder/view.php?id=31324"
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
md5sums=('3658f7ab86ba995e612178de6920825c')
validpgpkeys=()

prepare() {
    cd $srcdir
    rm -rf SystemVerilog
    unzip "$pkgname-$pkgver.zip" -x '*.exe' '*.bat' '*.mac'

    dos2unix SystemVerilog/bin/*.sh
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
