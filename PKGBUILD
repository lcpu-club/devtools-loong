# Maintainer: wszqkzqk <wszqkzqk@qq.com>

pkgname=devtools-loong64
pkgver=1.2.1.patch3
pkgrel=1
pkgdesc='Tools for Arch Linux LoongArch package maintainers'
arch=('x86_64' 'loong64')
license=('GPL-3.0-or-later')
url='https://gitlab.archlinux.org/archlinux/devtools'
depends=(devtools)
depends_x86_64=(qemu-user-static)
source=(makepkg-loong64.patch
        pacman-extra-loong64.patch
        pacman-extra-testing-loong64.patch
        pacman-extra-staging-loong64.patch
        sogrep-loong64.patch
        valid-repos-loong64.sh)
source_x86_64=(z-qemu-loong64-static-for-archpkg.conf)
sha256sums=('dff0d9beb29efd2fd87968acb3fc312cee85037697b1f572a27d6fc773bfc9d5'
            'f6b6fea81ec0552dc19cc13e2104d06062f142c0dd7fa59be39dfd6d62eb597f'
            '05861a53f193c53bab5d82a617865ac8c23fd35f6333d0f99c6490a2e6867253'
            'a46e1f8ba72ec6c16dd719b7bc8e5a3c4b27a06215f7f44343b8964dd73c40ea'
            'dd871d8bacab29fa66f761ea96f3f2c60b8cb21d64909fd4f9242699fa58be56'
            'b0f4d2fb78849abe57a6250de42a4e768eec7dd5c09f16c84270a0c24cde5e6c')
sha256sums_x86_64=('0fa4957e6a2097a288036d18953969ff765912518f5b6a01f983a3d2f7f6a8e1')

package() {
  install -Dm644 valid-repos-loong64.sh -t "$pkgdir"/usr/share/devtools/lib
  patch /usr/bin/sogrep -i sogrep-loong64.patch -o sogrep-loong64
  install -Dm755 sogrep-loong64 -t "$pkgdir"/usr/bin/

  ln -s /usr/bin/archbuild "$pkgdir"/usr/bin/extra-loong64-build
  ln -s /usr/bin/archbuild "$pkgdir"/usr/bin/extra-testing-loong64-build
  ln -s /usr/bin/archbuild "$pkgdir"/usr/bin/extra-staging-loong64-build

  patch /usr/share/devtools/makepkg.conf.d/x86_64.conf -i makepkg-loong64.patch -o loong64.conf
  install -Dm644 loong64.conf -t "$pkgdir"/usr/share/devtools/makepkg.conf.d
  patch /usr/share/devtools/pacman.conf.d/extra.conf -i pacman-extra-loong64.patch -o extra-loong64.conf
  install -Dm644 extra-loong64.conf -t "$pkgdir"/usr/share/devtools/pacman.conf.d
  patch extra-loong64.conf -i pacman-extra-testing-loong64.patch -o extra-testing-loong64.conf
  install -Dm644 extra-testing-loong64.conf -t "$pkgdir"/usr/share/devtools/pacman.conf.d
  patch extra-loong64.conf -i pacman-extra-staging-loong64.patch -o extra-staging-loong64.conf
  install -Dm644 extra-staging-loong64.conf -t "$pkgdir"/usr/share/devtools/pacman.conf.d

  if [[ ! "$CARCH" =~ loong ]]; then
    install -dm755 "$pkgdir"/usr/share/devtools/setarch-aliases.d
    echo "$CARCH" > "$pkgdir"/usr/share/devtools/setarch-aliases.d/loong64

    # qemu-user-static-binfmt with C flag
    install -Dm644 z-qemu-loong64-static-for-archpkg.conf -t "$pkgdir"/usr/lib/binfmt.d/
  fi
}
