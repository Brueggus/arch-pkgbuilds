# Contributor: Spider.007 <archlinux AT spider007 DOT net>
pkgname=kibana
pkgver=5.4.0
pkgrel=1
pkgdesc="browser based analytics and search dashboard for Elasticsearch. Please note; this package replaces the distributed precompiled binary 'node'"
arch=('any')
url="https://www.elastic.co/products/kibana"
license=('apache')
depends=('nodejs')
optdepends=('elasticsearch>=2.4')
backup=('etc/elasticsearch/kibana/kibana.yml')
options=('!strip')
source=(
	"https://artifacts.elastic.co/downloads/$pkgname/$pkgname-$pkgver-linux-x86_64.tar.gz"
	kibana.service)
sha256sums=('58838dcb5b3195455e1eb05926fed27d882a3476370facfc35d39d837940b1bc'
            '610c50d38ff0d4cff308b2ff2f38ce3012bf70e396aa25a9b85b821ad3675e3b')

package() {
	cd "$pkgdir"

	install -dm755 usr/share/kibana
	install -Dm644 "$srcdir/kibana.service" usr/lib/systemd/system/kibana.service
	install -Dm644 "$srcdir"/$pkgname-$pkgver-linux-x86_64/config/kibana.yml etc/elasticsearch/kibana/kibana.yml

	rm -R "$srcdir"/$pkgname-$pkgver-linux-x86_64/node/
	cp -Rp "$srcdir"/$pkgname-$pkgver-linux-x86_64/* usr/share/kibana
	chmod -R g+w,o+w usr/share/kibana/{optimize,data}/
}
