# Vérité & Justice — site de campagne (FR / AR)

Site statique, **un seul fichier** (`index.html`). Aucune dépendance, aucun serveur.
Hébergeable gratuitement (GitHub Pages, Netlify, Cloudflare Pages…).

## Ce qu'il fait
- Récit **à chapitres**, façon documentaire.
- **Bilingue Français / العربية** (bouton FR / ع en haut), passage automatique en **RTL** pour l'arabe.
- **Lecture audio** de chaque chapitre, en FR ou en AR, via la synthèse vocale du navigateur
  (Web Speech API) — donc **sans fichier audio ni serveur**.
- **Documents** affichés en bas des chapitres, avec système de **caviardage**.
- Bandeau **présomption d'innocence** + rôles anonymisés (aucun nom propre).

## ⚠️ Règle d'or pour ne pas se faire attaquer
1. **Aucun nom.** On garde « la notaire », « la mandataire », « l'aînée »… jamais de patronyme.
2. **On ne dit jamais « coupable / assassin »** pour une personne identifiable.
   On écrit « selon le rapport de police… », « il s'agirait de… », et on **pose des questions**.
3. **Caviardage RÉEL des documents.** Le flou/barre noire en CSS est seulement cosmétique :
   l'image d'origine reste téléchargeable. Avant de publier un document, **caviarde les zones
   sensibles DANS LE FICHIER IMAGE** (barre noire en dur, ex. avec un éditeur d'image), puis
   dépose le fichier déjà caviardé dans le dossier `docs/`.

## Ajouter tes documents
1. Caviarde l'image (voir ci-dessus).
2. Place-la dans `docs/` avec l'un de ces noms (déjà attendus par le site) :
   - `docs/police-2021.jpg`          → chapitre 1 (rapport police Neuilly)
   - `docs/classement-2021.jpg`      → chapitre 2 (classement sans suite)
   - `docs/ordonnance-2026.jpg`      → chapitre 4 (ordonnance d'instruction)
   - `docs/acte-notoriete-2026.jpg`  → chapitre 5 (acte « succession vide »)
   - `docs/releve-vente-300k.jpg`    → chapitre 6 (relevé vente ≈ 300 000 €)
   - `docs/rapport-mission-220k.jpg` → chapitre 6 (rapport de mission ≈ 220 000 €)
   - `docs/releve-compte-129k.jpg`   → chapitre 6 (relevé compte ≈ 129 000 €)
   - `docs/gendarmerie-maroc.jpg`    → chapitre 7 (pièce gendarmerie royale / biens au Maroc)
3. Tant qu'aucune image n'est présente, un cadre « Déposez ici le document caviardé » s'affiche.
   Un chapitre peut contenir plusieurs documents (le chapitre 6 en attend trois).

### (Optionnel) flou cosmétique en plus du caviardage réel
Dans `index.html`, cherche `exemple de caviardage cosmétique` et ajoute, dans le `.frame`,
des barres positionnées en pourcentage :
```html
<div class="redact" style="top:20%;left:12%;width:40%;height:6%"></div>
<div class="redact blur" style="top:55%;left:10%;width:55%;height:5%"></div>
```
`.redact` = barre noire ; `.redact.blur` = flou. **Ça ne remplace pas** le caviardage du fichier.

## Modifier le texte / les chapitres
Tout le contenu est dans `index.html`, objet `I18N` (clés `fr` et `ar`).
Chaque chapitre a : `date`, `title`, `html` (affiché) et `speak` (texte lu à voix haute,
sans balises). Pense à modifier **les deux langues** et **les deux champs** (`html` + `speak`).

## Audio : 2 modes (le mode MP3 est déjà prêt)
Le site lit chaque chapitre à voix haute. Deux sources possibles :

**Mode A — Enregistrements MP3 (recommandé, surtout pour l'arabe).**
1. Crée le dossier `docs/audio/`.
2. Dépose tes fichiers, ex. `fr-1.mp3 … fr-8.mp3` et `ar-1.mp3 … ar-8.mp3`
   (ou un seul gros fichier par langue : `fr-full.mp3`, `ar-full.mp3`).
3. Dans `index.html`, renseigne l'objet `AUDIO` :
   ```js
   const AUDIO = {
     fr:{ chapters:["docs/audio/fr-1.mp3","docs/audio/fr-2.mp3", /*…*/ ], full:null },
     ar:{ chapters:["docs/audio/ar-1.mp3","docs/audio/ar-2.mp3", /*…*/ ], full:null }
   };
   ```
   Mets `null` là où tu n'as pas (encore) de fichier. Dès qu'un fichier est renseigné,
   il est joué **à la place** de la synthèse vocale.

**Mode B — Synthèse vocale du navigateur (par défaut, sans fichier).**
Dépend des voix installées sur l'appareil. **L'arabe est souvent absent** → la lecture peut
rester muette. Le site affiche alors un message expliquant comment installer une voix arabe.
Pour une vraie voix humaine et fiable sur tous les téléphones, **utilise le mode A (MP3)**.

> D'où viennent les MP3 ? Tu peux t'enregistrer toi-même, faire enregistrer un proche,
> ou utiliser un service de synthèse en ligne de qualité, puis exporter en MP3.

## Mettre en ligne (GitHub Pages, gratuit)
1. Crée un **nouveau dépôt** GitHub (séparé de l'app Tchipa).
2. Pousse le contenu de ce dossier (`index.html`, `docs/`, `README.md`) à la racine.
3. Settings → Pages → Branch `main` / `/root` → Save.
4. (Option) domaine perso via un fichier `CNAME`.

> Ce dossier est **indépendant** de l'app Tchipa ; il est juste rangé ici pour l'instant.
> Tu peux le déplacer dans son propre dépôt quand tu veux.
