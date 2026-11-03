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
* Neon : hébergement cloud de la base de données PostgreSQL en production.
* Beekeeper Studio : client graphique utilisé pour se connecter à Neon et consulter et gérer les données.

### Outils de développement

* Visual Studio Code
* Postman
* pgAdmin 4
* Beekeeper Studio
* Git et GitHub

## Architecture du projet

Le projet est organisé en deux parties distinctes :

### Frontend

Le frontend est développé avec React et Vite. Il constitue l'interface utilisateur du site web et communique avec le backend à travers des requêtes HTTP vers l'API REST.

Le dossier du frontend est :

`frontend/`

Les principaux fichiers de l'application React se trouvent dans :

`frontend/src/`

Le fichier `main.jsx` initialise l'application et affiche le site public ou l'interface d'administration en fonction du chemin demandé.

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

Ces adresses correspondent à l'environnement local de développement. En production, le frontend utilise l'URL du backend hébergé sur Render.

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

Le frontend et le backend doivent tous les deux être démarrés pour que les fonctionnalités nécessitant l'API puissent fonctionner en environnement local.

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

## Mise en production

L'application est déployée en ligne. Le frontend et le backend sont hébergés séparément sur Render, tandis que la base de données PostgreSQL est hébergée sur Neon.

### Adresses de production

| Composant                      | Adresse                                                      | Description                                    |
| ------------------------------ | ------------------------------------------------------------ | ---------------------------------------------- |
| Site web — Frontend            | `https://steveroggers-frontend.onrender.com`                 | Application React accessible aux visiteurs     |
| API REST — Backend             | `https://steveroggers.onrender.com`                          | API Spring Boot utilisée par le frontend       |
| API des devis                  | `https://steveroggers.onrender.com/api/v1/devis`             | Création et consultation des demandes de devis |
| API des avis clients           | `https://steveroggers.onrender.com/api/avis`                 | Soumission et consultation des avis clients    |
| Tableau de bord administrateur | `https://steveroggers-frontend.onrender.com/admin/dashboard` | Accès à l'espace d'administration              |

### Hébergement et rôle des outils

* **Render — Frontend :** héberge le site React/Vite sous forme de site statique.
* **Render — Backend :** héberge l'application Java Spring Boot et expose l'API REST.
* **Neon :** héberge la base de données PostgreSQL dans le cloud. Les demandes de devis et les avis clients sont enregistrés dans cette base par le backend.
* **Beekeeper Studio :** outil client utilisé pour se connecter à la base Neon, consulter les tables et vérifier les données. Beekeeper Studio ne sert pas à héberger la base de données.
* **GitHub :** héberge le dépôt du code source. Les modifications sont envoyées depuis le poste de développement avec Git. Le push sur la branche `master` déclenche le déploiement automatique configuré sur Render.

### Configuration des routes du frontend sur Render

Le frontend utilise React pour gérer les pages côté navigateur. Pour permettre l'accès direct aux routes de l'application et éviter une erreur `404` lors de l'ouverture ou de l'actualisation d'une page comme `/admin/dashboard`, une règle de réécriture (Rewrite) a été ajoutée dans les paramètres du site statique Render :

| Type      | Source | Destination   | Action    |
| --------- | ------ | ------------- | --------- |
| Règle SPA | `/*`   | `/index.html` | `Rewrite` |

Cette règle renvoie les requêtes de pages vers le point d'entrée HTML de l'application. React peut ensuite afficher la page correspondant au chemin demandé. L'URL affichée dans le navigateur est conservée.

### Communication frontend / backend en production

Les appels du frontend destinés au backend utilisent l'origine de production :

`https://steveroggers.onrender.com`

Les principaux endpoints utilisés par le frontend sont :

| Méthode HTTP | Endpoint                           | Fonction                                  |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `GET`        | `/api/avis`                        | Charger les avis clients publiés          |
| `POST`       | `/api/avis`                        | Envoyer un nouvel avis client             |
| `GET`        | `/api/v1/devis`                    | Récupérer les demandes de devis           |
| `POST`       | `/api/v1/devis`                    | Enregistrer une nouvelle demande de devis |
| `PATCH`      | `/api/v1/devis/{id}/statut`        | Modifier le statut d'une demande de devis |
| `GET`        | `/api/avis/admin`                  | Récupérer les avis pour l'administration  |
| `PATCH`      | `/api/avis/admin/{id}/approbation` | Modifier l'approbation d'un avis          |

Les routes de gestion des administrateurs sont également utilisées par l'interface d'administration sous le préfixe `/api/admin/administrateurs`. Les opérations administratives restent soumises aux règles d'authentification et d'autorisation configurées dans Spring Security.

### Parcours de demande de devis

1. Le visiteur remplit le formulaire de demande de devis sur le site.
2. Le frontend transmet les informations au backend avec `POST /api/v1/devis`.
3. Le backend enregistre la demande dans PostgreSQL sur Neon.
4. Après confirmation de l'enregistrement, le frontend prépare le message contenant les informations de la demande et ouvre WhatsApp avec un lien `https://wa.me/`.
5. La demande enregistrée peut ensuite être consultée dans l'espace d'administration.

L'ouverture de WhatsApp intervient après la réponse positive du backend. Le frontend ouvre d'abord un nouvel onglet au clic de l'utilisateur, puis le redirige vers le lien WhatsApp après l'enregistrement afin de limiter le blocage des fenêtres contextuelles par le navigateur.

### Parcours des avis clients

1. Le visiteur soumet un avis depuis le formulaire public.
2. Le frontend transmet l'avis au backend avec `POST /api/avis`.
3. Le backend traite et enregistre l'avis dans PostgreSQL sur Neon.
4. Les avis sont consultables dans l'administration pour modération.
5. Les avis approuvés sont récupérés par le site public avec `GET /api/avis`.

### Configuration et sécurité en production

* Les URL du frontend pointent vers le backend Render et non vers `localhost`.
* Le backend autorise l'origine du frontend de production dans sa configuration CORS.
* Les informations de connexion à Neon et les autres paramètres sensibles doivent être configurés dans les variables d'environnement du service backend sur Render.
* Les mots de passe, chaînes de connexion et secrets ne doivent pas être ajoutés au dépôt GitHub ni au README.
* Les routes d'administration doivent rester protégées par Spring Security.

### Vérifications réalisées après déploiement

Les vérifications suivantes ont été effectuées sur les services en production :

* Ouverture du site public hébergé sur Render.
* Accès direct à `/admin/dashboard` après configuration de la règle Rewrite.
* Envoi de demandes de devis depuis le formulaire public.
* Vérification de l'enregistrement des demandes par l'API et de leur affichage dans le tableau de bord.
* Vérification de l'ouverture de WhatsApp après l'enregistrement d'une demande.
* Soumission d'avis clients depuis le site.
* Vérification du fonctionnement des échanges entre le frontend, le backend Spring Boot et PostgreSQL sur Neon.
* Utilisation de Beekeeper Studio pour se connecter à Neon et consulter les données.

### Déploiement et mise à jour

Pour publier une nouvelle version du frontend ou du backend :

1. Effectuer et tester les modifications en local.
2. Vérifier les changements avec `git status`.
3. Ajouter les fichiers nécessaires avec `git add .`.
4. Créer un commit avec `git commit -m "description des modifications"`.
5. Envoyer les modifications vers GitHub avec `git push origin master`.
6. Vérifier dans Render que le déploiement correspondant se termine avec le statut `Live`.
7. Tester les fonctionnalités concernées sur les URL de production.

Le déploiement automatique dépend de la configuration du dépôt GitHub et du service Render correspondant.

## Évolutions prévues

* Poursuite de l'amélioration de l'interface d'administration.
* Amélioration continue de l'expérience utilisateur.
* Ajout éventuel de nouvelles fonctionnalités de gestion.
* Renforcement et suivi de la sécurité.
* Optimisation des performances et de la supervision de l'application.

## Auteur

Projet développé par Sialou Tibana Larissa dans le cadre de la réalisation d'une application web de gestion de services de piscine.
