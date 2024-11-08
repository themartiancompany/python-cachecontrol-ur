# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: David Runge <dvzrv@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=cachecontrol
pkgname="${_py}-${_pkg}"
pkgver=0.14.0
pkgrel=3
epoch=1
_pkgdesc=(
  "Port of the caching algorithms in httplib2"
  "for use with requests session object"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  any
)
_http="https://github.com"
_ns="ionrock"
url="${_http}/${_ns}/${_pkg}"
license=(
  Apache-2.0
)
depends=(
 "${_py}>=${_pymajver}"
 "${_py}<${_pynextver}"
 "${_py}-filelock"
 "${_py}-msgpack"
 "${_py}-requests"
 "${_py}-urllib3"
)
makedepends=(
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-cherrypy"
  "${_py}-pytest"
  "${_py}-redis"
)
optdepends=(
  "${_py}-lockfile: for filecache"
  "${_py}-redis: for redis cache"
)
source=(
  "${_pkg}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz"
)
sha256sums=(
  '159f4341e015d11b16de5b9f86e207cff753d6080642671f4cd09717e34a12a0'
)
b2sums=(
  '352b417512dd2858ba5d43c72116a6930037adc6fc70f66efbee9c1e4e81c296bf9ebf0e862834311afaff0c66d9bbfc16a35dfe978fdf759e07e993d49a0a71'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir=test_dir \
    dist/*.whl
  export \
    PYTHONPATH="test_dir/${_site_packages}:${PYTHONPATH}"
  pytest \
    -vv
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -vDm644 \
    README.rst \
    -t \
    "${pkgdir}/usr/share/doc/${pkgname}/"
}
