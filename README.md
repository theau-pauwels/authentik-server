# Authentik Server

Serveur d'identité central destiné aux applications de la Fédération des étudiants Polytech.

Authentik gère l'identité, l'authentification et le SSO. Les applications gardent leurs données et permissions métier. Chaque application associe son utilisateur local au claim OIDC stable `sub` via `authentik_sub`.

## Développement local

```bash
cp .env.example .env
docker compose up -d
```

Assistant initial : `http://localhost:9000/if/flow/initial-setup/`.

## Production

Le Compose est réservé au développement/test. La production sera gérée dans `Commission-Web-FPMs/k8s-cluster` via Argo CD, Helm, CloudNativePG, Traefik/Gateway API et Sealed Secrets.

## Documentation

- `docs/architecture.md`
- `docs/oidc.md`
- `docs/migration-carte.md`
