# tailscale-caddy-custom-domains

This repo contains the install script to setup Caddy with custom domains in conjunction with Tailscale to provide secure remote access to self-hosted services.
We're going to use Tailscale and the reverse proxy Caddy to share self-hosted services on your Tailnet with friends family.

## Links

+ [Cloudflare - Generating a Cloudflare API token documentation](https://developers.cloudflare.com/fundamentals/api/get-started/create-token/)
+ [Caddy - Reverse proxy quick start](https://caddyserver.com/docs/quick-starts/reverse-proxy)
+ [Tailscale - Running Tailscale in LXC containers](https://tailscale.com/kb/1130/lxc-unprivileged)

# Cloudflare Dashboard

- Ensure there is a wildcard (*) CNAME record pointing at the FQDN of the container exposed on the tailnet
- Ensure the Caddyfile is formatted with ```caddy fmt /etc/caddy/Caddyfile --overwrite```
- Start caddyserver with the following commands

```
systemctl enable caddy
systemctl start caddy
```

The enable command only prepares the service for the next reboot. It will not launch the service in the current session or you can add the
```---now flag``` to simultaneously enable the service to start at boot *and* start it immediately.

```
systemctl enable --now caddy
```

## lsof -i :80 -s TCP:LISTEN

This will check if anything else is listening on port 80
If Apache 2 is running, disable it with

```
systemctl disable --now apache2
```

