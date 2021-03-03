# Guide to certbot configuration on Debian/Nginx servers (Sectigo example)

- remove existing certbot installations `apt-get remove certbot`
- install snap [https://snapcraft.io/docs/installing-snapd](https://snapcraft.io/docs/installing-snapd)
- install from snap to obtain latest version `snap install --classic certbot`
- IMPORTANT: check that your version is the latest `certbot --version`. If result is not the expected, may be you have an existing installation that wasn't purged. In this case you can make these commands, `usr/bin/certbot` and `usr/local/bin/certbot`, point to the following `/snap/bin/certbot`. Try now to check version and if this is the latest go ahead. 
- register your ACME account 
```
certbot register --email <EMAIL_RAO> --server https://acme.sectigo.com/v2/OV --eab-kid <KEY ID> --eab-hmac-key <HMAC KEY>
```
- create certificates
```
certbot run --nginx --email [your email] --server https://acme.sectigo.com/v2/OV --domain [your@domain.ext] --rsa-key-size 3072
```
- auto renew command is installed in one of the following locations:

  - `/etc/crontab/`
  - `/etc/cron.*/*`
  - `systemctl list-timers`

### References

- GARR Consortium GARRCS:GARR-TCS-4 [https://wiki.idem.garr.it/wiki/GARRCS:GARR-TCS-4#Creazione_account_ACME_su_SCM](https://wiki.idem.garr.it/wiki/GARRCS:GARR-TCS-4#Creazione_account_ACME_su_SCM)
- Certbot official site [https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx.html](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx.html)
