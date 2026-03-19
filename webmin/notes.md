local tarafından webmin arayüzüne girip ssl kapatmak lazım
listen=127.0.0.1

/etc/webmin/miniserv.conf dosyası içerisinde ssl zorlamasını iptal etmen gerekiyor.

referers=domain name

/etc/webmin/config
npm tarafına alttaki gibi eklemek lazım.

domain names: webmin.soydan.fun
forward hostname: http://192.168.1.x:10000