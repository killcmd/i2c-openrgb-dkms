# Maintainer: Martin Sandsmark <martin.sandsmark@kde.org>
# Contributor: Térence Clastres <t.clastres@gmail.com>

pkgname=i2c-openrgb-dkms
_pkgbase=${pkgname%-dkms}
pkgver=5.6.7
pkgrel=1
pkgdesc='The i2c-openrgb kernel driver'
arch=('any')
url='https://gitlab.com/CalcProgrammer1/OpenRGB'
license=('GPL2')
depends=('dkms')
conflicts=('i2c-piix4-aura-dkms')
source=('i2c-nct6775.c'
        'dkms.conf'
        'Makefile'
        'i2c-piix4.c'
        'i2c-openrgb.conf')
md5sums=('6b41c8cd2bd4ecb9730245c2b64c969f'
         'da9f65e6c471c2713ae993b032e40252'
         '26291c6e947270780692affd34b62676'
         '5ed9c7a9702a23f7e6804baffddc3c8a'
         '3acb7c084599e43948304ef942742bb2')

prepare() {
  mkdir -p "${srcdir}/${_pkgbase}" && cd "${srcdir}/${_pkgbase}"

  cp ../dkms.conf ../Makefile .
  cp ../i2c-nct6775.c i2c-nct6775.c
  cp ../i2c-piix4.c i2c-piix4.c
}

package() {
  # Copy dkms.conf
  install -Dm644 dkms.conf "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"

  # Copy sources (including Makefile)
  cp -r ${_pkgbase}/{i2c-nct6775.c,Makefile,i2c-piix4.c} "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/"

  # udev rule to alow users part of the 'wheel' group to access i2c without root privileges
#   install -Dm644 90-i2c-aura.rules "${pkgdir}/usr/lib/udev/rules.d/90-i2c-aura.rules"

  # modprobe needed modules at boot
  install -Dm644 i2c-openrgb.conf "${pkgdir}/usr/lib/modules-load.d/i2c-openrgb.conf"
}
