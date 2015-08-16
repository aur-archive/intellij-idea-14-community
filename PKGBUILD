# Maintainer: Christian Staude <christian.staude@s2009.tu-chemnitz.de>
pkgname=intellij-idea-14-community
pkgver=14.1.1
_buildver=141.178.9
pkgrel=1
pkgdesc='An intelligent IDE for Java, Groovy and other programming languages with advanced refactoring features intensely focused on developer productivity.'
arch=('i686' 'x86_64') # not 'any' because of fsnotifier
url="http://www.jetbrains.com/idea/"
backup=("usr/share/${pkgname}/bin/idea.vmoptions" "usr/share/${pkgname}/bin/idea64.vmoptions")
license=('Commercial')
depends=('java-environment' 'giflib')
options=(!strip)
source=("http://download.jetbrains.com/idea/ideaIC-${pkgver}.tar.gz"
        "${pkgname}.sh"
        "${pkgname}.desktop")
md5sums=('9c9bbdfbaf88b79009bb2a87aa8f0376'
         'c505df3e5f76840b6a9e4349005daccd'
         '8417e84044d308dc539700a5b9055d05')

package() {
  cd "${srcdir}"

  install -d -m755 $pkgdir/usr/{bin,share}
  cp -a "idea-IC-${_buildver}" "${pkgdir}/usr/share/${pkgname}"
  chown -R root:root "${pkgdir}/usr/share"

  find $pkgdir/usr/share/$pkgname -type d -exec chmod 0755 {} ';'
  find $pkgdir/usr/share/$pkgname -type f -exec chmod 0644 {} ';'

  # never wait on user input when starting idea; copied from -ce PKGBUILD
  sed -i '/.*read IGNORE.*/ d' "${pkgdir}"/usr/share/$pkgname/bin/idea.sh

  chmod +x $pkgdir/usr/share/$pkgname/bin/idea.sh
  chmod +x "$pkgdir"/usr/share/$pkgname/bin/fsnotifier
  chmod +x "$pkgdir"/usr/share/$pkgname/bin/fsnotifier64

  install -D -m755 "${srcdir}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
  install -D -m644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -D -m644 "$srcdir/idea-IC-$_buildver/bin/idea.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -D -m644 "$srcdir/idea-IC-$_buildver/NOTICE.txt" "$pkgdir/usr/share/licenses/$pkgname/NOTICE.txt"

  # workaround FS#40934
  sed -i 's|lcd|on|'  "$pkgdir"/usr/share/$pkgname/bin/*.vmoptions
}

# vim:set ts=2 sw=2 et:
