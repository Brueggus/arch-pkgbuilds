# Maintainer: Malte Rabenseifner <mail@malte-rabenseifner.de>
# Contributor: EnteEnteEnte <ducksource@duckpond.ch>

pkgname='teamspeak3-server'
pkgver='3.0.12.2'
pkgrel=1
pkgdesc='A proprietary VoIP conference software'
license=('custom')
arch=('i686' 'x86_64')
url="http://www.teamspeak.com"
depends=('glibc')
optdepends=('mariadb-connector-c: for MariaDB backend')
backup=(etc/default/teamspeak3-server)
install='teamspeak3-server.install'
source=('teamspeak3-server.default'
        'teamspeak3-server.service')
source_i686=("http://teamspeak.gameserver.gamed.de/ts3/releases/$pkgver/teamspeak3-server_linux_x86-$pkgver.tar.bz2")
source_x86_64=("http://teamspeak.gameserver.gamed.de/ts3/releases/$pkgver/teamspeak3-server_linux_amd64-$pkgver.tar.bz2")
sha256sums=('bc52b851f5d7c878050e70661fafa8983031a43d115bc2762bae82f4331ee36e'
            '3d1b7c34e6d460d12f4bf51bdf96d2d58036493a969025fabd2b4ea38c9ac170')
sha256sums_i686=('2b8241052747ee8ce65b88ea7db689791c373dccc37832747600e5b2cc462c82')
sha256sums_x86_64=('24180a1a4c2e7d33b0574fa6b9860f25c248b96638410c01622c275e7284184a')

if [ "$CARCH" == "x86_64" ]; then
  _TSARCH='amd64'
elif [ "$CARCH" == "i686" ]; then
  _TSARCH='x86'
fi

package() {
    cd "$srcdir"

    install -Dm 644 teamspeak3-server.default "$pkgdir/etc/default/teamspeak3-server"
    install -Dm 644 teamspeak3-server.service "$pkgdir/usr/lib/systemd/system/teamspeak3-server.service"

    install -Dm 755 "teamspeak3-server_linux_$_TSARCH/ts3server" "$pkgdir/usr/bin/ts3server"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/libts3db_mariadb.so" "$pkgdir/usr/lib/libts3db_mariadb.so"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/libts3db_sqlite3.so" "$pkgdir/usr/lib/libts3db_sqlite3.so"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/LICENSE" "$pkgdir/usr/share/licenses/teamspeak3-server/LICENSE"

    mkdir -p "$pkgdir/usr/share/doc/teamspeak3-server" \
             "$pkgdir/usr/share/teamspeak3-server" \
             "$pkgdir/var/lib/teamspeak3-server" \
             "$pkgdir/var/log/teamspeak3-server"

    cp -a "teamspeak3-server_linux_$_TSARCH/doc/" "$pkgdir/usr/share/doc/teamspeak3-server/"
    cp -a "teamspeak3-server_linux_$_TSARCH/sql/" "$pkgdir/usr/share/teamspeak3-server/"

    find "$pkgdir/usr/share/teamspeak3-server" -type d -exec chmod 755 {} \;
    find "$pkgdir/usr/share/teamspeak3-server" -type f -exec chmod 644 {} \;
    find "$pkgdir/usr/share/doc/teamspeak3-server" -type d -exec chmod 755 {} \;
    find "$pkgdir/usr/share/doc/teamspeak3-server" -type f -exec chmod 644 {} \;

    chmod 750 "$pkgdir/var/lib/teamspeak3-server" \
              "$pkgdir/var/log/teamspeak3-server"
}
