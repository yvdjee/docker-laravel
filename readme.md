```
$ cd volumes/proxy/certs/
$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout legacyseller.local.key -out legacyseller.local.crt
$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout dld.legacyseller.local.key -out dld.legacyseller.local.crt

```