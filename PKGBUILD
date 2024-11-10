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
url='https://bitbucket.org/tuxedocomputers/clevo-xsm-wmi'
options=(!emptydirs)
conflicts=("$_pkgbase" 'tuxedo-wmi' 'tuxedo-wmi-dkms')
provides=("$_pkgbase")
depends=('dkms' 'gcc' 'make' 'linux-headers')
source=("clevo-xsm-wmi-${_pkgtag}.src.tar.gz::https://bitbucket.org/tuxedocomputers/clevo-xsm-wmi/get/${_pkgtag}.tar.gz"
        "ZX-550.patch"
        "rfkill.patch"
        "kernel-6.11.patch"
        "dkms.conf"
        "Makefile")
sha256sums=('dd326e9855b708b7ab922d47b3abcd24c53a3af4fdc1c164399c8dbdb5a7f6ce'
            '4829ea13de13694881fefaae6ddffbec3506db3b0b86d67a904907567ee4f7a0'
            '2fee44a215c1f52c48e302ca6dcfbb8dd3c048a38d8984cd40b64646b168ec34'
            '414d6357d14efb0838ed497882a62933dc174ae2bcd8750c8c012d8e3166ec2d'
            '0cdf0213692a71d69f54730d1856d9f1e7b3d363d9b2a66a5d6bb363e8d8212f'
            'fb20847bde676a305fda41b865b46aff52ae9de60e1262d6e9725a71d72b806b')
install='clevo-xsm-wmi-dkms.install'

prepare() {
    cd "${srcdir}/tuxedocomputers-clevo-xsm-wmi-${_pkgtag}"
    patch -i "${srcdir}/ZX-550.patch" -p1
    patch -i "${srcdir}/rfkill.patch" -p1
    patch -i "${srcdir}/kernel-6.11.patch" -p1
}

package() {
    cd "${srcdir}/tuxedocomputers-clevo-xsm-wmi-${_pkgtag}/module"

    # Copy sources (including Makefile)
    install -dm755 "${pkgdir}/usr/src/${_modname}-${pkgver}/"
    install -Dm644 "${srcdir}/Makefile" "${srcdir}/dkms.conf" "clevo-xsm-wmi.c" "${pkgdir}/usr/src/${_modname}-${pkgver}/"
    
    # Module loading
    install -Dm644 /dev/null "$pkgdir/usr/lib/modules-load.d/$pkgname.conf"
    echo "clevo-xsm-wmi" > "$pkgdir/usr/lib/modules-load.d/$pkgname.conf"
}
