# Maintainer: SDUSTLUG <lug at sdust.edu.cn>
_pkgname=mugi
pkgname=$_pkgname-git
pkgver="r11.8e422ac"
pkgrel=1
pkgdesc="mugi 是 SDUSTLUG 使用的镜像同步工具"
arch=('any')
url="https://github.com/sdustlug/mugi"
license=('GPL3.0')
depends=('rsync' 'jq' 'moreutils')
provides=("$_pkgname")
conflicts=()
replaces=()
backup=()
options=()
source=(
    'mugi-git::git+https://github.com/sdustlug/mugi.git'
)
noextract=()
sha512sums=(
    'SKIP'
)

pkgver() {
    cd "$srcdir/$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"

}

package() {
    mkdir -p "$pkgdir/usr/bin"
    install -D -m755 "$srcdir/$pkgname/mugi" "$pkgdir/usr/bin/mugi"

    mkdir -p "$pkgdir/etc/mugi"
    install -D -m644 "$srcdir/$pkgname/mugi.conf" "$pkgdir/etc/mugi/mugi.conf"

    mkdir -p "$pkgdir/etc/systemd/"
    cp -rf "$srcdir/$pkgname/systemd" "$pkgdir/etc/systemd/system"


}