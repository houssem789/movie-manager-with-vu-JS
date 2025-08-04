# vue-project

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
pnpm install
```

### Compile and Hot-Reload for Development

```sh
pnpm dev
```

### Compile and Minify for Production

```sh
pnpm build
```

# 🎬 Gestionnaire de Films – Vue 3 + Docker

Une petite application Vue.js pour gérer une liste de films, avec un compteur, tri automatique, et une section bonus "Film de la semaine".

## 🚀 Démarrage rapide (avec Docker)

### 1. Prérequis

- [Docker](https://www.docker.com/) installé
- [Docker Compose](https://docs.docker.com/compose/) (inclus avec Docker Desktop)

### 2. Lancer le projet

Dans la racine du projet (là où se trouve `docker-compose.yml`) :

```bash
docker-compose up --build


.
├── docker-compose.yml
├── frontend/
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── .gitignore
│   ├── package.json
│   ├── src/
│   └── public/
└── README.md

cd frontend
npm install
npm run dev

npm run build


