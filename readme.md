# Atelier : Concevoir une application en architecture logicielle en couches

## Date du projet et équipe
**16 décembre 2024**

   - Nina Guiguet
   - Julien Vaglia
   - Angie Pons
   - Ludovic Andreotti
   - Catherine Jules

## Objectif
Dans cet atelier, nous avons conçu l'architecture logicielle d’une application en couches pour un système de gestion de bibliothèque.  
L'objectif principal était de :
- Comprendre et formaliser les rôles de chaque couche.
- Appliquer les principes de modularité et de séparation des préoccupations.
- Structurer le projet de manière claire et cohérente.

---

## Contexte métier
L'application vise à gérer les **livres**, les **utilisateurs**, et les **emprunts**, tout en respectant des règles métier spécifiques.  
Voici les principales fonctionnalités demandées :

### Fonctionnalités :
1. **Gestion des livres** :
   - Ajouter, modifier, supprimer un livre.
   - Consulter la liste des livres disponibles.
   - Rechercher un livre par titre ou par auteur.
   
2. **Gestion des utilisateurs** :
   - Ajouter, modifier, supprimer un utilisateur.
   - Rechercher un utilisateur par son nom ou identifiant.

3. **Gestion des emprunts** :
   - Enregistrer un emprunt (vérification de disponibilité).
   - Retourner un livre.
   - Empêcher un emprunt si le livre n’est pas disponible.

4. **Gestion des pénalités** :
   - Calculer une pénalité en cas de retard.
   - Afficher ou apurer une pénalité.

5. **Statistiques** :
   - Nombre de livres disponibles/empruntés.
   - Nombre total d’emprunts par mois.
   - Livres les plus empruntés.

---

## Architecture en Couches

Le projet suit une architecture en **trois couches principales**, avec une séparation claire des responsabilités :

1. **Couche Présentation (Presentation)**  
   Responsable de l’interface utilisateur et des interactions. Elle contient :
   - Les pages et interfaces (ex. `Dashboard.html`).
   - Les gestionnaires de vues pour les actions métier (ex. `BookManagement.ts`).

2. **Couche Métier (Business)**  
   Gère la logique métier et les règles associées. Elle inclut :
   - Les modèles de données (DTO) comme `BookModel.js`, `UserModel.js`.
   - Les workflows pour les fonctionnalités métier (ex. `BookQueries.ts`, `LoanQueries.ts`).

3. **Couche Persistance (Persistence)**  
   Responsable de l’accès aux données et des opérations CRUD. Elle inclut :
   - Les modèles persistants pour représenter les entités telles qu'elles sont stockées en base de données (ex. `BookModel.md`, `UserModel.md`).
   - Les repositories pour chaque entité, qui fournissent des méthodes pour interagir avec les données (lecture, écriture, suppression, etc.).   
   
---

## Organisation de l'arborescence

```text
1_Presentation/                   # Couche de présentation : Interface utilisateur.
├── AdminManagement/
│   ├── BookManagement.md         # Logique pour afficher et gérer les actions liées aux livres.
│   ├── LoanManagement.md         # Logique pour afficher et gérer les actions liées aux emprunts.
│   ├── PenalityManagement.md     # Logique pour afficher et gérer les actions liées aux pénalités.
│   ├── Statistics.md             # Logique pour afficher les statistiques (d'emprunts, de livres disponibles, de popularité des livres).
│   └── UserManagement.md         # Logique pour afficher et gérer les actions liées aux utilisateurs.
├── Pages/
│   └── AdminPage/
│       └── Dashboard.html        # Page représentant l'interface du tableau de bord administrateur.
│
2_Business/                       # Couche de logique métier : Règles de gestion et manipulations principales.
├── DTO/
│   ├── BookModel.md              # Modèle représentant un livre (id, titre, auteur, disponibilité).
│   ├── LoansModel.md             # Modèle représentant un emprunt (utilisateur, livre, dates, statut).
│   ├── PenalityModel.md          # Modèle représentant une pénalité (livre, utilisateur, montant, paiement).
│   └── UserModel.md              # Modèle représentant un utilisateur (id, nom, emprunts, pénalités).
└── workflow/
│   ├── BookQueries.md            # Logique pour manipuler les livres (CRUD, recherche).
│   ├── LoanQueries.md            # Logique pour gérer les emprunts (ajout, modification, suppression).
│   ├── PenalitiesQueries.md      # Logique pour gérer les pénalités (calcul, ajout, suppression).
│   ├── StatisticQueries.md       # Logique pour générer des statistiques (emprunts, livres disponibles, popularité).
│   └── UsersQueries.md           # Logique pour gérer les utilisateurs (création, récupération, suppression).
│
3_Persistence/                    # Couche de persistance : Modèles et accès aux données.
└── Repository/
    ├── Books/
    │   └── Model/
    │       └── BookModel.md      # Modèle persistant pour un livre dans la base de données.
    ├── Loans/
    │   └── Model/
    │       └── LoansModel.md     # Modèle persistant pour un emprunt dans la base de données.
    ├── Penalities/
    │   └── Model/
    │       └── PenalityModel.md  # Modèle persistant pour une pénalité dans la base de données.
    └── Users/
        └── Model/
            └── UserModel.md      # Modèle persistant pour un utilisateur dans la base de données.

```

## Architecture en Couches

Voici le diagramme de l'architecture en couches :

![Diagramme d'architecture](https://kroki.io/plantuml/svg/eNp1U8tu4zAMvOsrCOeSPTS9FIu2aAL0cVmgi7qvU3cPskw72jiSK8koioX_p_2O_FgpO47lxDUQwxkOSc2QKjBz4DQYmS8dpNKgcFIrxvwHV3mBEF0ki2tdiSVCbNCictxTLo6TxR_1Szk0GRcIlZOFtNxhZSLgdsCFiTjFn-LsPwMouVjxnMrG9LYReCxAL9O1VD7URQCmN9wuE81NOlu6dfGjgWvW_IZ5v7miP2tq22VPr7Re9fDM2TZ9equ5GsNjVLyQ7n0s9ujVWCeF7bFni-aAW7N63MCrykqF1rbm3epcvlYI682nk9ja1jFgkmXZmTghGWwn8ubpbihMp1jM_oWa7B620zOEm2MHUN03edNmlRX6bdDpvkIj0Q79OwC3zQg7CO28O4j4o-zxa8K_szAmNhVCJbB1cQtwAtrF6wkwSZIUs4SEBLUesNRWOm3eSSIEO-SF2hGDu6EGa9pYvaWGvo9Qe1M6fszDmYykNJZ07H5UnulXi7GX4ZX4C0dHC9i7AnBOhZpLiRHbj83nC-gG7YmXZYlFxHaQj4dGEuVh8ymqcvNhENABKoM5RQ0GWXQIWtFB4-75Ala7aXE=)




