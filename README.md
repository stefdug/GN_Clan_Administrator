# GN Clan Administrator

Application web pour gérer les membres d'un clan de jeux de rôle grandeur nature (GN).

## Features

### Pour les Membres
- 📝 **Gestion des présences** : Confirmer ou annuler sa participation aux événements
- 🎒 **Inventaire personnel** : Gérer ses objets, équipements et armes
- 🎭 **Rôles assignés** : Visualiser ses rôles dans le clan (front-line, backup, mission, politics, etc.)

### Pour les Administrateurs
- 👥 **Gestion des membres** : Ajouter, modifier, désactiver les membres et attribuer les rangs
- 📅 **Gestion des événements** : Créer et gérer les événements GN
- 📊 **Tableau de bord** : Vue d'ensemble du clan (statistiques, taux de participation)
- ⭐ **Attribution de rangs** : Chef, Assistant, Membre avec permissions différentes

## Documentation

- [SPECIFICATION.md](./SPECIFICATION.md) - Spécification complète des fonctionnalités (user stories, requirements, success criteria)

## Project Structure

```
├── README.md                 # This file
├── SPECIFICATION.md          # Feature specification
├── .specify/                 # Spec-kit configuration
│   ├── init-options.json    # Spec-kit initialization
│   ├── integration.json     # Integration configuration
│   ├── extensions.yml       # Extensions and hooks
│   └── templates/            # Specification templates
├── .github/
│   └── prompts/             # GitHub Copilot prompts
└── .vscode/                 # VS Code configuration
```

## Development

This project uses [Spec-kit](https://github.com/speckit-io/speckit) for applying specification-driven development (SDD) methodology.
