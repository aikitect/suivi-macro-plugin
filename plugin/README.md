# suivi-macro — plugin Claude

Coach nutrition et suivi macro-nutritionnel d'un foyer. Ce plugin embarque la **skill** (le comportement du coach) et le **connecteur MCP** du backend (`https://suivi-macro-backend.vercel.app/mcp`). Une installation, les deux. Aucun secret dedans : la connexion est personnelle, par e-mail et lien magique, au premier appel.

## Installer

- **Claude (web, Desktop)** : *Paramètres → Plugins → Ajouter → Ajouter une place de marché* : `aikitect/suivi-macro-plugin`, puis installer `suivi-macro`. Ou *Téléverser un plugin* avec le fichier `suivi-macro.plugin` d'une release.
- **Claude Code** : `claude plugin marketplace add aikitect/suivi-macro-plugin` puis `claude plugin install suivi-macro@suivi-macro`.

## Préalable

Un compte dans le foyer, créé par le propriétaire du backend. Détails et branchement par client : `plugin/skills/suivi-macro/references/mcp.md`.

## Source

La skill vit ici (`plugin/skills/suivi-macro/`). Le backend est dans `aikitect/suivi-macro-backend` (privé) ; un test y vérifie que la skill respecte ses exigences.
