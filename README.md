# Portfolio — François Toyi

Site en HTML/CSS pur (aucune dépendance à installer), prêt à déployer sur GitHub Pages.

## 1. Tester en local

Ouvrez simplement `index.html` dans votre navigateur. Aucune installation,
aucun serveur requis.

## 2. Déployer sur GitHub Pages

1. Créez un dépôt GitHub, par exemple `portfolio`.
2. Mettez `index.html`, `style.css` et le dossier `assets/` (photo + CV) à la racine du dépôt.
3. Dans le dépôt : **Settings → Pages**.
4. Sous **Build and deployment**, choisissez **Deploy from a branch**, branche `main`, dossier `/ (root)`.
5. Enregistrez. Le site est disponible après une minute ou deux à l'adresse :
   `https://frannoi12.github.io/portfolio/`

## Contenu du site

- **Accueil** — nom, titre, photo, accès rapide au contact + téléchargement du CV
- **Profil** — résumé professionnel
- **Expérience** — Digital Hub Togo (2025–2026) + ONG ESPOIR PLUS (2023–2025)
- **Projets principaux** — BANDJELI, EPHAB Togo, gestion de collecte des déchets,
  app mobile de contacts (GraphQL/React Native), app mobile de plannings (Flutter)
- **Projets académiques** — gestion de pharmacie, gestion d'école, gestion de tâches,
  automatisation électronique
- **Compétences techniques** — backend, front/mobile, bases de données, DevOps, conception
- **Formation** — Licence IFNTI, FACEG, Baccalauréat
- **Contact** — email, téléphone, GitHub, LinkedIn, téléchargement du CV

## Fichiers importants

| Fichier | Rôle |
| --- | --- |
| `index.html` | Tout le contenu du site (textes, sections, liens) |
| `style.css` | Couleurs, typographie, mise en page, thème clair/sombre |
| `assets/photo.jpg` | Photo de profil affichée dans le rond en haut de page |
| `assets/CV-Francois-Toyi.pdf` | CV téléchargeable depuis deux endroits de la page |
| `assets/favicon.ico`, `favicon-*.png` | Icône de l'onglet du navigateur (tirée de `photo.jpg`) |

### Changer la photo

Placez la nouvelle image dans `assets/` **sous le nom exact `photo.jpg`**
(format JPEG). Si votre fichier est dans un autre format, changez l'extension
dans `index.html`, ligne `<img src="assets/photo.jpg" ...>`. Si l'image est
absente ou illisible, un fallback avec vos initiales s'affiche à la place.

Puis régénérez l'icône d'onglet avec ImageMagick :

```bash
cd assets
convert -resize 512x512^ -gravity north -extent 512x512 photo.jpg favicon-256.png
convert -resize 32x32 favicon-256.png favicon-32.png
convert -resize 16x16 favicon-256.png favicon-16.png
convert -resize 180x180 favicon-256.png favicon-180.png
convert favicon-256.png favicon.ico
```

Le recadrage `-gravity north` reprend exactement ce que fait l'avatar du site
(`.avatar img { object-position: center top }`), donc l'icône et la photo
montrent la même partie de l'image. Si l'icône te paraît mal cadrée, joue sur
`-gravity center` ou remplace `north` par `northwest`.

### Mettre à jour le CV

Remplacez `assets/CV-Francois-Toyi.pdf` par une nouvelle version **en gardant
exactement le même nom de fichier**, sinon les deux liens de téléchargement
(hero et section Contact) cassent.

## Modifications courantes

- **Modifier un texte** : ouvrez `index.html`, cherchez le passage à changer.
- **Changer les couleurs, polices ou la mise en page** : éditez `style.css`.
  Les couleurs sont des variables CSS en haut de fichier (`--accent`,
  `--bg`, `--ink`…) et existent en deux jeux : thème clair et thème sombre.
- **Ajouter une section** : copiez un bloc `<section>` existant dans `index.html`,
  ajoutez le lien correspondant dans la `<nav>` du header et donnez-lui un
  `id` unique. Pour un décalage d'animation, ajoutez une règle
  `.section:nth-of-type(n)` en fin de `style.css`.

## Modes et animations

Le bouton en haut à droite (icône soleil/lune) bascule entre les deux thèmes.
Le choix du visiteur est mémorisé dans `localStorage` ; par défaut, le site suit
la préférence système de l'appareil.

Les sections apparaissent en fondu au chargement et les cartes de projets se
soulèvent au survol. Ces animations sont désactivées automatiquement si le
visiteur a réduit les animations dans les réglages de son système, et le
contenu reste lisible même si le JavaScript est bloqué.
