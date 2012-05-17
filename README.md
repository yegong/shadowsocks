shadowsocks
===========

shadowsocks is a lightweight tunnel proxy which can help you get through firewalls

usage
-----------

Put `server.py` on your server. Edit `server.py`, change the following values:

    PORT           server port
    KEY            a password to identify clients
    ENABLE_SSL     whether to use ssl. please see SSL section for more information
    SSL_KEY_FILE   ssl key file
    SSL_CERT_FILE  ssl cert file

Run `python server.py` on your server. To run it in the background, run `setsid python server.py`.

If you want to listen to IPv6 port, run `python server.py -6`.

Put `local.py` on your client machine. Edit `local.py`, change these values:

    SERVER         your server ip or hostname
    REMOTE_PORT    server port
    PORT           local port
    KEY            a password, it must be the same as the password of your server
    ENABLE_SSL     whether to use ssl

Run `python local.py` on your client machine.

Change proxy settings of your browser into

    SOCKS5 127.0.0.1:PORT

SSL
------------

If you want to use SSL, please generate your own key and cert.

    openssl genrsa -des3 -out server.key 1024
    openssl req -new -key server.key -out server.csr
    cp server.key server.key.org
    openssl rsa -in server.key.org -out server.key
    openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
