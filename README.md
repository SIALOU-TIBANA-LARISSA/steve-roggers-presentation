# Steve Roggers — Gestion de services de piscine

## Présentation du projet

Steve Roggers est une application web destinée à une entreprise spécialisée dans la construction, l'entretien et la maintenance de piscines et de jacuzzis à Yamoussoukro, en Côte d'Ivoire.

Ce projet vise à faciliter la présentation des prestations, la gestion des demandes de devis et la prise de rendez-vous des clients.

L'application est composée de deux parties :

* Un frontend permettant aux visiteurs de découvrir les services de l'entreprise et d'interagir avec le site.
* Un backend fournissant une API REST pour traiter les demandes, gérer les données et sécuriser les opérations d'administration.

## Fonctionnalités

* Consultation des services proposés.
* Soumission de demandes de devis.
* Demande de rendez-vous.
* Gestion des projets réalisés.
* Gestion des articles.
* Gestion des témoignages clients.
* Soumission et modération des avis clients.
* Authentification des administrateurs.
* Protection des routes privées.
* Validation des données et gestion des erreurs.

### Fonctionnalités de l'administration

L'application dispose d'un espace d'administration permettant de centraliser la gestion des activités du site.

Cet espace comprend plusieurs interfaces :

* **Tableau de bord administrateur :** interface centrale permettant d'accéder aux différentes fonctionnalités de gestion.
* **Gestion des demandes de devis :** consultation et suivi des demandes de devis transmises par les visiteurs.
* **Gestion des avis clients :** consultation des avis reçus, approbation des avis et retrait des avis publiés sur le site.
* **Gestion des administrateurs :** interface dédiée à la gestion des comptes administrateurs.
* **Authentification :** connexion des administrateurs à l'aide de leurs identifiants.
* **Déconnexion :** fermeture de la session et suppression des informations d'authentification enregistrées côté frontend.

Les interfaces d'administration sont développées avec React et communiquent avec le backend Spring Boot pour accéder aux données et effectuer les opérations autorisées.

## Technologies utilisées

### Frontend

* React
* Vite
* JavaScript
* CSS
* npm

### Backend

* Java
* Spring Boot
* Spring Security
* Spring Data JPA
* Maven

### Base de données

* PostgreSQL

### Outils de développement

* Visual Studio Code
* Postman
* pgAdmin 4
* Git et GitHub

## Architecture du projet

Le projet est organisé en deux parties distinctes :

### Frontend

Le frontend est développé avec React et Vite. Il constitue l'interface utilisateur du site web et communique avec le backend à travers des requêtes HTTP vers l'API REST.

Le dossier du frontend est :

`frontend/`

Les principaux fichiers de l'application React se trouvent dans :

`frontend/src/`

Le fichier `main.jsx` initialise l'application et affiche le site public ou l'interface d'administration des avis clients en fonction du chemin demandé.

#### Organisation de l'administration

Les composants de l'administration sont regroupés dans le dossier :

`frontend/src/admin/`

Ce dossier contient notamment :

| Fichier                    | Rôle                                                        |
| -------------------------- | ----------------------------------------------------------- |
| `AdminLayout.jsx`          | Structure générale et navigation de l'espace administrateur |
| `AdminDashboard.jsx`       | Interface du tableau de bord administrateur                 |
| `AdminDevis.jsx`           | Interface de gestion des demandes de devis                  |
| `AdminAvis.jsx`            | Interface de gestion et de modération des avis clients      |
| `AdminAdministrateurs.jsx` | Interface de gestion des comptes administrateurs            |

Les fichiers CSS associés permettent de personnaliser l'apparence de chaque interface.

L'organisation de ces composants permet de séparer les différentes fonctionnalités administratives et de faciliter leur maintenance.

### Backend

Le backend est développé avec Java et Spring Boot. Il expose les routes de l'API REST, applique les règles métier, communique avec PostgreSQL et sécurise les opérations nécessitant une authentification.

Le backend est organisé en plusieurs couches :

* `controller` : gestion des requêtes HTTP et des réponses de l'API.
* `service` : logique métier de l'application.
* `repository` : accès aux données.
* `entity` : représentation des données stockées en base.
* `dto` : transfert et validation des données.
* `config` : configuration de la sécurité.

## Adresses locales — Frontend et Backend

Pendant le développement, les deux parties fonctionnent sur des serveurs locaux distincts.

| Composant                               | Adresse locale                         | Description                                             |
| --------------------------------------- | -------------------------------------- | ------------------------------------------------------- |
| Site web — Frontend                     | `http://localhost:5173`                | Interface publique du site                              |
| API REST — Backend                      | `http://localhost:8080`                | Serveur qui traite les requêtes du frontend             |
| Administration des avis — Frontend      | `http://localhost:5173/admin/avis`     | Interface de gestion des avis clients                   |
| API des avis — Backend                  | `http://localhost:8080/api/avis`       | Consultation des avis approuvés et soumission d'un avis |
| API d'administration des avis — Backend | `http://localhost:8080/api/avis/admin` | Consultation de tous les avis, avec authentification    |

Ces adresses sont utilisées en environnement local. Elles devront être adaptées lors du déploiement de l'application.

## API REST du Backend

Les routes principales de l'API utilisent le préfixe `/api/v1`.

### Routes principales

| Ressource         | Route                 | Fonction                            |
| ----------------- | --------------------- | ----------------------------------- |
| Services          | `/api/v1/services`    | Accès aux services                  |
| Projets           | `/api/v1/projets`     | Accès aux projets réalisés          |
| Articles          | `/api/v1/articles`    | Accès aux articles                  |
| Témoignages       | `/api/v1/temoignages` | Accès aux témoignages               |
| Demandes de devis | `/api/v1/devis`       | Gestion des demandes de devis       |
| Rendez-vous       | `/api/v1/rendez-vous` | Gestion des demandes de rendez-vous |

### Routes des avis clients

| Méthode HTTP | Route                              | Fonction                                      |
| ------------ | ---------------------------------- | --------------------------------------------- |
| `GET`        | `/api/avis`                        | Récupérer les avis approuvés                  |
| `POST`       | `/api/avis`                        | Soumettre un nouvel avis                      |
| `GET`        | `/api/avis/admin`                  | Récupérer tous les avis pour l'administration |
| `PATCH`      | `/api/avis/admin/{id}/approbation` | Modifier le statut d'approbation d'un avis    |

Les routes publiques permettent aux visiteurs de consulter les contenus autorisés et d'envoyer leurs demandes.

Les opérations d'administration nécessitent une authentification. Les routes d'administration des avis sont protégées par Spring Security.

### Gestion des administrateurs

Le backend intègre également des fonctionnalités dédiées à la gestion des comptes administrateurs.

Les composants concernés comprennent :

* `UtilisateurController.java` : contrôleur dédié aux opérations liées aux utilisateurs.
* `AdministrateurDTO.java` : objet de transfert des informations d'un administrateur.
* `CreationAdministrateurDTO.java` : objet de transfert des données nécessaires à la création d'un administrateur.
* `GestionUtilisateur.java` : service chargé de la gestion des utilisateurs.
* `UtilisateurDetailsService.java` : service utilisé pour retrouver les informations des utilisateurs lors de l'authentification.
* `InitialisationAdministrateurs.java` : initialisation des comptes administrateurs.

La configuration de Spring Security permet de contrôler les accès aux ressources protégées.

## Communication entre le Frontend et le Backend

Le frontend envoie des requêtes HTTP au backend pour récupérer ou transmettre les données.

Exemples :

* Consultation des avis approuvés : `GET http://localhost:8080/api/avis`
* Soumission d'un avis client : `POST http://localhost:8080/api/avis`
* Consultation des avis dans l'administration : `GET http://localhost:8080/api/avis/admin`
* Approbation ou retrait d'un avis : `PATCH http://localhost:8080/api/avis/admin/{id}/approbation`

Le frontend et le backend doivent tous les deux être démarrés pour que les fonctionnalités nécessitant l'API puissent fonctionner.

### Authentification de l'administration

L'espace administrateur dispose d'un mécanisme d'authentification permettant de contrôler l'accès aux fonctionnalités protégées.

Le processus comprend :

1. Saisie de l'adresse e-mail et du mot de passe par l'administrateur.
2. Transmission des informations d'authentification au backend.
3. Vérification des identifiants par Spring Security.
4. Accès aux données administratives après validation.
5. Conservation temporaire des informations d'authentification dans `sessionStorage` côté frontend.
6. Suppression des informations d'authentification lors de la déconnexion.

Pour la gestion des avis clients, les requêtes administratives transmettent les informations d'authentification dans l'en-tête HTTP `Authorization`.

Les accès non autorisés sont contrôlés par le backend.

## Installation et lancement

### Prérequis

* Java compatible avec la version configurée dans le projet.
* Maven ou le Maven Wrapper fourni avec le projet.
* PostgreSQL.
* Node.js et npm.
* Git.

### Récupérer le projet

```bash
git clone https://github.com/SIALOU-TIBANA-LARISSA/steveroggers.git
cd steveroggers
```

### Configuration de la base de données

Configure la connexion à PostgreSQL et les paramètres nécessaires dans la configuration locale du backend.

Vérifie que PostgreSQL est démarré et que la base de données attendue par l'application existe.

Ne publie jamais de mot de passe, de clé secrète ou d'identifiant sensible dans le dépôt GitHub.

### Lancer le Backend sous Windows

Ouvre un premier terminal à la racine du projet et exécute :

```powershell
.\mvnw.cmd spring-boot:run
```

Lorsque le serveur démarre correctement, le backend est accessible à l'adresse :

`http://localhost:8080`

### Lancer le Frontend

Ouvre un deuxième terminal et place-toi dans le dossier du frontend :

```powershell
cd frontend
npm install
npm run dev
```

Lorsque le serveur Vite démarre, le frontend est accessible à l'adresse :

`http://localhost:5173`

### Accéder à l'application

Pour accéder au site public :

`http://localhost:5173`

Pour accéder à l'interface d'administration des avis clients :

`http://localhost:5173/admin/avis`

Le backend doit rester démarré pendant l'utilisation des fonctionnalités du frontend qui communiquent avec l'API.

## Sécurité

* Les opérations d'administration sont protégées par Spring Security.
* Les données transmises par les utilisateurs doivent être validées par le backend.
* Les identifiants et secrets de connexion doivent rester confidentiels.
* Les paramètres de sécurité et les autorisations doivent être vérifiés avant le déploiement en production.
* Les informations d'authentification ne doivent jamais être publiées dans le dépôt GitHub.
* Les accès aux fonctionnalités administratives doivent être réservés aux utilisateurs autorisés.

## Tests

Le projet a été compilé avec succès à l'aide de Maven (`BUILD SUCCESS`).

Plusieurs routes de l'API, les validations des données et les mécanismes d'authentification ont également été testés avec Postman.

Les fonctionnalités de l'administration ont également fait l'objet de vérifications, notamment :

* L'accès à l'interface de gestion des avis clients.
* L'authentification des administrateurs.
* La consultation des avis reçus.
* L'approbation et le retrait des avis.
* La gestion des sessions de connexion et de déconnexion.
* L'accès aux différentes interfaces de gestion.

## Évolutions prévues

* Poursuite de l'intégration du frontend avec l'API.
* Finalisation et amélioration de l'interface d'administration.
* Vérification complète des fonctionnalités.
* Déploiement de l'application.
* Configuration des adresses de production et des paramètres de sécurité associés.

## Auteur

Projet développé par Sialou Tibana Larissa dans le cadre de la réalisation d'une application web de gestion de services de piscine.
