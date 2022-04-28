#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

# NOTE:
# 10-bit depth currently fails to build
# https://github.com/pkuvcl/xavs2/issues/9

pkgname=xavs2
pkgver=1.4
pkgrel=1
arch=("x86_64")
pkgdesc="Open-Source encoder of AVS2-P2/IEEE1857.4 video coding standard"
url="https://github.com/pkuvcl/xavs2/"
license=("GPL")
depends=(
    # Arch Linux dependencies
    "glibc"
    "l-smash"
)
makedepends=(
    # Arch Linux dependencies
    "nasm"
)
provides=(
    "libxavs2"
)
conflicts=(
    "libxavs2"
)
replaces=(
    "libxavs2"
)
source=(
    "${pkgname}-${pkgver}.tar.gz"::"https://github.com/pkuvcl/${pkgname}/archive/${pkgver}.tar.gz"
)
sha512sums=(
    "2dd93fe94b85ba019adc808b6bc348a79fcecb812a1a9bfb7f67d5274c29fedbee87de3b2307627aa851d813eb142b270c235e8e17fee4e227f84530f9ce0926"
)
options=("!lto")

build() {
    cd "${pkgname}-${pkgver}/build/linux"

    ./configure \
        --prefix="/usr" \
        --extra-ldflags="-Wl,-z,noexecstack" \
        --enable-shared \
        --bit-depth="8" \
        --chroma-format="all" \
        --enable-lto \
        --enable-pic \
        --disable-swscale \
        --disable-lavf \
        --disable-ffms \
        --disable-gpac

    make
}

package() {
    make -C "${pkgname}-${pkgver}/build/linux" DESTDIR="$pkgdir" install-cli install-lib-shared
}
