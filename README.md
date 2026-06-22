<div align="center">

# Ummah

**Plateforme communautaire — Bénévolat · Associations · Gamification**

<br/>

### [→ Accéder au site](https://ummah-app.duckdns.org/)

<br/>

[![Site live](https://img.shields.io/badge/Site%20live-ummah--app.duckdns.org-1C130A?style=for-the-badge&logoColor=C49A3C)](https://ummah-app.duckdns.org/)
[![Statut](https://img.shields.io/badge/Statut-Production-16a34a?style=for-the-badge)](https://ummah-app.duckdns.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-100%25-3178c6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/Propriété%20intellectuelle-Tous%20droits%20réservés-C49A3C?style=for-the-badge)](./LICENSE)

<br/>

> Ce dépôt est une **présentation portfolio** du projet Ummah.
> Le code source est privé — propriété intellectuelle de l'auteur.

</div>

---

## Le projet

Ummah connecte les **associations** avec leurs **bénévoles** via une plateforme web complète, pensée mobile-first et progressive (PWA). L'engagement communautaire est gamifié : chaque bénévole accumule de l'XP, débloque des badges et monte en niveau selon ses compétences.

Trois espaces distincts coexistent sur la même plateforme :

| Espace | Utilisateur | Rôle |
|--------|------------|------|
| **Espace bénévole** | Membres de la communauté | S'inscrire aux événements, suivre ses badges et son XP |
| **Espace admin association** | Responsables d'associations | Créer des événements, gérer les bénévoles, publier des annonces |
| **Espace super-admin** | Équipe Ummah | Modérer le contenu, valider les associations, superviser la plateforme |

---

## Fonctionnalités

### Espace bénévole
- **Dashboard personnel** — XP totale, niveau, badges récents, prochains événements
- **Catalogue d'événements** — inscription, liste d'attente automatique, désincription
- **Système de badges** — 10+ compétences (Logistique, Sécurité, Animation…), 5 niveaux (Bronze → Diamant)
- **Progression XP** — barre de progression vers le niveau suivant, historique des gains
- **Chat de groupe** — messagerie par événement entre bénévoles acceptés
- **Notifications in-app** — temps réel + Web Push (PWA)
- **Carte interactive** — annuaire des associations via OpenStreetMap
- **Profil** — informations, historique de participation, badges obtenus
- **Dons en ligne** — contribution aux associations via paiement sécurisé Stripe

### Espace admin association
- **Gestion des événements** — création (bénévole ou annonce communautaire), brouillons, publication
- **Gestion des inscriptions** — accepter / refuser les candidatures, voir les profils et badges
- **Validation post-événement** — marquer les présences, distribuer l'XP, noter (Normal / Difficile / Exceptionnel)
- **Messagerie broadcast** — envoyer un message à tous les bénévoles d'un événement
- **Gestion des bénévoles** — liste, profils, calibration manuelle des niveaux
- **Ma structure** — informations publiques, horaires, photos, localisation

### Espace super-admin
- **Validation des associations** — vérification des justificatifs, activation des comptes
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
│   ├── terraform/        # Infrastructure as Code (provisioning VPS)
│   └── ansible/          # Configuration serveur + gestion des secrets
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
        └──────► Cloudflare R2 (fichiers, URLs signées)
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

### Paiement & Emails
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white)
![Brevo](https://img.shields.io/badge/Brevo-0B996E?style=flat-square&logo=sendinblue&logoColor=white)

### Infrastructure & DevOps
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)
![OVH](https://img.shields.io/badge/OVH%20VPS-123F6D?style=flat-square&logo=ovh&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare%20R2-F38020?style=flat-square&logo=cloudflare&logoColor=white)

### Monitoring & Qualité
![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat-square&logo=sentry&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana%20Loki-F46800?style=flat-square&logo=grafana&logoColor=white)
![Uptime Kuma](https://img.shields.io/badge/Uptime%20Kuma-5CDD8B?style=flat-square&logo=uptimekuma&logoColor=black)
![Telegram](https://img.shields.io/badge/Telegram%20Bot-2CA5E0?style=flat-square&logo=telegram&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?style=flat-square&logo=jest&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)

---

## Paiement & Emails transactionnels

### Stripe — Dons en ligne
- Intégration Stripe complète pour la collecte de dons
- Paiement sécurisé, gestion des webhooks Stripe côté API
- Campagnes de dons activables par association (feature flag)
- Confirmation de paiement et reçu automatique

### Brevo — Emails automatiques
Tous les emails transactionnels sont gérés via l'SMTP Brevo :

| Déclencheur | Email envoyé |
|------------|-------------|
| Inscription | Email de bienvenue |
| Mot de passe oublié | Lien de réinitialisation (token SHA256, 1h) |
| Inscription acceptée | Notification bénévole |
| Événement annulé | Notification à tous les inscrits |
| Validation association | Notification activation compte |

---

## Infrastructure as Code

### Terraform — Provisioning
L'ensemble de l'infrastructure est décrit en code via Terraform :
- Provisioning du VPS OVH
- Configuration réseau et firewall
- Gestion des DNS
- Reproductibilité totale de l'environnement en une commande

### Ansible — Configuration serveur
- Installation et configuration de l'environnement Docker
- Déploiement des secrets (variables d'environnement chiffrées via Ansible Vault)
- Aucun secret en clair dans le repository

---

## CI/CD & Déploiement

```
Push sur main
     │
     ▼
GitHub Actions
     ├── Build & lint TypeScript
     ├── Tests unitaires (Jest)
     ├── Tests d'intégration (Supertest)
     └── Deploy automatique sur OVH VPS
           │
           ▼
       docker compose pull
       docker compose up -d --no-deps
       (rolling update — zéro downtime)
```

- **Déploiement continu** — chaque push sur `main` déclenche un déploiement automatique
- **Zéro downtime** — rolling update via Docker Compose
- **Multi-stage builds** — images Alpine légères (builder + runner séparés)
- **Health checks Docker** — sur chaque service, redémarrage automatique en cas de crash
- **Mode maintenance** — page statique activable en une commande sans redéploiement

---

## Monitoring & Alerting

### Health checks automatisés (Crontab)
Des scripts de vérification tournent en crontab sur le serveur et contrôlent en permanence :
- Disponibilité de l'API (`/health`)
- Disponibilité du frontend
- État des conteneurs Docker
- Espace disque et mémoire

### Bot Telegram — Alertes temps réel
Un bot Telegram envoie une alerte instantanée en cas de problème détecté :
- Notification immédiate si un service tombe
- Rapport de redémarrage automatique
- Alertes seuils (disque, mémoire)

### Uptime Kuma
- Dashboard de monitoring en temps réel
- Historique de disponibilité
- Alertes multi-canal

### Sentry + Grafana Loki
- Tracking des erreurs frontend et backend en production
- Agrégation et recherche des logs applicatifs

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
- **Secrets** — zéro secret en dur, gestion via Ansible Vault + variables d'environnement
- **Reset mot de passe** — token SHA256 stocké hashé, usage unique, expiration 1h, révocation de toutes les sessions

---

## Mobile & PWA

- **Progressive Web App** — installable sur iOS et Android, fonctionne hors-ligne (pages statiques)
- **Safe area inset** — support natif de l'encoche / Dynamic Island (iOS standalone mode)
- **Navigation native** — barre d'onglets bas d'écran (pattern app native) + drawer hamburger
- **Inputs ≥ 16px** — empêche le zoom auto iOS Safari au focus
- **Touch targets 44×44** — accessibilité tactile WCAG

---

## Qualité & Méthodologie

- **Monorepo** — workspace partagé (`packages/shared`) pour les types et codes d'erreur entre API et frontend, zéro duplication
- **Source de vérité unique** — `prisma/schema.prisma` est la référence absolue du modèle de données
- **Conventions strictes** — documentation interne de 500+ lignes définissant les règles d'architecture, de sécurité et de nommage
- **Versioning API** — préfixe global `/api/v1/` via NestJS `setGlobalPrefix`
- **Soft delete** — User, Association, Événement ne sont jamais supprimés physiquement (RGPD)
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
> Stack moderne, sécurité production-grade, infrastructure as code, déploiement containerisé.

[![GitHub](https://img.shields.io/badge/GitHub-Nabil--42-181717?style=flat-square&logo=github)](https://github.com/Nabil-42)

---

<div align="center">

### [→ Visiter le site](https://ummah-app.duckdns.org/)

*© 2026 Nabil Abboud — Tous droits réservés. Reproduction interdite sans autorisation.*

</div>
