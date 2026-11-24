# Promesses 2027

Les programmes des candidats à la présidentielle française de 2027 (1er tour le 18 avril 2027), chiffrés mesure par mesure avec une méthode unique, confrontés aux estimations indépendantes publiées et aux obstacles juridiques. Simulateur personnel, quiz à l'aveugle, faisabilité, et un volet « vie quotidienne » (sécurité, santé, école, environnement, logement, libertés, économie, rayonnement).

**Site : [p2027.org](https://p2027.org)**

<!-- totaux:debut (généré par pipeline/run.py, ne pas modifier à la main) -->
Données à jour au 24 novembre 2026 : 8 candidats, 175 mesures.

| Candidat | Parti | Mesures chiffrées | Effet sur le déficit en 2030 (Md€/an) | Fourchette à 80 % |
| --- | --- | --- | --- | --- |
| Marine Le Pen | RN | 29 | −88,3 | −116,0 à −70,2 |
| Jean-Luc Mélenchon | LFI | 29 | −249,3 | −278,6 à −204,5 |
| Édouard Philippe | Horizons | 12 | −1,9 | −26,6 à +3,1 |
| Raphaël Glucksmann | PS-Place publique | 10 | −92,9 | −121,9 à −71,1 |
| David Lisnard | Nouvelle Énergie | 15 | −40,9 | −51,4 à −33,8 |
| Gabriel Attal | Renaissance | 7 | −61,1 | −70,2 à −55,8 |
| Bruno Retailleau | LR | 23 | −21,5 | −29,1 à −9,0 |
| Éric Zemmour | Reconquête | 17 | −116,6 | −133,9 à −87,5 |
<!-- totaux:fin -->

Un montant négatif creuse le déficit. Ces totaux supposent que toutes les mesures passent, y compris celles qui exigent une révision de la Constitution ou des traités. Les mesures non reconfirmées en 2026 et celles dont un paramètre clé n'est pas publié sont hors total.

## Structure

```
public/            le site, tel qu'il est servi (index.html autonome + data/promesses-2027.json)
functions/api/     fonctions Cloudflare Pages : report (signalements), reports (lecture admin)
lib/               code partagé des fonctions
pipeline/          la source de vérité
  base.json        base fusionnée des programmes (avant corrections)
  corrections.py   règles communes, corrections datées, totaux (simulation à 20 000 tirages), résumés
  life.py          volet « vie quotidienne » : fusion, test « précis / intention », lecture commune des études
  build.py         méthode, historique, injection des données dans le gabarit
  template.html    l'app (HTML, CSS, JS sans dépendance)
  data/            fichiers de travail par candidat, vie quotidienne, quiz, repères officiels
  run.py           lance tout et écrit public/
tests/smoke.py     test de bout en bout (Playwright)
```

## Construire

```
python3 pipeline/run.py        # reconstruit public/
python3 tests/smoke.py         # vérifie l'app (Playwright + Chromium)
```

Rien n'est à modifier à la main dans `public/` ni dans le tableau ci-dessus : on modifie `pipeline/`, puis on relance `run.py`. La CI GitHub vérifie que le site versionné correspond aux sources.

Pour faire évoluer le site (où modifier quoi, registre des manques, historique, liste de contrôle) : [DEVELOPPER.md](DEVELOPPER.md).

## Déployer

Voir [DEPLOY.md](DEPLOY.md) (Cloudflare Pages, déploiement automatique à chaque push).

## Méthode

Voir [METHODOLOGIE.md](METHODOLOGIE.md) et l'onglet « Méthode » de l'app.

## Contester un chiffre

Voir [CONTRIBUER.md](CONTRIBUER.md), ou le bouton « Signaler une erreur » sur chaque fiche. Toute correction acceptée est datée dans l'historique de l'app.

## Licences

Code : MIT. Données : CC BY 4.0 (citer « Promesses 2027 »). Les sources citées restent la propriété de leurs auteurs.
