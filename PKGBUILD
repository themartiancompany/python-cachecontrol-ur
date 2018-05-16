# Maintainer: Eli Schwartz <eschwartz@archlinux.org>

_pkgname=cachecontrol
pkgbase='python-cachecontrol'
pkgname=('python-cachecontrol' 'python2-cachecontrol')
pkgver=0.12.4
pkgrel=1
pkgdesc="httplib2 caching for requests"
arch=('any')
url="https://github.com/ionrock/${_pkgname}"
license=('Apache')
makedepends=('python-msgpack' 'python-requests' 'python2-msgpack' 'python2-requests')
checkdepends=('python-mock' 'python-pytest' 'python-lockfile' 'python-cherrypy'
              'python2-mock' 'python2-pytest' 'python2-lockfile' 'python2-cherrypy')
source=("${_pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "0001-Remove-unnecessary-console-script.patch")
sha256sums=('99face8fb57c6b4d2a9a9e35671a25f3522b359cc83477084f9e8a0a57d4e996'
            '8aa781f3c25f0538a26614870c3feead4ba3f8ef0a9d1cff0a9abda8c300cea1')

prepare() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    patch -p1 -i ../0001-Remove-unnecessary-console-script.patch
}

build() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python setup.py build
    python2 setup.py build
}

check() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    pytest
    pytest2
}

package_python-cachecontrol() {
    depends=('python-msgpack' 'python-requests')
    optdepends=('python-lockfile: for the FileCache')

    cd "${srcdir}"/${_pkgname}-${pkgver}
    python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}

package_python2-cachecontrol() {
    depends=('python-msgpack' 'python2-requests')
    optdepends=('python2-lockfile: for the FileCache')

    cd "${srcdir}"/${_pkgname}-${pkgver}
    python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
