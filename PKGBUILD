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
_pkg=aioetherscan
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=0.9.6
_commit="79cdaa85fda278f2abbe82132eacf93df572d6f0"
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
  'AGPL3'
)
depends=(
  "evm-chains-explorers"
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
  "${_py}-eip3091=${pkgver}"
)
conflicts=(
  "${_pkg}"
)
source=(
  "${_pkg}-${_commit}.zip::${url}/archive/${_commit}.zip"
  # "${url}/archive/v${pkgver}/${_pkg}-${pkgver}.tar.gz"
)
sha256sum=(
  '51c2f03acb880bf59ee8d58990e277f7b4c0489fb995cb1fe04c82133e6358c8'
)
b2sums=(
  'b21d490de9dafbd6154d35ae79993e4517d3308b433feef0fc5473e1d6646a6a1f022495c1f2527df531d54ed058c6a0519f15b5157994c231e15b4d47c0bdcc'
)

build() {
  cd \
    "${_pkg}-${_commit}"
  poetry \
    -vvv \
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
