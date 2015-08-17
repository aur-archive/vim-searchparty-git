# Maintainer: Andy Weidenbaum <archbaum@gmail.com>

pkgname=vim-searchparty-git
pkgver=20140502
pkgrel=1
pkgdesc="Extended search commands and maps for Vim"
arch=('any')
depends=('vim')
makedepends=('git')
groups=('vim-plugins')
url="http://of-vim-and-vigor.blogspot.com/2014/03/welcome-to-search-party.html"
license=('custom:vim')
source=(${pkgname%-git}::git+https://github.com/dahu/SearchParty)
sha256sums=('SKIP')
provides=('vim-searchparty')
conflicts=('vim-searchparty')
install=vimdoc.install

pkgver() {
  cd ${pkgname%-git}
  git log -1 --format="%cd" --date=short | sed "s|-||g"
}

package() {
  cd ${pkgname%-git}

  msg 'Installing documentation...'
  for _doc in README.asciidoc search_party_cheat_sheet.odt search_party_cheat_sheet.pdf; do
    install -Dm 644 $_doc "$pkgdir/usr/share/doc/vim-searchparty/$_doc"
  done

  msg 'Installing appdirs...'
  install -dm 755 "$pkgdir/usr/share/vim/vimfiles"
  for _appdir in autoload doc plugin; do
    cp -dpr --no-preserve=ownership $_appdir "$pkgdir/usr/share/vim/vimfiles/$_appdir"
  done

  msg 'Cleaning up pkgdir...'
  find "$pkgdir" -type d -name .git -exec rm -r '{}' +
}
