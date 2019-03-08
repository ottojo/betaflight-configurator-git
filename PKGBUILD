# Maintainer: Jonas Otto < jonas at jonasotto dot com >
pkgname=betaflight-configurator-git
_pkgname=betaflight-configurator
pkgver=10.5.0.4dcc9105
pkgrel=1
pkgdesc="Crossplatform configuration tool for the Betaflight flight control system"
arch=('x86_64')
url="https://github.com/betaflight/betaflight-configurator"
source=("betaflight-configurator::git+https://github.com/betaflight/betaflight-configurator.git#branch=master")
md5sums=('SKIP')
license=('GPL3')
conflicts=('betaflight-configurator')
makedepends=('gulp' 'npm' 'git' 'jq')

pkgver() {
  cd "$_pkgname"
  echo $(cat package.json| jq -r ".version").$(git rev-parse --short HEAD)
}

build() {
    cd $_pkgname
    npm install gulp-cli
    gulp apps --linux64
}

package() {
    mkdir -p "$pkgdir/opt/betaflight"
    mkdir -p "$pkgdir/usr/bin"
    install -Dm644 "$srcdir/$_pkgname/apps/betaflight-configurator/linux64/$_pkgname.desktop" "$pkgdir/usr/share/applications/$_pkgname.desktop"
    cp -dpr --no-preserve=ownership "$srcdir/$_pkgname/apps/betaflight-configurator/linux64" "$pkgdir/opt/betaflight/betaflight-configurator"
    ln -s "/opt/betaflight/betaflight-configurator/$_pkgname" "$pkgdir/usr/bin/$_pkgname"

    echo 'Dont forget to add your user into dialout group "sudo usermod -aG dialout YOUR_USERNAME" for serial access'
}
