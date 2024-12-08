# Maintainer: Marc ROZANC <marc@rozanc.fr>

_pkgbase='clevo-xsm-wmi'
_modname=$_pkgbase
pkgname="${_pkgbase}-dkms"
pkgver='1.1'
_pkgtag='dcf282992eb8'
pkgrel=8
pkgdesc='A reverse engineering driver for the Clevo SM series backlight keyboard (DKMS version)'
arch=('i686' 'x86_64')
license=('GPL')
url='https://gitlab.com/tuxedocomputers/development/clevo-xsm-wmi'
options=(!emptydirs)
conflicts=("$_pkgbase" 'tuxedo-wmi' 'tuxedo-wmi-dkms')
provides=("$_pkgbase")
depends=('dkms' 'gcc' 'make' 'linux-headers')
source=("clevo-xsm-wmi-${_pkgtag}.src.tar.gz::https://gitlab.com/tuxedocomputers/development/clevo-xsm-wmi/-/archive/$_pkgtag/clevo-xsm-wmi-$_pkgtag.tar.gz"
        "ZX-550.patch"
        "rfkill.patch"
        "kernel-6.11.patch"
        "dkms.conf"
        "Makefile")
sha256sums=('eb64ca7ee61d4f3776b7d3b1dc3d920eefc6a7ad2d13319086ac99b33cd590c2'
            '4829ea13de13694881fefaae6ddffbec3506db3b0b86d67a904907567ee4f7a0'
            '2fee44a215c1f52c48e302ca6dcfbb8dd3c048a38d8984cd40b64646b168ec34'
            'b3ca9b5cc53e5ec202796a9fe498a52bf4abf9451c9dd310e1cb8501c6604acc'
            '0cdf0213692a71d69f54730d1856d9f1e7b3d363d9b2a66a5d6bb363e8d8212f'
            'fb20847bde676a305fda41b865b46aff52ae9de60e1262d6e9725a71d72b806b')
install='clevo-xsm-wmi-dkms.install'

prepare() {
    cd "${srcdir}/clevo-xsm-wmi-${_pkgtag}"
    patch -i "${srcdir}/ZX-550.patch" -p1
    patch -i "${srcdir}/rfkill.patch" -p1
    patch -i "${srcdir}/kernel-6.11.patch" -p1
}

package() {
    cd "${srcdir}/clevo-xsm-wmi-${_pkgtag}/module"

    # Copy sources (including Makefile)
    install -dm755 "${pkgdir}/usr/src/${_modname}-${pkgver}/"
    install -Dm644 "${srcdir}/Makefile" "${srcdir}/dkms.conf" "clevo-xsm-wmi.c" "${pkgdir}/usr/src/${_modname}-${pkgver}/"
    
    # Module loading
    install -Dm644 /dev/null "$pkgdir/usr/lib/modules-load.d/$pkgname.conf"
    echo "clevo-xsm-wmi" > "$pkgdir/usr/lib/modules-load.d/$pkgname.conf"
}
