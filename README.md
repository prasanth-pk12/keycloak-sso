# Keycloak Local HTTPS Test (DNS-01 + Traefik)

This project demonstrates a **fully local HTTPS setup** using:
- Private IP (`127.0.0.1`)
- Public DNS (`keycloak.prasanth.dev`)
- Traefik reverse proxy
- Let's Encrypt (DNS-01 challenge)
- Keycloak (behind proxy)

## Architecture

Browser → keycloak.prasanth.dev → 127.0.0.1 → Traefik → Keycloak

Traefik obtains certificates using **DNS-01**, so no public server access is required.

## Prerequisites

1. Public domain `prasanth.dev`
2. DNS provider with API access (example: Cloudflare)
3. DNS API token with:
   - Zone: Read
   - DNS: Edit
4. Hosts file entry:
   ```
   127.0.0.1 keycloak.prasanth.dev
   ```

## Files

- `docker-compose.yml` – Services definition
- `traefik.yml` – Traefik static configuration
- `.env.example` – Environment variables template
- `acme.json` – Certificate storage (auto-generated)

## Run

```bash
cp .env.example .env
docker compose up -d
```

Then open:
```
https://keycloak.prasanth.dev
```

## Stop

```bash
docker compose down
```

## Notes

- Uses DNS-01 challenge (works with private IPs)
- For testing, prefer Let's Encrypt **staging CA**
- `acme.json` must have `600` permissions

