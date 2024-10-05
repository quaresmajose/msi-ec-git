# Maintainer: Catemiko
# Contributor: BeardOverflow

_gitname=msi-ec
pkgname=$_gitname-dkms-git
pkgver=0
pkgrel=08
pkgdesc="Driver for MSI laptop EC"
arch=('any')
url="https://github.com/BeardOverflow/msi-ec"
license=('GPL2')
depends=(dkms)
makedepends=('git')
backup=()
conflicts=('msi-ec-git')
provides=('msi-ec')

source=("git+https://github.com/BeardOverflow/msi-ec.git")
source+=("0001-fix-kernel-6.11.patch")
sha256sums=('SKIP'
            'a419987c2d609da8ca4299cb36919e30a71ca76ba1ce39cd7bf7b107933deeea')

prepare() {
    git -C ${_gitname} am ${srcdir}/0001-fix-kernel-6.11.patch
}

package() {
    cd "${_gitname}"
    echo msi-ec > msi-ec.conf
    sed -e "s/@VERSION@/${pkgver}.${pkgrel}/" -e 's/^MAKE.*//' -i dkms.conf

    install -Dm 644 msi-ec.conf "${pkgdir}/etc/modules-load.d/msi-ec.conf"
    install -Dm 644 msi-ec.c ec_memory_configuration.h dkms.conf Makefile -t ${pkgdir}/usr/src/${_gitname}-${pkgver}.${pkgrel}
}
