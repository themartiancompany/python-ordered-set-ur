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
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Tobias Roettger <toroettg@gmail.com>

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
_pkg=ordered-set
pkgname="${_py}-${_pkg}"
pkgver=4.1.0
pkgrel=4
_pkgdesc=(
  'A MutableSet that remembers its order,'
  'so that every entry has an index'
)
arch=(
  'any'
)
_http="https:/github.com"
_ns="rspeer"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pytest"
)
_pypa="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  'f12d19f7d9cf0ebcc414d97798f0959ff69a77146839cc6a9067c864f9e0be795795c4d648f736fd7448ddf89666ce37f23e7380d1c9b1678a4787961e4e1e79'
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
  cd \
    "${_pkg}-${pkgver}"
  pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
        --destdir="${pkgdir}" \
        "dist/"*".whl"
  install \
    -Dm644 \
    "MIT-LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set ts=2 sw=2 et:
