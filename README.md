<div align="center">

# Ummah

**Plateforme communautaire musulmane — Bénévolat · Mosquées · Gamification**

[![Site live](https://img.shields.io/badge/Site%20live-ummah.eu-1C130A?style=for-the-badge&logo=vercel&logoColor=C49A3C)](https://ummah.eu)
[![Statut](https://img.shields.io/badge/Statut-Production-16a34a?style=for-the-badge)](https://ummah.eu)
[![TypeScript](https://img.shields.io/badge/TypeScript-100%25-3178c6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/Propriété%20intellectuelle-Tous%20droits%20réservés-C49A3C?style=for-the-badge)](./LICENSE)

> Ce dépôt est une **présentation portfolio** du projet Ummah.
> Le code source est privé — propriété intellectuelle de l'auteur.

</div>

---

## Le projet

Ummah connecte les **mosquées** avec leurs **bénévoles** via une plateforme web complète, pensée mobile-first et progressive (PWA). L'engagement communautaire est gamifié : chaque bénévole accumule de l'XP, débloque des badges et monte en niveau selon ses compétences.

Trois espaces distincts coexistent sur la même plateforme :

| Espace | Utilisateur | Rôle |
|--------|------------|------|
| **Espace bénévole** | Membres de la communauté | S'inscrire aux événements, suivre ses badges et son XP |
| **Espace admin mosquée** | Responsables d'associations | Créer des événements, gérer les bénévoles, publier des annonces |
| **Espace super-admin** | Équipe Ummah | Modérer le contenu, valider les mosquées, superviser la plateforme |

---

## Fonctionnalités

### Espace bénévole
- **Dashboard personnel** — XP totale, niveau, badges récents, prochains événements
- **Catalogue d'événements** — inscription, liste d'attente automatique, désincription
- **Système de badges** — 10+ compétences (Logistique, Sécurité, Animation…), 5 niveaux (Bronze → Diamant)
- **Progression XP** — barre de progression vers le niveau suivant, historique des gains
- **Chat de groupe** — messagerie par événement entre bénévoles acceptés
- **Notifications in-app** — temps réel + Web Push (PWA)
- **Carte interactive** — annuaire des mosquées via OpenStreetMap
- **Profil** — photo, compétences, historique de participation

### Espace admin mosquée
- **Gestion des événements** — création (bénévole ou annonce communautaire), brouillons, publication
- **Gestion des inscriptions** — accepter / refuser les candidatures, voir les profils et badges
- **Validation post-événement** — marquer les présences, distribuer l'XP, noter (Normal / Difficile / Exceptionnel)
- **Messagerie broadcast** — envoyer un message à tous les bénévoles d'un événement
- **Gestion des bénévoles** — liste, profils, calibration manuelle des niveaux
- **Ma mosquée** — informations publiques, horaires, photos, localisation

### Espace super-admin
- **Validation des mosquées** — vérification des justificatifs, activation des comptes
- **Modération** — gestion des signalements (messages, événements, profils)
- **Gestion des tags** — taxonomie des compétences bénévoles
- **Broadcast global** — notifications système à tous les utilisateurs
- **Tableau de bord** — stats globales en temps réel

---

## Architecture

```
ummah/
├── apps/
│   ├── web/              # Next.js 14 (App Router) + PWA
│   └── api/              # NestJS — API REST
├── packages/
│   ├── shared/           # Types, interfaces, enums, codes d'erreur
│   └── config/           # Configuration partagée
├── prisma/
│   └── schema.prisma     # Schéma DB — source de vérité unique
├── infra/
│   └── ansible/          # Provisioning VPS + gestion des secrets
└── docker/
    ├── api/              # Dockerfile API (multi-stage Alpine)
    ├── web/              # Dockerfile Web (multi-stage Alpine)
    └── nginx/            # Reverse proxy + SSL
```

### Flux de données

```
Client (Browser / PWA)
        │
        ▼
   Nginx (SSL + reverse proxy)
        │
   ┌────┴────────────────────────────┐
   │                                 │
   ▼                                 ▼
Next.js 14                       NestJS API
(App Router + proxy.ts)    (REST /api/v1/*)
        │                            │
        │                    ┌───────┴───────┐
        │                    │               │
        │               PostgreSQL         Redis
        │               (Prisma ORM)   (cache + sessions)
        │
        └──────► Cloudflare R2 (fichiers statiques, signés)
```

---

## Stack technique

### Backend
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Socket.io](https://img.shields.io/badge/Socket.io-010101?style=flat-square&logo=socket.io&logoColor=white)

### Frontend
![Next.js](https://img.shields.io/badge/Next.js%2014-000000?style=flat-square&logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React%2018-61DAFB?style=flat-square&logo=react&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Shadcn/ui](https://img.shields.io/badge/Shadcn%2Fui-000000?style=flat-square&logo=shadcnui&logoColor=white)
![Zod](https://img.shields.io/badge/Zod-3E67B1?style=flat-square&logo=zod&logoColor=white)

### Infrastructure
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![Hetzner](https://img.shields.io/badge/Hetzner%20VPS-D50C2D?style=flat-square&logo=hetzner&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare%20R2-F38020?style=flat-square&logo=cloudflare&logoColor=white)

### Monitoring & Qualité
![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat-square&logo=sentry&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana%20Loki-F46800?style=flat-square&logo=grafana&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?style=flat-square&logo=jest&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)

---

## Sécurité

La sécurité a été traitée comme une contrainte de conception dès le début, pas comme une couche ajoutée après.

- **Auth** — JWT access token (15 min) + refresh token httpOnly cookie (30 jours), rotation à chaque usage, blacklist Redis
- **Account lockout** — 5 tentatives échouées → blocage 15 min (Redis)
- **IDOR** — chaque endpoint vérifie que l'utilisateur est propriétaire de la ressource demandée
- **Mass assignment** — DTOs explicites, le champ `role` n'apparaît jamais dans un DTO public
- **XSS** — sanitisation `sanitize-html` côté backend, `DOMPurify` côté frontend
- **CSRF** — tokens CSRF + cookies httpOnly + CORS strict
- **Uploads** — validation magic bytes (pas seulement l'extension), strip EXIF via `sharp`, noms générés côté serveur, SVG interdit
- **Injection SQL** — Prisma exclusivement, zéro requête brute
- **Rate limiting** — 100 req/min global, 5 req/15 min sur les endpoints d'auth
- **Headers** — Helmet.js avec Content-Security-Policy configurée
- **Secrets** — zéro secret en dur, gestion via Ansible + variables d'environnement

---

## Mobile & PWA

- **Progressive Web App** — installable sur iOS et Android, fonctionne hors-ligne (pages statiques)
- **Safe area inset** — support natif de l'encoche / Dynamic Island (iOS standalone mode)
- **Navigation native** — `MobileTabBar` (pattern app native) + `Drawer` hamburger
- **Inputs ≥ 16px** — empêche le zoom auto iOS Safari au focus
- **Touch targets 44×44** — accessibilité tactile WCAG

---

## CI/CD & Infrastructure

```
Push sur main
     │
     ▼
GitHub Actions
     ├── Build & lint TypeScript
     ├── Tests unitaires (Jest)
     ├── Tests d'intégration (Supertest)
     └── Deploy automatique
           │
           ▼
       Hetzner VPS
       docker compose pull
       docker compose up -d --no-deps
```

- **Déploiement zéro downtime** — rolling update via Docker Compose
- **Secrets** — provisionnés via Ansible Vault, jamais dans le repo
- **Multi-stage builds** — images Alpine légères (builder + runner séparés)
- **Health checks** — sur chaque service Docker
- **Reverse proxy** — Nginx avec SSL Let's Encrypt
- **Mode maintenance** — page statique activable en une commande sans redéploiement

---

## Qualité & Méthodologie

- **Monorepo** — workspace partagé (`packages/shared`) pour les types et codes d'erreur entre API et frontend, zéro duplication
- **Source de vérité unique** — `prisma/schema.prisma` est la référence absolue du modèle de données
- **Conventions strictes** — CLAUDE.md de 500+ lignes définit les règles d'architecture, de sécurité et de nommage
- **Versioning API** — préfixe global `/api/v1/` via NestJS `setGlobalPrefix`
- **Soft delete** — User, Mosquée, Event ne sont jamais supprimés physiquement (RGPD)
- **Tests** — unitaires (Jest), intégration (Supertest), E2E (Playwright), charge (k6)
- **Coverage** — 80% minimum sur la logique métier critique
- **i18n** — français (défaut), arabe (RTL), anglais via `next-intl`
- **Accessibilité** — ARIA, navigation clavier, contraste WCAG AA minimum

---

## Métriques

| Indicateur | Valeur |
|-----------|--------|
| Durée de développement | ~3 mois |
| Modules NestJS | 15+ |
| Pages Next.js | 35+ |
| Endpoints API | 60+ |
| Modèles Prisma | 20+ |
| Migrations DB | 12+ |
| Commits | 100+ |
| Lignes de code | ~15 000 |

---

## Auteur

**Nabil Abboud** — Concepteur & développeur fullstack

> Projet conçu, architecturé et développé intégralement de A à Z.
> Stack moderne, sécurité production-grade, déploiement containerisé.

[![GitHub](https://img.shields.io/badge/GitHub-Nabil--42-181717?style=flat-square&logo=github)](https://github.com/Nabil-42)

---

<div align="center">

**[Visiter le site →](https://ummah.eu)**

*© 2026 Nabil Abboud — Tous droits réservés. Reproduction interdite sans autorisation.*

</div>
