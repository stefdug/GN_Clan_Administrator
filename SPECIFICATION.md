# Feature Specification: Clan GN Administrator

**Feature Branch**: `001-clan-gn-admin`  
**Created**: 2026-04-09  
**Status**: Draft  
**Input**: User description: "Une app web pour gérer les membres d'un clan de GN. Les membres peuvent saisir leurs présences avant événements, gérer leur inventaire d'objets et se voir attribuer des rôles dans le clan (front-line, backup, mission, politics, etc.). L'admin peut gérer les membres, les événements et voir une vue d'ensemble du clan et même attribuer des rangs (chef, assistant, etc.)."

## User Scenarios & Testing

### User Story 1 - Membre saisit sa présence pour un événement (Priority: P1)

Un membre du clan doit pouvoir confirmer ou annuler sa participation à un événement GN avant la date limite. C'est une fonctionnalité essentielle puisque les organisateurs ont besoin de connaître les effectifs prévisionnels pour préparer l'événement.

**Why this priority**: Sans confirmations de présences, les événements ne peuvent pas être organisés correctement. C'est le cœur métier de l'application.

**Independent Test**: Un utilisateur membre peut accéder à une liste d'événements à venir, sélectionner un événement et confirmer ou annuler sa participation en deux clics. L'application persiste cette décision et l'affiche ultérieurement.

**Acceptance Scenarios**:

1. **Given** un membre authentifié, **When** il consulte les événements à venir, **Then** il voit une liste des événements avec dates et lieux
2. **Given** un événement à venir, **When** le membre clique sur un événement, **Then** il voit le détail (titre, date, lieu, limite d'inscription) et peut confirmer sa présence
3. **Given** un membre ayant confirmé sa présence, **When** il change d'avis, **Then** il peut annuler sa participation avant la limite
4. **Given** la limite de confirmation dépassée, **When** un membre tente de confirmer, **Then** le système rejette la modification avec un message d'erreur explicite

---

### User Story 2 - Membre gère son inventaire d'objets (Priority: P1)

Un membre doit pouvoir lister ses objets personnels (équipements GN, armes, armures, etc.), ajouter de nouveaux objets et les marquer comme disponibles/indisponibles. Cela permet à l'admin et aux autres membres de savoir quel matériel est disponible pour les événements.

**Why this priority**: L'inventaire est crucial pour la préparation des événements GN. C'est une fonctionnalité MVPindépendante qui crée de la valeur.

**Independent Test**: Un membre peut accéder à son inventaire, ajouter un nouvel objet avec description et état, puis modifier ou supprimer des objets existants. Un autre membre peut consulter librement cet inventaire.

**Acceptance Scenarios**:

1. **Given** un membre authentifié, **When** il accède à son inventaire, **Then** il voit la liste de ses objets avec descriptions et états
2. **Given** un accès à l'inventaire, **When** le membre clique sur "Ajouter un objet", **Then** il peut saisir le nom, la description et l'état (disponible/indisponible)
3. **Given** un objet existant, **When** le membre clique sur modifier, **Then** il peut changer les détails et l'état
4. **Given** un objet, **When** le membre le marque indisponible, **Then** cet état est visible pour les autres et il ne peut être emprunté

---

### User Story 3 - Membre se voit attribuer un rôle dans le clan (Priority: P1)

Un membre doit avoir un ou plusieurs rôles attribués par l'admin (front-line, backup, mission, politics, etc.). Ces rôles définissent son objectif pendant les événements et sont visibles aux autres membres.

**Why this priority**: Les rôles sont fondamentaux pour le gameplay GN et l'organisation des événements. C'est une donnée centrale de l'application.

**Independent Test**: Un admin attribue un rôle "front-line" à un membre. Le membre connecté voit immédiatement ce rôle dans son profil. Les autres membres voient aussi ce rôle (visibilité publique ou restreinte selon la règle).

**Acceptance Scenarios**:

1. **Given** un membre authentifié, **When** il consulte son profil, **Then** il voit tous les rôles qui lui sont attribués
2. **Given** un admin, **When** il accède au profil d'un membre, **Then** il peut ajouter ou retirer des rôles parmi les rôles disponibles
3. **Given** un nouveau rôle attribué, **When** le membre se reconnecte, **Then** le rôle est persisté et visible
4. **Given** plusieurs rôles, **When** un membre les consulte, **Then** il comprend clairement chaque rôle et ses implications

---

### User Story 4 - Admin gère les membres du clan (Priority: P2)

L'admin doit pouvoir consulter la liste complète des membres, les modifier (nom, email, roles, rang), les désactiver ou les supprimer. Il peut aussi inviter de nouveaux membres.

**Why this priority**: La gestion des effectifs est importante mais peut être légèrement décalée après les fonctionnalités de base des membres eux-mêmes.

**Independent Test**: Un admin peut ajouter un nouveau membre en saisissant son email, accède à la liste complète des membres, clique sur un membre pour le modifier, change son rang ou ses rôles, puis confirme. Ces changements sont persistés.

**Acceptance Scenarios**:

1. **Given** un admin authentifié, **When** il accède à la gestion des membres, **Then** il voit une liste des membres avec (nom, email, rang, rôles, statut)
2. **Given** la liste des membres, **When** l'admin clique sur un membre, **Then** il peut éditer ses informations
3. **Given** l'interface d'édition, **When** l'admin change le rang (chef, assistant, membre), **Then** le changement est sauvegardé
4. **Given** l'interface d'édition, **When** l'admin sélectionne de nouveaux rôles, **Then** ils sont ajoutés au profil du membre
5. **Given** un membre, **When** l'admin clique "désactiver", **Then** le membre ne peut plus se connecter mais ses données restent

---

### User Story 5 - Admin gère les événements (Priority: P2)

L'admin doit créer, modifier et supprimer les événements GN. Pour chaque événement, il doit spécifier la date, le lieu, la limite d'inscription, la description et potentiellement les responsabilités par rôle.

**Why this priority**: Les événements sont le cœur de l'application, mais la gestion basique des membres (présences) est prioritaire.

**Independent Test**: Un admin crée un événement avec titre, date, lieu et limite d'inscription. Il le modifie ensuite. Les membres reçoivent une notification et peuvent confirmer leur présence.

**Acceptance Scenarios**:

1. **Given** un admin, **When** il clique sur "Créer un événement", **Then** un formulaire apparaît avec les champs requis
2. **Given** le formulaire de création, **When** l'admin remplit titre, date, lieu, limite, **Then** l'événement est créé
3. **Given** un événement créé, **When** l'admin le sélectionne, **Then** il peut le modifier ou le supprimer
4. **Given** un événement modifié, **When** l'admin change la date ou le lieu, **Then** les membres reçoivent une notification

---

### User Story 6 - Admin consulte une vue d'ensemble du clan (Priority: P2)

L'admin doit accéder à un tableau de bord affichant :
- Nombre total de membres et statuts (actifs/inactifs)
- Répartition des rôles (combien de "front-line", "backup", etc.)
- Prochains événements et taux de confirmation
- Graphiques de participation au fil des événements

**Why this priority**: Le tableau de bord offre une vision stratégique, important mais peut être itéré après les fonctionnalités critiques.

**Independent Test**: Un admin accède au tableau de bord et voit immédiatement : 25 membres (20 actifs), 40% front-line, 30% backup, etc. Il voit aussi "Événement X: 15/20 confirmés".

**Acceptance Scenarios**:

1. **Given** un admin au tableau de bord, **When** il charge la page, **Then** il voit les statistiques actualisées
2. **Given** le dashboard, **When** il consulte les événements, **Then** il voit le taux de confirmation pour chacun
3. **Given** des données historiques, **When** l'admin consulte les graphiques, **Then** il voit les tendances de participation

---

### User Story 7 - Admin attribue des rangs aux membres (Priority: P3)

L'admin doit pouvoir attribuer des rangs hiérarchiques aux membres : Chef, Assistant, Membre. Les rangs déterminent le niveau d'accès et de responsabilité.

**Why this priority**: Les rangs ajoutent une hiérarchie utile mais peuvent être gérés après la version 1.0 de base.

**Independent Test**: Un admin assigne le rang "Assistant" à un membre. Ce membre reçoit plus de permissions (peut voir certains rapports, modérer les messages, etc.).

**Acceptance Scenarios**:

1. **Given** un profil membre, **When** l'admin change le rang en "Chef", **Then** le système mnet à jour les permissions
2. **Given** un membre avec rang "Chef", **When** il se connecte, **Then** il accède aux fonctionnalités d'administration

---

### Edge Cases

- Que se passe-t-il si un événement est supprimé après qu'une personne ait confirmé sa présence ? (Les confirmations doivent être supprimées en cascade)
- Comment le système gère-t-il les doublons d'email lors de l'ajout de membres ?
- Que se passe-t-il quand la limite de confirmation est dépassée mais qu'un admin force une confirmation pour un membre ? (L'admin peut outrepasser la limite)
- Peut-on attribuer plusieurs rôles au même membre simultanément ? (Oui, c'est nécessaire)
- Que se passe-t-il si une personne supprime son propre compte ? (Confirmation nécessaire, données archivées)

## Requirements

### Functional Requirements

- **FR-001**: Système MUST permettre aux membres authentifiés de consulter une liste des événements à venir
- **FR-002**: Système MUST permettre aux membres de confirmer ou annuler leur participation à un événement avant la limite
- **FR-003**: Système MUST persister l'état de participation (confirmé/annulé) et afficher l'historique des participations
- **FR-004**: Système MUST empêcher les modifications de présences après la date limite de confirmation
- **FR-005**: Système MUST permettre à tout membre de visualiser et gérer son inventaire personnel d'objets
- **FR-006**: Système MUST permettre aux membres de créer, modifier et supprimer des objets dans leur inventaire
- **FR-007**: Système MUST permettre aux autres membres de consulter les inventaires publics (ou avec permissions)
- **FR-008**: Système MUST mantenir l'état (disponible/indisponible) de chaque objet
- **FR-009**: Système MUST attribuer un ou plusieurs rôles à chaque membre (front-line, backup, mission, politics, etc.)
- **FR-010**: Système MUST afficher les rôles d'un membre sur son profil, visible par lui et les autres
- **FR-011**: Système MUST permettre à l'admin de modifier les rôles d'un membre
- **FR-012**: Système MUST permettre à l'admin de consulter et filtrer la liste des membres
- **FR-013**: Système MUST permettre à l'admin de créer, modifier et supprimer des événements
- **FR-014**: Système MUST permettre à l'admin de définir une limite de confirmation pour chaque événement
- **FR-015**: Système MUST afficher un tableau de bord avec statistiques du clan (total membres, répartition des rôles)
- **FR-016**: Système MUST afficher sur le dashboard le taux de confirmation pour les événements à venir
- **FR-017**: Système MUST permettre à l'admin d'attribuer un rang (Chef, Assistant, Membre) à chaque membre
- **FR-018**: Système MUST limiter certaines fonctionnalités selon le rang de l'utilisateur
- **FR-019**: Système MUST supporter l'authentification des utilisateurs (email/mot de passe ou SSO)
- **FR-020**: Système MUST valider les adresses email au format correct
- **FR-021**: Système MUST permettre la réinitialisation de mot de passe
- **FR-022**: [NEEDS CLARIFICATION: Quel système d'authentification utiliser ? Email/mot de passe, OAuth, SSO d'entreprise ?]
- **FR-023**: [NEEDS CLARIFICATION: Quel système de permissions faut-il au-delà des rangs ? Rôles granulaires ?]
- **FR-024**: Système MUST journaliser les modifications importantes (changements de rang, suppression de membres, création d'événements)
- **FR-025**: Système MUST persister toutes les données de manière durable (base de données appropriée)

### Key Entities

- **User (Membre)**: ID, email, nom, mot de passe, rang (Chef/Assistant/Membre), rôles[], statut (actif/inactif), créé_at, modifié_at
- **Event (Événement)**: ID, titre, description, date, lieu, limite_confirmation, créé_par, créé_at, modifié_at, supprimé_at (soft delete)
- **Attendance (Participation)**: ID, user_id, event_id, statut (confirmé/annulé), confirmé_at, annulé_at
- **Role (Rôle)**: ID, nom (front-line, backup, mission, politics, etc.), description, permissions[]
- **UserRole**: user_id, role_id, attribué_par, attribué_at
- **Inventory Item (Objet inventaire)**: ID, user_id, nom, description, état (disponible/indisponible), créé_at, modifié_at
- **Rank (Rang)**: ID, nom (Chef, Assistant, Membre), niveau_hiérarchique, permissions[]

## Success Criteria

### Measurable Outcomes

- **SC-001**: Au moins 90% des membres peuvent confirmer leur présence à un événement en moins de 30 secondes
- **SC-002**: Un admin peut créer un nouvel événement en moins de 2 minutes
- **SC-003**: Le tableau de bord charge les statistiques en moins de 2 secondes
- **SC-004**: L'inventaire affiche la liste complète d'objets pour 100+ objets en moins de 1 seconde
- **SC-005**: Le système peut gérer 500+ membres actifs simultanément sans dégradation visible
- **SC-006**: 95% des opérations critiques (confirmation de présence, ajout d'objet) s'effectuent sans erreur
- **SC-007**: Les modifications d'admin sont visibles par les utilisateurs concernés en moins de 5 secondes (temps de propagation)
- **SC-008**: Au moins 80% des utilisateurs réussissent à utiliser l'application sans aide lors duonboarding

## Assumptions

- Les utilisateurs ont une connexion internet stable
- L'authentification peut être implémentée avec email/mot de passe dans la v1 (OAuth/SSO peut être ajouté plus tard)
- Tous les utilisateurs ont accès via un navigateur web moderne (Chrome, Firefox, Safari, Edge)
- L'application fonctionne en priorité sur desktop, responsive mobile en v1 mais optimisé en v2
- Les événements ne sont pas supprimés mais archivés (soft delete) pour conserver l'historique
- Les utilisateurs peuvent consulter librement les profils et inventaires des autres (visibilité publique par défaut)
- Les rôles sont gérés par l'admin initiale, les membres ne peuvent pas les modifier eux-mêmes
- La suppression d'un compte par un membre nécessite une confirmation et archive les données
- Les notifications (confirmation d'événement, changements) sont optionnelles pour la v1
- Pas de système de chat/messagerie dans la v1, focus sur gestion de données
- Pas de système de paiement ou de cotisation dans la v1
- Pas de gestion des localisations/fuseaux horaires complexes dans la v1
