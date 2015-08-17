# Contributor: 3ED <krzysztof1987 at gmail dot com>
#
pkgname=perl-module-implementation
_lastauthor=D/DR/DROLSKY
_pkgname=Module-Implementation
pkgver=0.06
pkgrel=2
pkgdesc="Loads one of several alternate underlying implementations for a module"
arch=('any')
license=('PerlArtistic2')
options=('!emptydirs')
depends=('perl-module-runtime>=0.012')
checkdepends=('perl-test-requires' 'perl-test-fatal')
url="http://search.cpan.org/dist/${_pkgname}/"
source=(http://search.cpan.org/CPAN/authors/id/${_lastauthor}/${_pkgname}-${pkgver}.tar.gz)
sha256sums=('da3b78025ab82b04c042e7cc1fdefc3af225ca90865c215d4d8bcf3bbf54186d')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL="--skipdeps" \
    PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
    PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
    MODULEBUILDRC=/dev/null

  if [ -f "Build.PL" ]; then
    perl Build.PL
    perl Build
  elif [ -f "Makefile.PL" ]; then
    perl Makefile.PL
    make
  else
    return 1
  fi
}
check() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  if [ -f "Build.PL" ]; then
    perl Build test
  elif [ -f "Makefile.PL" ]; then
    make test
  fi
}
package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  if [ -f "Build.PL" ]; then
    perl Build install
  elif [ -f "Makefile.PL" ]; then
    make install
  fi

  find "${pkgdir}" -name .packlist -o -name perllocal.pod -delete
}
