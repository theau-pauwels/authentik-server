# Migration de Carte Fédé

Source : `Commission-Web-FPMs/carte-fede`.

Carte possède une table `user` et les cartes sont dans `membership`, liées par `membership.user_id -> user.id`.

## Règle principale

Ne pas remplacer `user.id` par l'identifiant Authentik. Ajouter `user.authentik_sub`.

```text
Authentik sub
      |
User.authentik_sub
User.id
      |
Membership.user_id
```

## Ordre de migration

1. Sauvegarder PostgreSQL Carte.
2. Ajouter `authentik_sub` nullable, unique et indexé.
3. Importer les utilisateurs dans Authentik.
4. Rapprocher en priorité les comptes par `member_id` et traiter explicitement les exceptions.
5. Enregistrer le `sub` correspondant.
6. Produire un rapport des comptes associés, ambigus et non associés.
7. Créer le provider OIDC Carte.
8. Ajouter login et callback OIDC au backend Flask.
9. Retrouver le User par `authentik_sub`, puis utiliser `login_user(user)`.
10. Vérifier cartes, rôles et QR codes.
11. Désactiver progressivement login/register/reset-password locaux.
12. Conserver temporairement `password_hash` pour le rollback.
13. Migrer ensuite, séparément, PostgreSQL Carte vers CloudNativePG.
14. Supprimer l'ancien système de mots de passe après validation finale.
