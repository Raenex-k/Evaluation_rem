# Méthode examen BC01 – Front-end sans framework

> Fichier de préparation à donner à Claude au début de la conversation d'examen, avec le sujet.
> Il est valable quel que soit le sujet. Ordre de priorité : **1. le sujet** → **2. les règles « Toujours »** → **3. les choix « Par défaut »**.

---

## 0. Instructions pour Claude (à lire en premier)

1. Lis ce fichier en entier, puis le sujet.
2. **Le sujet passe avant tout.** Relève tout ce qu'il impose (section 2). Ce qu'il impose remplace les choix « Par défaut » (section 6).
3. Les règles « Toujours » (section 4) et les leçons du feedback (section 5) s'appliquent quel que soit le sujet, sauf si le sujet dit explicitement le contraire.
4. Relie chaque demande du sujet à un critère de la grille (section 3).
5. Propose en moins de 10 minutes : la liste des fonctionnalités, l'arborescence (celle du sujet si elle est donnée), le nom du projet (celui du sujet). Attends la validation de Rayane.
6. Demande à Rayane de connecter **tout le dossier du projet** dès le début (pas un sous-dossier), pour lire, modifier et tester les fichiers directement.
7. Produis ensuite le code **par blocs** : un bloc = une fonctionnalité complète qu'on peut tester à l'écran (pas fichier par fichier). Teste, puis explique chaque bloc en 1 ou 2 phrases pour que Rayane puisse le défendre.
8. Applique la checklist finale (section 10) avant le rendu.
9. Ton : franc, concis, en français, sans flatterie. Signale clairement un conflit entre deux règles au lieu de trancher en silence.
10. **Quand Rayane pose une question, réponds-y sans modifier de fichier.** N'agis que s'il le demande explicitement.

---

## 1. Contexte de l'épreuve

- **BC01** : concevoir et réaliser des interfaces utilisateur adaptatives et interactives front-end.
- Épreuve **individuelle**, **4 heures**, sur ordinateur, **sans framework ni bibliothèque externe** (HTML5, CSS3, JavaScript ES6+ natif).
- **Livrable** : le code produit, plus ce que le sujet demande (souvent README, parfois captures d'écran).
- **IA autorisée** par le prof.

---

## 2. Priorité 1 : ce qu'il faut relever dans le sujet

Quand le sujet précise un de ces points, **il gagne toujours** sur le reste de ce fichier.

- [ ] **Nom** du projet et de l'entreprise (jamais une vraie marque).
- [ ] **Arborescence** et noms de fichiers imposés (ex. `style.css`, `utils.js`, `assets/images/`).
- [ ] **Pages et URL** (ex. `index.html`, `user.html?id={id}`).
- [ ] **API** : base URL, endpoints, méthodes (GET, **POST**…), format des données.
- [ ] **Liste exacte des fonctionnalités**, page par page.
- [ ] **Animations et effets demandés** (loader, survol, menu, scroll…).
- [ ] **Contenu du menu** (liens obligatoires, page active, burger, animation).
- [ ] **Formulaires** et règles de validation.
- [ ] **Points de rupture** (ex. < 768, 768–1024, > 1024 px).
- [ ] **Navigateurs cibles** (ex. Chrome, Firefox, Safari, Edge).
- [ ] **Conventions de nommage** (ex. camelCase en JS, kebab-case en CSS).
- [ ] **Choix à justifier** (ex. « mobile first ou desktop first, à justifier »).
- [ ] **Livrables** (code, README, captures d'écran, démo…).
- [ ] **Critères d'évaluation** propres au sujet.

---

## 3. Grille d'évaluation (11 critères × 5 points = 55)

Niveaux : 0 (non traité), 2 (insuffisant), 3 (suffisant, améliorable), **5 (professionnel)**.

| Critère | Ce qu'il faut pour 5/5 |
|---|---|
| **Cr1.1 W3C** | 0 erreur au validateur (validator.w3.org) sur **toutes** les pages. Aucun fichier en 404 (favicon, images). |
| **Cr1.2 Accessibilité** | Sémantique correcte, `alt` partout, ARIA juste, focus visible, tout faisable au clavier, 0 alerte axe / Lighthouse ≥ 95. Pas de lien vers une section cachée. |
| **Cr1.3 Clarté du code** | Indentation cohérente, commentaires sur les parties complexes, pas de duplication, **une seule langue pour les noms**, conventions de nommage respectées, une responsabilité par fichier. |
| **Cr2.1 Cohérence du design** | Variables CSS, mêmes header / nav / footer / favicon sur **toutes** les pages, boutons secondaires bien contrastés, **une seule police**. |
| **Cr2.2 Expérience utilisateur** | Navigation identique partout, page active indiquée, règle des 3 clics, retour à l'accueil toujours possible, messages clairs (chargement, aucun résultat, erreur qui disparaît quand ça remarche). |
| **Cr3.1 Responsive** | Media queries, Flexbox/Grid, rien ne déborde, testé en 375 / 768 / 1024 / 1440 px, menu burger en mobile, approche mobile first ou desktop first **justifiée**. |
| **Cr4.1 Fonctionnalités** | **Toutes** les fonctionnalités du sujet, **y compris les animations** et la **validation des formulaires**. |
| **Cr4.2 Compatibilité** | API standard uniquement, toute promesse gérée (`.catch()` ou `try/catch`), testé sur les navigateurs du sujet. |
| **Cr4.3 ECMAScript** | Modules ES, `async/await`, `const/let`, fonctions fléchées, template literals, spread, déstructuration si utile. |
| **Cr5.1 AJAX** | `fetch` sans rechargement de page (GET et POST si demandé), `response.ok` vérifié, `try/catch`, affichage mis à jour après l'envoi. |
| **Cr5.2 Performance** | Debounce sur la saisie, **pas de double requête**, annulation des **recherches** périmées, requêtes en parallèle (`Promise.all`) plutôt qu'en série, pas de requête inutile (filtrer en local si les données sont déjà chargées). |

---

## 4. Toujours (quel que soit le sujet)

### HTML et sémantique
- La balise dit ce que la chose **est**, la classe dit à quoi elle **ressemble**.
- `header`, `nav`, `main`, `section`, `article`, `footer` utilisés à bon escient. **Un seul** `<h1>` par page, aucun niveau de titre sauté.
- `<section>` uniquement si elle a un titre (sinon `<div>`). `<article>` pour un élément autonome (une carte).
- Listes de résultats en `<ul>/<li>` (ou `<ol>` si l'ordre compte).
- `<button>` = agit dans la page. `<a href>` = emmène ailleurs. **Jamais de div cliquable.**
- Toute saisie dans un `<form>` avec un `<label for="...">` lié à l'input, et des **attributs de validation HTML5** (`required`, `type="email"`, `minlength`, `maxlength`, `pattern`…).
- Test : désactiver le CSS, la page doit rester lisible de haut en bas.

### Accessibilité
- Pas d'ARIA vaut mieux que du mauvais ARIA. Un vrai `<button>` plutôt qu'un `role="button"`.
- `aria-pressed` : bouton à deux états, mis à jour à chaque clic.
- `aria-expanded` : bouton qui ouvre ou ferme (burger), mis à jour à chaque clic, **Échap referme**.
- `aria-label` : seulement si aucun texte visible (bouton icône).
- `aria-live="polite"` : zone de message (chargement, nombre de résultats, erreur, confirmation d'ajout).
- `aria-current="page"` : lien de la page active dans le menu.
- `alt` sur chaque image, `alt=""` si décorative ou si le texte voisin dit déjà la même chose.
- Classe `sr-only` pour un texte lu mais invisible. Lien d'évitement « Aller au contenu ».
- Les 3 fautes graves : `outline: none` sans remplacement, une div cliquable, un état montré par la couleur seule.
- `prefers-reduced-motion` respecté pour toutes les animations.

### CSS
- **Variables CSS** nommées par **rôle** (`--bg`, `--text`, `--accent`), jamais par couleur. Espacements et rayons aussi en variables.
- **Flexbox et/ou Grid** pour la mise en page, **media queries** pour le responsive.
- **Mobile first ou desktop first, au choix, mais justifié** (dans le README).
- **Animations et transitions** : survol des éléments cliquables, apparition des contenus, menu animé, loader. C'est attendu dans tous les sujets.
- **Design cohérent** entre toutes les pages : mêmes couleurs, mêmes composants, **une seule police** (`system-ui` par défaut, aucune ressource externe).

### JavaScript
- **ES6+** : `const`/`let`, fonctions fléchées, template literals, modules (`type="module"`).
- Données de l'API insérées avec `createElement` + `textContent`. **Jamais `innerHTML`** pour des données (pour vider un élément : `replaceChildren()`).
- **Gestion des événements** avec `addEventListener`, **délégation** (un seul écouteur sur une liste, `event.target.closest(...)`).
- `dataset` renvoie toujours une **chaîne** : convertir avec `Number()` avant de comparer à un nombre.
- `fetch` + `async/await` + `try/catch`, `if (!response.ok) throw new Error(...)`.
- `encodeURIComponent()` pour tout texte saisi mis dans une URL.
- **Zéro résultat n'est pas une erreur**, c'est un état à afficher (« Aucun résultat »).
- **Trois états affichés** : chargement (loader + message), aucun résultat, erreur. Retirer l'état d'erreur au début de chaque nouvelle requête.
- **Validation côté client** des formulaires (HTML5 + vérifications JS), messages d'erreur clairs.
- Tri ou modification sur une **copie** du tableau : `[...items].sort(...)`.
- Toute promesse a son `.catch()` ou son `try/catch` (ex. `media.play()`).
- `localStorage` (si utilisé) : `JSON.stringify` à l'écriture, `JSON.parse` dans un `try/catch` avec repli à la lecture.
- **Performance** : debounce sur la saisie, pas de double requête, annulation des recherches périmées, `Promise.all` pour les requêtes indépendantes.
- **Aucune bibliothèque ni framework externe.**

### Qualité du code
- Indentation cohérente, pas de duplication (une fonction réutilisée plutôt que du code copié).
- Commentaires courts sur les parties complexes.
- **Une seule langue pour les noms : anglais.** camelCase en JS, kebab-case en CSS (sauf convention différente du sujet).
- Une responsabilité par fichier, pas de variable globale.

### Navigation et expérience utilisateur
- Header, nav, footer et favicon **identiques** sur toutes les pages.
- Page active indiquée dans le menu (`aria-current` + style visible, pas seulement une couleur).
- Règle des 3 clics, retour à l'accueil toujours possible (logo cliquable + lien), bouton retour quand on est sur une page de détail.
- Aucun lien vers une section cachée ou vide.

### Serveur, outils et tests
- Jamais en `file://` : Live Server (VS Code) ou `py -m http.server 8000`, adresse en `http://`.
- F12 : Console (erreurs), Elements (DOM réel), Network (requêtes, statut 200/404), Lighthouse (accessibilité).
- Tests avant rendu : validateur W3C sur chaque page, Lighthouse / axe, 375 / 768 / 1024 / 1440 px, parcours complet au clavier, navigateurs du sujet.

### Livrables
- **README** : lancement, fonctionnalités, architecture, choix techniques **justifiés** (dont mobile/desktop first), tests réalisés, **utilisation de l'IA**.
- Captures d'écran si le sujet les demande (mobile + desktop, chaque page).

---

## 5. Feedback de l'entraînement E1 (≈ 15/20) – à ne plus refaire

Réussi : architecture découpée, accessibilité (0 alerte), 0 erreur W3C, debounce, `response.ok`, `try/catch`, requêtes groupées, tri sur copie.

| Erreur E1 | Correction à appliquer d'office |
|---|---|
| **Aucune animation** (attendu du sujet) | Transitions sur cartes et boutons, apparition des résultats en `@keyframes`, menu animé, `prefers-reduced-motion`. |
| Site nommé d'après une vraie marque, avec son logo | **Nom et dossier = ceux du sujet.** Aucune marque réelle, aucun logo de marque. |
| Noms mélangés français / anglais | **Tout en anglais** dans le code. |
| Boutons secondaires sombres sur fond sombre | Fond plus clair ou bordure visible, contraste vérifié. |
| 3 polices importées pour une seule utilisée | Une seule famille, seulement les graisses utilisées. |
| Nav différente entre les pages | Header / nav / footer **identiques** partout. |
| `favicon.ico` en 404 sur une page | Même favicon, même chemin sur toutes les pages. |
| `alt="Logo"` à côté du nom du site écrit en texte | `alt=""`. |
| Lien de nav vers une section cachée | Pas de lien vers une section `hidden`. |
| Message d'erreur resté rouge | Retirer la classe d'erreur au début de chaque requête. |
| « 0 résultats trouvés » affiché tel quel | Message dédié : « Aucun résultat ». |
| Une carte par ligne en mobile | 2 colonnes en mobile (`minmax(150px, 1fr)`). |
| Entrée = 2 requêtes | Annuler le debounce au `submit`. |
| Réponse lente qui écrase une récente | Annulation de la recherche précédente (`AbortController`). |
| Pas de README | README avec documentation technique **et** déclaration de l'IA. |

---

## 6. Par défaut (seulement si le sujet ne précise rien)

Ce sont les habitudes du cours. **Si le sujet impose autre chose, on suit le sujet.**

### Architecture par défaut
```
nom-du-projet/
├── index.html
├── README.md
├── css/  reset.css  tokens.css  layout.css  components.css  responsive.css
└── js/   main.js  api.js  render.js  format.js  (+ un fichier par responsabilité)
```
1. **Un seul script** par page : `<script type="module" src="js/main.js"></script>` (une page avec sa propre logique peut avoir son propre point d'entrée, ex. `js/user.js`).
2. `api.js` ne touche **jamais** au DOM : il reçoit un paramètre, il renvoie des données.
3. `render.js` ne fait **jamais** de `fetch` : il reçoit un objet, il renvoie un élément sans l'insérer.
4. **Aucune variable globale** : l'état de la page vit dans un seul objet `state` dans son point d'entrée.
5. Un fichier de plus de **150 lignes** est à couper.

- `layout.css` = où sont placés les gros blocs. `components.css` = à quoi ressemble chaque élément réutilisable.
- Si le sujet impose une autre structure (ex. `style.css` + `responsive.css`, `utils.js`), on garde les mêmes principes **à l'intérieur** des fichiers imposés.

### Valeurs par défaut
- Points de rupture : 768 px (tablette) et 1024 px (desktop).
- Grille de cartes : `minmax(150px, 1fr)` en mobile, `minmax(250px, 1fr)` à partir de 768 px.
- Noms de fonctions du cours (`createCard`, `search`, `debounce`, `debouncedSearch`) : à réutiliser seulement si le sujet ou le prof les reprend.

---

## 7. Façon de travailler de Rayane

- Code **simple mais propre** : pas de syntaxe tordue, mais bien nommé, bien découpé. Le niveau « professionnel » de la grille passe par la clarté, pas par la complexité.
- **HTML léger : pas de classes ni d'id partout.** Une classe ou un id seulement si le CSS ou le JS en a vraiment besoin. Sinon, cibler par la balise (`header nav a`, `main section`, `form input`).
- **Noms de classes et d'id simples, pas trop « pro »** : courts et parlants (`card`, `menu`, `list`, `message`), jamais de noms à rallonge ou de style BEM (`results-section__item--active`).
- Pas de `div` d'emballage inutile : seulement quand la mise en page l'exige.
- Petits commentaires en français, naturels, seulement là où ils aident.
- Garder **exactement** les noms imposés par le sujet.
- Expliquer chaque bloc produit en 1 ou 2 phrases.
- Renommer une fonction ou un fichier : faire Ctrl+F pour corriger **tous** les appels et imports, dans tous les fichiers.
- Rayane veut comprendre : répondre clairement à ses questions de compréhension.
- Une question n'est pas un ordre : répondre sans modifier les fichiers.

---

## 8. Méthode le jour J (4 heures)

| Temps | Étape |
|---|---|
| 0:00 – 0:15 | Lire le sujet, remplir la liste de la section 2, relier à la grille. Claude propose fonctionnalités + arborescence + nom. Validation. |
| 0:15 – 0:30 | Créer le dossier (nom du sujet, minuscules, tirets, hors OneDrive), le connecter, lancer Live Server. Poser la structure HTML commune, les variables CSS, le layout. |
| 0:30 – 2:15 | Fonctionnalités par blocs, page par page. **Tester dans le navigateur après chaque bloc** (console ouverte). |
| 2:15 – 3:00 | CSS : composants, **animations**, loader, responsive. |
| **≈ 3:00** | **Déposer une première version de secours.** |
| 3:00 – 3:30 | Tests : W3C sur chaque page, Lighthouse / axe, 375 / 768 / 1024 / 1440 px, parcours au clavier, navigateurs du sujet. |
| 3:30 – 3:50 | README (+ captures d'écran si demandées). |
| 3:50 – 4:00 | Checklist finale, zip, rendu. |

Règle d'or : ne jamais écrire plus de 10 lignes sans tester.

---

## 9. Pièges déjà rencontrés (et diagnostic rapide)

| Symptôme | Cause probable |
|---|---|
| `Cannot GET /js/xxx.js` | Faute dans le nom du fichier (vécu : `palyer.js`) ou mauvais dossier. |
| `Cannot read properties of null` | Le sélecteur JS ne correspond plus au HTML (id ou classe changé d'un côté seulement). |
| Tout le JS est mort | Un seul import cassé ou une erreur de syntaxe (vécu : `}é`) bloque tout le module. |
| `xxx is not defined` | Fonction renommée ou supprimée mais encore appelée. |
| Espacements à 0 alors que les couleurs marchent | Variable CSS inexistante ou mal écrite. |
| Le CSS modifié ne change rien | Cache (Ctrl+Maj+R) ou Live Server lancé sur un autre dossier. |
| Message d'erreur générique dans le `catch` | Le `catch` attrape **toute** erreur : ajouter `console.error(error)` pour voir la vraie. |
| Une seule requête aboutit sur plusieurs | Un `AbortController` partagé annule les autres : l'annulation est réservée à la recherche. |

---

## 10. Checklist finale avant rendu

- [ ] Tout ce qui est relevé en section 2 est respecté (nom, arborescence, pages, API, fonctionnalités, livrables).
- [ ] Animations : survol des éléments cliquables, apparition des contenus, menu, loader, `prefers-reduced-motion`.
- [ ] Header / nav / footer / favicon identiques sur toutes les pages, page active indiquée, aucun 404 (onglet Network).
- [ ] 0 erreur W3C sur chaque page.
- [ ] Lighthouse accessibilité ≥ 95, parcours complet au clavier, focus visible.
- [ ] Un seul `h1` par page, pas de niveau sauté.
- [ ] Formulaires : labels, validation HTML5 + JS, messages d'erreur, affichage mis à jour après l'envoi.
- [ ] Aucun `innerHTML` avec des données. Aucune variable globale. Aucune bibliothèque externe.
- [ ] Noms de code tous en anglais, conventions de nommage respectées.
- [ ] HTML léger : classes et id seulement là où le CSS ou le JS en a besoin, noms courts et simples.
- [ ] Une seule police, boutons secondaires contrastés.
- [ ] Testé en 375, 768, 1024 et 1440 px, rien ne déborde.
- [ ] Messages : chargement, aucun résultat, erreur (et retrait de l'état d'erreur).
- [ ] Debounce, pas de double requête, annulation des recherches, `Promise.all`, promesses avec `.catch()`.
- [ ] README complet : choix justifiés (mobile/desktop first) et déclaration d'usage de l'IA.
- [ ] Captures d'écran si demandées.
- [ ] Console vide d'erreurs.

---

## 11. Boîte à outils (code validé, à adapter au sujet)

### Variables CSS
```css
:root {
  --bg: #0b1020;
  --surface: #161d33;
  --surface-2: #232c4a;
  --text: #f2f4ff;
  --text-muted: #a3abc7;
  --accent: #2563eb;
  --focus: #60a5fa;
  --error: #ff6b6b;
  --success: #4ade80;

  --space-sm: 10px;
  --space-md: 20px;
  --space-lg: 40px;

  --radius-sm: 6px;
  --radius-md: 10px;

  --font: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  --speed: 0.2s;
}
```

### Focus visible et boutons
```css
:focus-visible {
  outline: 3px solid var(--focus);
  outline-offset: 2px;
}

button {
  padding: var(--space-sm) var(--space-md);
  background: var(--accent);
  color: var(--text);
  font: inherit;
  border: 1px solid transparent;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: background var(--speed), transform var(--speed);
}

button:hover {
  transform: translateY(-2px);
}

.button-secondary {
  background: var(--surface-2);
  border-color: var(--text-muted);
}
```

### Cartes : survol et apparition
```css
.card {
  background: var(--surface);
  border-radius: var(--radius-md);
  padding: var(--space-sm);
  transition: transform var(--speed), box-shadow var(--speed);
  animation: appear 0.3s ease both;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgb(0 0 0 / 0.3);
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

### Grille mobile first (2 colonnes en mobile)
```css
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: var(--space-md);
  list-style: none;
  padding: 0;
}

@media (min-width: 768px) {
  .list {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
}
```

### Menu burger animé + page active
HTML (identique sur toutes les pages, seul `aria-current` change de lien) :
```html
<button class="toggle" type="button" aria-label="Menu" aria-expanded="false" aria-controls="main-nav">☰</button>
<nav class="nav" id="main-nav" aria-label="Navigation principale">
  <ul>
    <li><a href="index.html" aria-current="page">Accueil</a></li>
    <li><a href="about.html">À propos</a></li>
  </ul>
</nav>
```
CSS (on ne peut pas animer `display: none`, donc `max-height` + `visibility`) :
```css
.nav {
  width: 100%;
  max-height: 0;
  overflow: hidden;
  visibility: hidden;
  transition: max-height 0.3s ease, visibility 0.3s;
}

.nav.open {
  max-height: 300px;
  visibility: visible;
}

.nav a[aria-current="page"] {
  font-weight: 700;
  border-bottom: 2px solid var(--accent);
}

@media (min-width: 768px) {
  .toggle {
    display: none;
  }

  .nav {
    width: auto;
    max-height: none;
    visibility: visible;
  }
}
```
JS (`menu.js`, importé par chaque point d'entrée avec `import "./menu.js";`) :
```js
const toggle = document.querySelector(".toggle");
const nav = document.querySelector(".nav");

// ouvre ou ferme le menu et garde aria-expanded à jour
function setMenu(open) {
  nav.classList.toggle("open", open);
  toggle.setAttribute("aria-expanded", String(open));
}

toggle.addEventListener("click", () => setMenu(!nav.classList.contains("open")));

// Échap referme le menu et rend le focus au bouton
document.addEventListener("keydown", event => {
  if (event.key === "Escape" && nav.classList.contains("open")) {
    setMenu(false);
    toggle.focus();
  }
});
```

### Loader et messages
HTML :
```html
<div class="loader" hidden></div>
<p class="message" aria-live="polite"></p>
```
CSS :
```css
.loader {
  width: 40px;
  height: 40px;
  margin: var(--space-md) auto;
  border: 4px solid var(--surface-2);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.message.error {
  color: var(--error);
}
```
JS :
```js
const loader = document.querySelector(".loader");
const message = document.querySelector(".message");

function showMessage(text, isError) {
  message.textContent = text;
  if (isError) message.classList.add("error");
  else message.classList.remove("error");
}

function setLoading(isLoading) {
  loader.hidden = !isLoading;
  if (isLoading) showMessage("Chargement…");
}
```

### API : GET, POST et requêtes en parallèle
```js
// GET simple, sans annulation : utilisable pour plusieurs requêtes en même temps
export async function getJSON(url) {
  const response = await fetch(url);
  if (!response.ok) throw new Error("HTTP error " + response.status);
  return response.json();
}

// POST : envoie un objet en JSON et renvoie la réponse du serveur
export async function postJSON(url, body) {
  const response = await fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(body)
  });
  if (!response.ok) throw new Error("HTTP error " + response.status);
  return response.json();
}

// plusieurs requêtes indépendantes en parallèle plutôt qu'une par une
export function getAll(urls) {
  return Promise.all(urls.map(url => getJSON(url)));
}
```

### Recherche : annulation et cache (réservés à la recherche)
```js
const searchCache = new Map();
let searchController;

export async function searchJSON(url) {
  if (searchCache.has(url)) return searchCache.get(url);

  // annule seulement la recherche précédente si elle n'est pas finie
  if (searchController) searchController.abort();
  searchController = new AbortController();

  const response = await fetch(url, { signal: searchController.signal });
  if (!response.ok) throw new Error("HTTP error " + response.status);
  const data = await response.json();
  searchCache.set(url, data);
  return data;
}
```
Dans le `catch`, ignorer l'annulation :
```js
async function runSearch(url) {
  try {
    const data = await searchJSON(url);
    return data;
  } catch (error) {
    if (error.name === "AbortError") return;
    showMessage("Erreur : impossible de contacter le serveur.", true);
  }
}
```

### Filtrage en local (données déjà chargées, aucune requête)
```js
function filterItems(items, term) {
  const query = term.trim().toLowerCase();
  return items.filter(item => item.name.toLowerCase().includes(query));
}
```

### Debounce annulable (pas de double requête sur Entrée)
```js
function debounce(fn, delay) {
  let timer;
  const debounced = (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
  debounced.cancel = () => clearTimeout(timer);
  return debounced;
}

const debouncedSearch = debounce(search, 300);
searchInput.addEventListener("input", () => debouncedSearch(searchInput.value));

form.addEventListener("submit", event => {
  event.preventDefault();
  debouncedSearch.cancel();
  search(searchInput.value);
});
```

### Paramètre d'URL (page de détail)
Lien vers la page de détail, créé en JS :
```js
const link = document.createElement("a");
link.href = `detail.html?id=${item.id}`;
link.textContent = item.name;
```
Lecture sur la page de détail :
```js
const id = Number(new URLSearchParams(window.location.search).get("id"));

if (!id) {
  showMessage("Élément introuvable.", true);
}
```

### Formulaire : validation + POST + mise à jour de l'affichage
HTML :
```html
<form class="add-form" novalidate>
  <label for="title">Titre</label>
  <input id="title" name="title" type="text" required minlength="3" maxlength="100">
  <p class="form-error" aria-live="polite"></p>
  <button type="submit">Ajouter</button>
</form>
```
JS :
```js
form.addEventListener("submit", async event => {
  event.preventDefault();
  const title = form.title.value.trim();

  // validation côté client : règles HTML5 + vérification du texte réel
  if (!form.checkValidity() || title.length < 3) {
    formError.textContent = "Le titre doit contenir au moins 3 caractères.";
    form.title.focus();
    return;
  }
  formError.textContent = "";

  try {
    const created = await postJSON(API_URL, { title, completed: false });
    list.prepend(createItem(created));
    form.reset();
    showMessage("Élément ajouté.");
  } catch (error) {
    showMessage("Erreur : l'ajout a échoué.", true);
  }
});
```

### Apparition au scroll (optionnelle)
```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s, transform 0.5s;
}

.reveal.visible {
  opacity: 1;
  transform: none;
}
```
```js
// ajoute la classe "visible" quand l'élément entre dans l'écran
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add("visible");
      observer.unobserve(entry.target);
    }
  });
});

document.querySelectorAll(".reveal").forEach(element => observer.observe(element));
```
Penser à ajouter `.reveal` dans la règle `prefers-reduced-motion` (`opacity: 1; transform: none;`).

### localStorage
```js
export function readList(key) {
  try {
    return JSON.parse(localStorage.getItem(key)) || [];
  } catch (error) {
    return [];
  }
}

export function saveList(key, list) {
  localStorage.setItem(key, JSON.stringify(list));
}
```

### Squelette du README
```md
# Nom du projet

Description en 2 lignes.

## Lancer le projet
Ouvrir le dossier avec Live Server (ne fonctionne pas en file://).

## Fonctionnalités
- ...

## Architecture
- (arborescence du projet et rôle de chaque fichier)

## Choix techniques
- Mobile first / desktop first : [choix] parce que [justification].
- Modules ES, fetch + async/await, debounce, annulation des recherches, Promise.all...
- Accessibilité : sémantique, ARIA, navigation clavier, prefers-reduced-motion.

## Tests réalisés
Validateur W3C, Lighthouse/axe, 375 / 768 / 1024 / 1440 px, [navigateurs du sujet].

## Captures d'écran
(si demandées)

## Utilisation de l'IA
Projet réalisé avec l'aide de Claude (Anthropic), autorisé par l'enseignant :
[ce pour quoi elle a servi]. Le code a été relu, testé et compris.
```
