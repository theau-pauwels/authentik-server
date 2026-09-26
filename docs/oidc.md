# Contrat OIDC des applications Fédé

Chaque application possède son propre client/provider OIDC dans Authentik et utilise Authorization Code Flow.

L'identité locale doit être liée au claim stable `sub`. Les claims `preferred_username`, `email` et `name` peuvent servir à afficher ou synchroniser des informations, mais ne remplacent pas `sub`.

## Exemple Flask

```text
/login
  -> Authentik
  -> callback OIDC
  -> validation du token
  -> lecture de sub
  -> recherche de authentik_sub
  -> login_user(user)
```

Cela permet de conserver Flask-Login, `current_user` et `@login_required`. Les rôles métier restent dans les applications.
