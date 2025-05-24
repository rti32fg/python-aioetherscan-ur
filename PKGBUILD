# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

_evmfs_available="$( \
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_setuptools="true"
_poetry="false"
_build="false"
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
pkgver=0.9.6.1
_commit="23dbbba312f7938b2d6250af4da4d9b7276788f1"
pkgrel=1
_pkgdesc=(
  'Etherscan API async Python wrapper.'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
  'pentium4'
  'i686'
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
  "${_py}-wheel"
  "${_py}-setuptools"
)
if [[ "${_poetry}" == "true" ]] || \
   [[ "${_build}" == "true" ]]; then
  makedepends+=(
    "${_py}-build"
    "${_py}-installer"
    "${_py}-poetry-core"
  )
fi
if [[ "${_poetry}" == "true" ]]; then
  makedepends+=(
    "${_py}-poetry"
  )
fi
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
  "${_py}-eip3091"
)
_tag="${_commit}"
_tarname="${_pkg}-${_tag}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_sum='7a55511d466126a07ac33ac26b6fd3c82bef9ff5016d48dbb66d6522e9e0d489'
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.zip::${_evmfs_archive_uri}"
_archive_sig_sum="1b77bbebc4e78b4a72891c0f4b56e66d115bcdf6c07484707d7f827a4c2c8443"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.zip.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
  _src="${_evmfs_archive_src}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  _src="${_tarname}.zip::${url}/archive/${_commit}.zip"
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_archive_sum}"
)
b2sums=(
  'd9076f256ee36cc9a5e06e27c19c032694aca8dee834f86e42f9af2098e1847c5b9df548bb6103db2ae8f4c2e4d92a8b17fa3ec668607134a0f40d85de3825a3'
)
validpgpkeys=(
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

_poetry_build() {
  export \
    POETRY_VIRTUALENVS_OPTIONS_NO_PIP=true \
    POETRY_VIRTUALENVS_OPTIONS_SYSTEM_SITE_PACKAGES=true
    # POETRY_VIRTUALENVS_CREATE=false
  # POETRY_VIRTUALENVS_CREATE=false \
  POETRY_VIRTUALENVS_OPTIONS_NO_PIP=true \
  POETRY_VIRTUALENVS_OPTIONS_SYSTEM_SITE_PACKAGES=true \
  poetry \
    -vvv \
    build
}

_build_build() {
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

build() {
  cd \
    "${_tarname}"
  if [[ "${_poetry}" == "true" ]]; then
    _poetry_build
  elif [[ "${_build}" == "true" ]]; then
    _build_build
  fi
}

_setuptools_package() {
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
        --optimize=1
}

_installer_package() {
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
}

package() {
  cd \
    "${_tarname}"
  if [[ "${_setuptools}" == "true" ]]; then
    _setuptools_package
  elif [[ "${_poetry}" == "true" ]] || \
       [[ "${_poetry}" == "true" ]]; then
    _installer_package
  fi
  install \
    -Dm644 \
    LICENSE \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set sw=2 sts=-1 et:
