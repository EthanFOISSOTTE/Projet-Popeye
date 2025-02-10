# Projet Docker Popeye

## Description
Ce projet est une application de sondage web basée sur Docker et Docker Compose. Il se compose de plusieurs services conteneurisés qui interagissent ensemble :

- **Poll** : Une application web Flask qui collecte les votes et les envoie à une file d'attente Redis.
- **Redis** : Un serveur Redis utilisé comme file d'attente pour stocker temporairement les votes.
- **Worker** : Une application Java qui récupère les votes de Redis et les enregistre dans une base de données PostgreSQL.
- **PostgreSQL** : Une base de données qui stocke les votes de manière persistante.
- **Result** : Une application web Node.js qui récupère les votes depuis la base de données et les affiche.

## Architecture
```
┌───────────┐      ┌──────────┐      ┌───────────┐      ┌──────────────┐
│   Poll    │ ---> │  Redis   │ ---> │  Worker   │ ---> │  PostgreSQL  │
└───────────┘      └──────────┘      └───────────┘      └──────────────┘
       |                                           │
       |                                           ▼
       └───────────────────────────────────> ┌───────────┐
                                             │  Result   │
                                             └───────────┘
```

## Prérequis
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Installation et Exécution
1. **Cloner le projet**
   ```sh
   git clone https://github.com/votre-utilisateur/votre-repo.git
   cd votre-repo
   ```
2. **Lancer les services avec Docker Compose**
   ```sh
   docker-compose up --build
   ```
3. **Accéder aux différentes interfaces :**
   - Poll : [http://localhost:5000](http://localhost:5000)
   - Result : [http://localhost:5001](http://localhost:5001)
   
## Structure du projet
```
.
├── compose.yml
├── schema.sql
├── poll/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── ...
├── worker/
│   ├── Dockerfile
│   ├── pom.xml
│   ├── src/
│   └── ...
├── result/
│   ├── server.js
│   ├── Dockerfile
│   ├── package.json
│   └── ...
├── .env
└── README.md
```

## Commandes utiles
- **Arrêter les conteneurs** :
  ```sh
  docker-compose down
  ```
- **Recompiler et relancer** :
  ```sh
  docker-compose up --build
  ```
- **Afficher les logs** :
  ```sh
  docker-compose logs -f
  ```
- **Accéder à un conteneur en ligne de commande** :
  ```sh
  docker exec -it <nom_du_conteneur> sh
  ```

## Déploiement
Pour déployer sur un serveur, vous pouvez utiliser Docker Compose sur la machine cible ou héberger les images sur un registre comme Docker Hub.

## Licence
Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus d’informations.

## Auteur
[FOISSOTTE Ethan] - Projet réalisé dans le cadre d'un exercice DevOps.
