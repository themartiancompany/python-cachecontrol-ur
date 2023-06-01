# Maintainer: David Runge <dvzrv@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

_name=cachecontrol
pkgname=python-cachecontrol
pkgver=0.13.0
pkgrel=1
epoch=1
pkgdesc="httplib2 caching for requests"
arch=(any)
url="https://github.com/ionrock/${_name}"
license=(Apache)
depends=(
  python
  python-filelock
  python-msgpack
  python-requests
  python-urllib3
)
makedepends=(
  python-build
  python-installer
  python-setuptools
  python-wheel)
checkdepends=(
  python-cherrypy
  python-mock
  python-pytest
  python-redis
)
optdepends=(
  'python-lockfile: for filecache'
  'python-redis: for redis cache'
)
# not tests in dist tarball on pypi.org: https://github.com/ionrock/cachecontrol/issues/281
# source=(https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz)
source=($_name-$pkgver.tar.gz::https://github.com/ionrock/$_name/archive/refs/tags/v$pkgver.tar.gz)
sha256sums=('c30d9112259dad7c83a84f781165076041d7d506ab8d99a6c0d6c06100f35f53')
b2sums=('b544d8a662a5850c629f76969fce32651c259fbdf59970c138db6418a2aa3104fe180377cfcee2613abd6d239d75d2878d95090615ff59f590c8a0080e711821')

build() {
  cd $_name-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  local _site_packages=$(python -c "import site; print(site.getsitepackages()[0])")

  cd $_name-$pkgver
  python -m installer --destdir=test_dir dist/*.whl
  export PYTHONPATH="test_dir/$_site_packages:$PYTHONPATH"
  pytest -vv
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -vDm 644 README.rst -t "$pkgdir/usr/share/doc/$pkgname/"
}
