# Actions manuelles — Jour 7

## 1. Secret GitHub UPPTIME_GH_PAT (FAIRE EN PREMIER)

github.com/MBI-NETWORK/legisbox-status
→ Settings → Secrets and variables → Actions → New repository secret

  Nom    : UPPTIME_GH_PAT
  Valeur : [PAT GitHub — créer sur github.com/settings/tokens]
           Scopes requis (fine-grained, repo legisbox-status uniquement) :
           Contents (write), Issues (write), Pull requests (write), Workflows (write)

## 2. Secret SMTP (pour alertes email)

Ajouter dans les mêmes Secrets :
  SMTP_HOST     : [host SMTP du projet — ex: smtp.infomaniak.com]
  SMTP_USERNAME : monitoring@legisbox.fr
  SMTP_PASSWORD : [mot de passe SMTP]

## 3. GitHub Pages

github.com/MBI-NETWORK/legisbox-status
→ Settings → Pages → Source : GitHub Actions

## 4. CNAME DNS (panneau Infomaniak legisbox.fr)

Type    : CNAME
Nom     : status
Valeur  : mbi-network.github.io
TTL     : 3600

## 5. Custom domain GitHub Pages

github.com/MBI-NETWORK/legisbox-status
→ Settings → Pages → Custom domain : status.legisbox.fr
→ Enforce HTTPS : ✅

## 6. Badge status dans le repo LegisBox principal

Ajouter dans MBI-NETWORK/LegisBox README.md :
[![Status](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2FMBI-NETWORK%2Flegisbox-status%2Fmaster%2Fapi%2Fapi-health-general%2Fuptime.json&label=Status)](https://status.legisbox.fr)

## 7. DNS app.legisbox.fr et api.legisbox.fr (même panneau Infomaniak)

Type    : A
Nom     : app
Valeur  : [IP VPS OVH]

Type    : A
Nom     : api
Valeur  : [IP VPS OVH]

## 8. Vérification finale

curl https://status.legisbox.fr → doit afficher la page de status
curl https://api.legisbox.fr/health → 200
curl https://api.legisbox.fr/health/qdrant → 200
curl https://api.legisbox.fr/health/redis → 200
