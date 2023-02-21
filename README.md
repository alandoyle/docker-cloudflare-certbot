# docker-cloudflare-certbot
Simple set of docker compose files to create and renew certbot certificates.

## Getting started

 - Clone this repository to **/srv** as `root`
 - Generate a Cloudflare API Token (see https://alandoyle.dev/blog/docker-cloudflare-certbot/ for details how)
 - Run `sudo ./install`
   - Enter the Cloudflare API Token when requested.
   - This installs a "Renew Certificates" cron job for root.
   - This also installs 3 new commands to `/usr/local/bin` to create/renew certificates manually.

## Commandline tools

### renew-certs
This simply attempts to renew all certificates on the system.

e.g. `sudo renew-certs`

### test-certbot
This script simply checks the configuration is all set and working

e.g. `sudo test-certbot <DOMAIN CONTROLLED BY API TOKEN>`

### test-certbot
This script generates a new certificate (with optional wildcard subdomains entry)

e.g. `sudo gen-cert <DOMAIN CONTROLLED BY API TOKEN>`

or to include wildcard subdomains in certificate `sudo gen-cert -w <DOMAIN CONTROLLED BY API TOKEN>`

## Note

  - All commands *MUST* be run as `root`, either directly or via *sudo*, as the certificates are generated in `/etc/letsencrypt` on the host machine. This allows the host machine as well as all local docker/LXC/LXD containers can access the certificates, if `/etc/letsencrypt` is mapped into those containers.
