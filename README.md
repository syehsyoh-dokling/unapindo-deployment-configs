# Unapindo Deployment Configs

Deployment configuration archive for Unapindo services.

This repository is intentionally separate from application code. It stores reverse-proxy and VPS deployment snippets so deployment concerns do not get mixed with API, worker, or frontend source code.

## Contents

```text
nginx-legacy/
  30.conf
  nginx_config
  nginx_unapi_config
  nginx_unapi_config_fixed
```

## What The Files Are For

- `30.conf`: Nginx Proxy Manager style host config for `unapi.danandad.org`, forwarding to port `8081`.
- `nginx_config`: direct Nginx server block for `apiutama.danandad.com`, forwarding to `localhost:3001`.
- `nginx_unapi_config`: direct Nginx server block for `unapi.danandad.org` on port `80`, forwarding to `localhost:3001`.
- `nginx_unapi_config_fixed`: alternate `unapi.danandad.org` config listening on `8081`.

## Usage

These files are reference configs. Review domain, port, SSL, upstream, and proxy settings before applying them to a live server.

Typical flow:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## Security Notes

- Do not commit `.env`, private keys, certificates, or server credentials.
- Keep production secrets in the server or secret manager.
- Treat these snippets as deploy templates, not automatically production-safe configs.
