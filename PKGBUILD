# Maintainer: TJ Vanderpoel <tj@rubyists.com>
pkgname=riak-search
pkgver=0.14.0
pkgrel=5
pkgdesc="A distributed, easily-scalable, failure-tolerant, real-time, full-text search engine built around Riak Core and tightly integrated with Riak KV."
arch=(i686 x86_64)
url="http://wiki.basho.com/Riak-Search.html"
license=('Apache 2')
depends=('erlang' 'jre')
makedepends=('jdk' 'git' 'spidermonkey' 'apache-ant')
provides=(riak)
replaces=(riak)
conflicts=(riak)
install=riak-search.install
source=(riak_search-0.14.0-1.tar.gz riaksearch riak-search.rc)
md5sums=('c784e42fbc306f84f799ebc780f20acb'
         'd3fadb88f2d1ed068693fe68d0fc4d92'
         '45a025cebac1f0dd76283047651aa16f')

build() {
  cd "$srcdir/riak_search-$pkgver"
  msg Cleaning
  make distclean
  # need to unset LDFLAGS because: ld: unrecognized option '-Wl,--hash-style=gnu'
  unset LDFLAGS
  msg Building
  make rel
}

package() {
  msg Packaging
  install -d $pkgdir/opt/riak-search/
  install -d $pkgdir/etc/rc.d
  install -d $pkgdir/var/log/
  install -d $pkgdir/usr/share/doc/
  install -d $pkgdir//usr/bin/

  cd "$srcdir/riak_search-$pkgver/rel/"
  cp -a riaksearch/* $pkgdir/opt/riak-search/
  chmod -R 755 $pkgdir/opt/riak-search/bin

  ln -s /opt/riak-search/log $pkgdir/var/log/riak-search
  ln -s /opt/riak-search/etc $pkgdir/etc/riak-search
  cp -r ${srcdir}/riak_search-${pkgver}/doc/man $pkgdir/usr/share/
  cp -r ${srcdir}/riak_search-${pkgver}/doc $pkgdir/usr/share/doc/riak-search
  rm -r ${pkgdir}/usr/share/doc/riak-search/man
  
  cp $srcdir/riaksearch $pkgdir/usr/bin
  chmod 755 $pkgdir/usr/bin/riaksearch
  ln -s /usr/bin/riaksearch $pkgdir/usr/bin/riaksearch-admin
  ln -s /usr/bin/riaksearch $pkgdir/usr/bin/search-cmd
  cp $srcdir/riak-search.rc $pkgdir/etc/rc.d/riak-search
  chmod 755 $pkgdir/etc/rc.d/riak-search
}
