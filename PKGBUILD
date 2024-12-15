# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Frederik Schwan <freswa at archlinux dot org>
# Contributor: Hao Long <imlonghao@archlinuxcn.org>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

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
_pkg="aioetherscan"
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=0.9.5.3
_commit="de3c77f4e4a0817fe55a3970ff06f624bf7915d9"
pkgrel=1
_pkgdesc=(
  'Etherscan API async Python wrapper.'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  any
)
# _ns="ape364"
_ns="themartiancompany"
_http="https://github.com"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}>=3.9"
  "${_py}-aiohttp>=3.4"
  "${_py}-asyncio-throttle>=1.0.1"
  "${_py}-aiohttp-retry>=2.8.3"
)
makedepends=(
  "cython"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-poetry"
  "${_py}-poetry-core"
  "${_py}-wheel"
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-pytest>=8.2.2"
  "${_py}-pytest-asyncio>=0.23.7"
)
provides=(
  "${_pkg}=${pkgver}"
)
conflicts=(
  "${_pkg}"
)
source=(
  "${_pkg}-${_commit}::${url}/archive/${_commit}.zip"
  # "${url}/archive/v${pkgver}/${_pkg}-${pkgver}.tar.gz"
)
sha256sum=(
  'a2010c4430264e359bb3c47315f38dfa94efda90c5cd6a6eac2d7010b78fe61e'
)
b2sums=(
  'e4a42368b46a7824d577f4ca716ece9ebdea50a8c44c2d1561d717e3e2f9b1814519d159793ba54622d2a6a542df2ff3b934f659454d54a2299b82c421bab84b'
)

build() {
  cd \
    "${_pkg}-${_commit}"
  poetry \
    build
}

package() {
  cd \
    "${_pkg}-${_commit}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}

# vim:set sw=2 sts=-1 et:
