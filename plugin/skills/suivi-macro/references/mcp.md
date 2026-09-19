# Serveur MCP du backend — brancher un client

Le backend expose ses opérations en outils MCP sur `https://suivi-macro-backend.vercel.app/mcp` (transport Streamable HTTP, sans état). C'est l'unique porte de la skill : Claude Desktop, claude.ai, ChatGPT et Claude Code s'y branchent, sans script ni fichier local.

## Préalable : un compte dans le foyer

Le propriétaire du foyer crée le compte de la personne, avec son e-mail, depuis le dépôt du backend :

```bash
pnpm admin account create --email liliya@example.org --name Liliya
pnpm admin member add --household <id-foyer> --account <id-compte> --role member
```

Rien d'autre à transmettre : la personne se connecte avec cet e-mail. Un e-mail sans compte reçoit « compte inconnu ».

## Claude Desktop, claude.ai, Claude mobile

1. *Paramètres → Connecteurs → Ajouter un connecteur personnalisé* : nom libre, URL `https://suivi-macro-backend.vercel.app/mcp`. Authentification : *Se connecter maintenant* ; client OAuth : *S'enregistrer automatiquement*.
2. Une page « Suivi Macro » s'ouvre : saisis ton e-mail, ouvre le lien reçu (valable une heure, usage unique, à ouvrir depuis le même navigateur), puis clique **Autoriser**.
3. C'est fait pour de bon : le renouvellement est silencieux. Tu refais le parcours seulement si tu retires le connecteur.

Le connecteur est partagé par les applications Claude (web, Desktop, mobile) d'un même compte.

## ChatGPT

*Paramètres → Connecteurs → Créer* (mode développeur) : même URL, authentification OAuth. Même parcours de connexion (e-mail, lien, Autoriser).

## Claude Code

Sans OAuth, avec un jeton personnel remis par le propriétaire du foyer :

```bash
claude mcp add -s user --transport http suivi-macro https://suivi-macro-backend.vercel.app/mcp --header "Authorization: Bearer sm_…"
```

Le jeton se crée côté backend (`pnpm admin token create …`). Ne l'écris jamais dans un dépôt ni dans une réponse.

## Les outils

Le serveur publie ses outils avec leur description et leur schéma : c'est la référence, lue par le client au branchement. Ce fichier n'en tient pas de liste. Prépas et frigo ne sont pas pris en charge : un besoin de ce genre se note avec l'outil de registre des besoins.

## Si les outils n'apparaissent pas

Le serveur n'est pas branché sur ce client, ou la connexion a été retirée : refaire le branchement ci-dessus. Vérification côté serveur : `https://suivi-macro-backend.vercel.app/health` doit répondre `{"status":"ok","db":"ok"}`.
