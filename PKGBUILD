#Maintainer: Wesley Wiedenmeier <magicalchicken@mail.magicalchicken.dnsdynamic.net>

pkgname=run-one
pkgver=34
pkgrel=1
pkgdesc="Run one instance of some unique combination of command and arguments at a time"
arch=('any')
url="http://launchpad.net/run-one"
license=('GPL')
depends=('procps' 'coreutils' 'bash')
makedepends=('bzr')

_bzrtrunk="https://code.launchpad.net/~run-one/run-one/trunk"
_bzrmod="run-one"

build() {
    msg "Connecting to Bazzar server..."

    if [[ -d "$_bzrmod" ]]; then
        cd "$_bzrmod" && bzr --no-plugins pull "$_bzrtrunk" -r "$pkgver"
        msg "The local files are updated."
    else
        bzr --no-plugins branch "$_bzrtrunk" "$_bzrmod" -q -r "$pkgver"
    fi

    msg "Bazzar checkout done or server timeout"
    msg "Starting install..."

}

package() {
    cd run-one
    msg "Compressing man page..."
    if [[ -e run-one.1.gz ]]; then
        msg "Compressed man page already exists"
    else
        gzip -9 run-one.1
    fi
    install -Dm755 run-one "$pkgdir"/usr/bin/run-one
    install -Dm755 run-this-one "$pkgdir"/usr/bin/run-this-one
    install -Dm755 keep-one-running "$pkgdir"/usr/bin/keep-one-running
    install -Dm644 run-one.1.gz "$pkgdir"/usr/share/man/man1/run-one.1.gz
}
