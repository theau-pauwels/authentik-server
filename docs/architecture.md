# Architecture

Authentik est le fournisseur d'identité commun : il détermine qui est l'utilisateur. Chaque application détermine ensuite ce qu'il peut faire.

Authentik gère comptes, mots de passe, SSO, MFA éventuel et providers OIDC/OAuth2. Les applications conservent rôles, autorisations et données métier.

## Identifiant commun

Le claim OIDC `sub` est l'identifiant externe stable. Le matricule ne doit pas servir de clé étrangère inter-applications.

```text
Authentik: sub = abc123, username = 230466
        |
        +-- Carte Fédé: authentik_sub = abc123
        +-- CAP:        authentik_sub = abc123
```

## Production cible

```text
Reverse proxy HTTPS
        |
MetalLB / Traefik
        |
Gateway API
        |
Authentik
        |
CloudNativePG
```

Les manifests de production appartiennent au dépôt `k8s-cluster`.
