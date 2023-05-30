# Maintainer: David Runge <dvzrv@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

_name=cachecontrol
pkgname=python-cachecontrol
pkgver=0.12.11
pkgrel=3
epoch=1
pkgdesc="httplib2 caching for requests"
arch=(any)
url="https://github.com/ionrock/${_name}"
license=(Apache)
depends=(python-msgpack python-requests)
makedepends=(python-build python-installer python-setuptools python-wheel)
checkdepends=(python-cherrypy python-lockfile python-pytest python-redis)
optdepends=(
  'python-lockfile: for filecache'
  'python-redis: for redis cache'
)
# not tests in dist tarball on pypi.org: https://github.com/ionrock/cachecontrol/issues/281
# source=(https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz)
source=($_name-$pkgver.tar.gz::https://github.com/ionrock/$_name/archive/refs/tags/v$pkgver.tar.gz
	use-unittest-mock.patch::https://github.com/ionrock/cachecontrol/commit/634cb776cb934908a1be3029e21d11ed7923ee07.patch)
sha256sums=('06f9ad43ed6bb9ed23883fda838bacada949a00dc557e7f41aecbd19787efdcf'
            '8b565a148a816a4dedf88acb90caf0f2fdab2fde77ca567eb945b7aa5b777129')
b2sums=('09ce2336216b69dbe9796d658db9f5b0d378259484cba3a78ecd789843e19683adc2b1b90d579cea8700d07ed55a93ecc3a56e5da2c8ab025e5084d2847d4dbf'
        'a2fd44afd7f9893cc4f2379b637953fcaa50a955f963cbf90f038dbbcd3d6002050c15b611c879e3553c200bdd536b85969444daff56f83f24b3dcc4c1698153')

prepare() {
  cd $_name-$pkgver
  patch -Np1 -i ${srcdir}/use-unittest-mock.patch
}

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
