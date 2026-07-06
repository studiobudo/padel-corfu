# Vols directs vers Corfou 2026 — vols.kerkyra.fr

Site autonome (fichier unique `index.html`) : guide + outil de recherche des vols
directs vers Corfou (CFU) pour la saison 2026, au départ de France, Belgique,
Luxembourg et Suisse.

## Fonctionnalités
- 3 langues (FR / EN / ΕΛ), FR par défaut.
- Outil de recherche par ville et par jour + carte cliquable.
- **Pop-up email (gate)** : à la validation, ouvre un e-mail pré-rempli vers
  `michael@boudot.me` (inscription du visiteur).
- **Formulaire devis** : nom, e-mail, période, nb de personnes, projet →
  e-mail pré-rempli vers `michael@boudot.me`.

Les deux formulaires utilisent `mailto:` : le message s'ouvre dans la messagerie
du visiteur, à destination de `michael@boudot.me`.

## Déploiement (Vercel)
Projet Vercel **distinct** de celui du site Padel Academy (même dépôt GitHub) :
- **Root Directory** : `vols-corfou`
- Aucun build (site statique). Vercel sert `index.html`.
- Domaine : `vols.kerkyra.fr` (DNS géré chez Gandi — voir instructions de mise
  en ligne).

## Données
Compagnies, fréquences et fins de saison : fiables. Jours, horaires et prix :
**indicatifs** (saison 2026), à confirmer sur les moteurs des compagnies.
Données modifiables dans les tableaux JS `FLIGHTS` / `MAP` et le dictionnaire `T`.
