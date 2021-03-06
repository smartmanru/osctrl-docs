+++
title = "provision.sh"
date = 2019-08-11T13:16:09+02:00
weight = 4
pre = ""
+++

[provision.sh](https://github.com/jmpsec/osctrl/blob/master/deploy/provision.sh) is the provisioning script for **osctrl** in Ubuntu 18.04. It uses several functions from [lib.sh](https://github.com/jmpsec/osctrl/blob/master/deploy/lib.sh).

Its purpose is to install all necessary components to deploy **osctrl** in an Ubuntu 18.04 system, although it could be easily adapted to work in CentOS 7.

Execute `./deploy/provision.sh [-h|--help]` to show the usage of the script:

```properties
$ ./deploy/provision.sh -h

Usage: ./deploy/provision.sh [-h|--help] [PARAMETER [ARGUMENT]] [PARAMETER [ARGUMENT]] ...

Parameters:
  -h, --help 		Shows this help message and exit.
  -m MODE, --mode MODE 	Mode of operation. Default value is dev
  -t TYPE, --type TYPE 	Type of certificate to use. Default value is self
  -p PART, --part PART 	Part of the service. Default is all

Arguments for MODE:
  dev 		Provision will run in development mode. Certificate will be self-signed.
  prod 		Provision will run in production mode.
  update 	Provision will update the service running in the machine.

Arguments for TYPE:
  self 		Provision will use a self-signed TLS certificate that will be generated.
  own 		Provision will use the TLS certificate provided by the user.
  certbot 	Provision will generate a TLS certificate using letsencrypt/certbot. More info here: https://certbot.eff.org/

Arguments for PART:
  admin 	Provision will deploy only the admin interface.
  tls 		Provision will deploy only the TLS endpoint.
  all 		Provision will deploy both the admin and the TLS endpoint.

Optional Parameters:
  --public-tls-port PORT 	Port for the TLS endpoint service. Default is 443
  --public-admin-port PORT 	Port for the admin service. Default is 8443
  --private-tls-port PORT 	Port for the TLS endpoint service. Default is 9000
  --private-admin-port PORT 	Port for the admin service. Default is 9001
  --tls-hostname HOSTNAME 	Hostname for the TLS endpoint service. Default is 127.0.0.1
  --admin-hostname HOSTNAME 	Hostname for the admin service. Default is 127.0.0.1
  -X PASS     --password 	Force the admin password for the admin interface. Default is random
  -U          --update 		Pull from master and sync files to the current folder
  -c PATH     --certfile PATH 	Path to supplied TLS server PEM certificate(s) bundle
  -d DOMAIN   --domain DOMAIN 	Domain for the TLS certificate to be generated using letsencrypt
  -e EMAIL    --email EMAIL 	Domain for the TLS certificate to be generated using letsencrypt
  -s PATH     --source PATH 	Path to code. Default is /vagrant
  -S PATH     --dest PATH 	Path to binaries. Default is /opt/osctrl
  -n          --nginx 		Install and configure nginx as TLS termination
  -P          --postgres 	Install and configure PostgreSQL as backend
  -M          --metrics 	Install and configure all services for metrics (InfluxDB + Telegraf + Grafana)
  -E          --enroll  	Enroll the serve into itself using osquery. Default is disabled

Examples:
  Provision service in development mode, code is in /vagrant and both admin and tls:
	./deploy/provision.sh -m dev -s /vagrant -p all
  Provision service in production mode using my own certificate and only with TLS endpoint:
	./deploy/provision.sh -m prod -t own -k /etc/certs/my.key -c /etc/certs/cert.crt -p tls
  Update service in development mode and running admin only from /home/foobar/osctrl:
	./deploy/provision.sh -U -s /home/foobar/osctrl -p admin
```
