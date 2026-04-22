# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Christian Hesse
#     <mail@eworm.de>
#   Christian Heusel
#     <gromit@archlinux.org>
#   Gaetan Bisson
#     <bisson@archlinux.org>
#   Andrea Scarpino
#     <andrea@archlinux.org>
#   dorphell
#     <dorphell@archlinux.org>
#   Tom Newsom
#     <Jeepster@gmx.co.uk>

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
_evmfs_available="$(
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
if [[ ! -v "_git_service" ]]; then
  # _git_service="finalrewind"
  # _git_service="gitlab"
  _git_service="github"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_docs" ]]; then
  if [[ "${_os}" == "GNU/Linux" ]]; then
    _docs="true"
  else
    _docs="false"
  fi
fi
if [[ ! -v "imagemagick" ]]; then
  _imagemagick="true"
fi
_pkg=feh
if [[ ! -v "_git_http" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _git_http="github.com"
  elif [[ "${_git_service}" == "gitlab" ]]; then
    _git_http="gitlab.com"
  elif [[ "${_git_service}" == "finalrewind" ]]; then
    _git_http="git.${_pkg}.org"
  fi
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _ns="themartiancompany"
  elif [[ "${_git_service}" == "gitlab" ]]; then
    _ns="themartiancompany"
  elif [[ "${_git_service}" == "finalrewind" ]]; then
    _ns=""
  fi
fi
if [[ ! -v "_http" ]]; then
  if [[ \
       "${_git_service}" == "github" || \
       "${_git_service}" == "gitlab" \
     ]]; then
    _http="https://${_git_service}.com"
  elif [[ "${_git_service}" == "finalrewind" ]]; then
    _http="https://${_pkg}.${_git_service}.org"
  fi
fi
if [[ ! -v "url" ]]; then
  if [[ \
       "${_git_service}" == "github" || \
       "${_git_service}" == "gitlab" \
     ]]; then
    url="${_http}/${_ns}/${_pkg}"
  elif [[ "${_git_service}" == "finalrewind" ]]; then
    url="${_http}"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="true"
  if [[ "${_git_service}" == "finalrewind" ]]; then
    _git="true"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=3.12.1
_commit="4566ff69a7b4bcc0c00c7fd49453098de10aff67"
_bundle_commit="fb0934d63d26b76cced40dc69a1a9d2eac39c2b1"
pkgrel=17
_pkgdesc=(
  'Fast and light imlib2-based image viewer'
)
pkgdesc="${_pkgdesc[*]}"
license=(
  'MIT'
)
arch=(
  "aarch64"
  "arm"
  "armv7l"
  "armv8l"
  "mips"
  "pentium4"
  "powerpc"
  "x86_64"
)
depends=(
  'curl'
  'libcurl.so'
  'file'
  'libmagic.so'
  "${_libc}"
  'hicolor-icon-theme'
  'imlib2' #'libImlib2.so'
  'libexif'
  'libexif.so'
  'libpng'
  'libpng16.so'
  'libx11' #'libX11.so'
  'libxinerama' #'libXinerama.so'
)
makedepends=(
  "${_compiler}"
  "${_libcompiler}"
  "${_libc}"
  'libexif'
  'imlib2' #'libImlib2.so'
  'libx11' #'libX11.so'
  'libxinerama' #'libXinerama.so'
  'libxt'
  "xorgproto"
)
if [[ "${_imagemagick}" == "true" ]]; then
  makedepends+=(
    'imagemagick'
  )
fi
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_libc_headers}"
    "windows-default-manifest"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
_imagemagick_optdepends=(
  'imagemagick:'
    "support more file formats"
)
optdepends=(
  "${_imagemagick_optdepends[*]}"
)
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_sum="1d653b2fcb0b6a159ce05531643ef9107914bcacb6de04fe6b9767dc629ceeb1"
_sig_sum="35e871f2ad17da6aaa3cebfa83a1b203678330833b31051de254f78792bccb32"
_github_sum="dc549aa6952fd1fda8b4dd9750101e63d2c7c0424f81b9d08ffbd574cc727b82"
_github_sig_sum="b3d0c5d3835fa323a92c7f2e26ad438b7e683d8c381f4182183c25ebc42fd5da"
_bundle_sum="e14a28353ad4a48b63c940e99f71788cb153b6e7d2c1c1b5269ff8a3075a468d"
_bundle_sig_sum="a44169ce325cda0d3337d3cb9b708b7fa5b00d5013986009293d6bf5cc6ebcee"
if [[ "${_git}" == "true" ]]; then
  _sum="${_bundle_sum}"
  _sig_sum="${_bundle_sig_sum}"
fi
# Dvorak
_dvorak_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
# Truocolo
_truocolo_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
_evmfs_sig_ns="${_dvorak_ns}"
_evmfs_ns="${_truocolo_ns}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  elif [[ "${_git}" == "true" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}.git#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
    if [[ "${_git_service}" == "finalrewind" ]]; then
      _sum='eaba7ce634a26b1ce6fc4e1789ac99638ddd91d637a28b5144fb39108430b9d4'
    fi
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"

      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Birte Kristina Friesel
  #   <birte.friesel@uni-osnabrueck.de>
  '429AF7B8E9EC9C0709D32F7F5333FB7712E24FE8'
  # Daniel Friesel
  #  <derf@finalrewind.org> 
  '781BB7071C6BF648EAEB08A1100D5BFB5166E005'
  # Derf Null
  #   <derf@ccc.de>
  '64FE6EC055560F9EF13A304419E6E524EBB177BA'
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

_git_unbundle() {
  local \
    _tarname="${1}" \
    _bundle \
    _repo \
    _msg=()
  _bundle="${srcdir}/${_tarname}.bundle"
  _repo="${srcdir}/${_tarname}"
  _msg=(
    "Cloning '${_bundle}' into '${_repo}'."
  )
  msg \
    "${_msg[*]}"
  git \
    clone \
      "${_bundle}" \
      "${_repo}" || \
  git \
    -C \
      "${_repo}" \
      pull || \
  true
}

prepare() {
  local \
    _bash_files=() \
    _src
  if [[ "${_evmfs}" == "true" ]]; then
    if [[ "${_git}" == "false" ]]; then
      ur \
        "never-gonna-give-you-up"
    elif [[ "${_git}" == "true" ]]; then
      _git_unbundle \
        "${_tarname}"
    fi
  fi
}

build() {
  local \
    _make_opts=()
  _make_opts+=(
    PREFIX="/usr"
    exif=1
    inotify=1
    stat64=1
  )
  if [[ "${_docs}" == "true" ]]; then
    _make_opts+=(
      help=1
    )
  fi
  if [[ "${_imagemagick}" == "true" ]]; then
    _make_opts+=(
      magic=1
    )
  fi
  cd \
    "${srcdir}/${_tarname}"
  make \
    "${_make_opts[@]}"
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${srcdir}/${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  install \
    -vDm0644 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
