# docker-cloudflare-certbot
Simple set of docker compose files to create and renew certbot certificates.

## Getting started

 - Generate a Cloudflare API Token (see https://alandoyle.com/blog/docker-cloudflare-certbot/ for details how)
 - Run `sudo bash -c "$(curl -sSfL https://raw.githubusercontent.com/alandoyle/docker-cloudflare-certbot/main/install)"`
   - Enter the email address to use with Lets Encrypt when requested.
   - Enter the Cloudflare API Token when requested.
   - This installs a "Renew Certificates" cron job for root.
   - This also installs 3 new commands to `/usr/local/bin` to create/renew certificates manually.

## Commandline tools

### renew-certs
This simply attempts to renew all certificates on the system.

Example:
  - `sudo renew-certs`

### test-certbot
This script simply checks the configuration is all set and working

Example:
  - `sudo test-certbot <DOMAIN CONTROLLED BY API TOKEN>`

### gen-cert
This script generates a new certificate.

***-w*** adds wildcard subdomains to the certificate.
***-m*** adds multiple domains/subdomains to the certificate without wildcards.

Examples:
  - `sudo gen-cert <DOMAIN CONTROLLED BY API TOKEN>`
  - `sudo gen-cert -w <DOMAIN CONTROLLED BY API TOKEN>`
  - `sudo gen-cert -m <DOMAIN CONTROLLED BY API TOKEN> <SUBDOMAIN CONTROLLED BY API TOKEN> <ANOTHER SUBDOMAIN CONTROLLED BY API TOKEN>`
  - `sudo gen-cert -m <DOMAIN CONTROLLED BY API TOKEN> <ANOTHER DOMAIN CONTROLLED BY API TOKEN> <YET ANOTHER DOMAIN CONTROLLED BY API TOKEN>`

## Note

  - All commands *MUST* be run as `root`, either directly or via *sudo*, as the certificates are generated in `/etc/letsencrypt` on the host machine. This allows the host machine as well as all local docker/LXC/LXD containers can access the certificates, if `/etc/letsencrypt` is mapped into those containers.
  - This also assumes that `docker` and `docker-compose` are installed and working.
