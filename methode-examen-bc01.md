# Méthode examen BC01 – Front-end sans framework

> Fichier de préparation à donner à Claude au début de la conversation d'examen, avec le sujet.
> Il est valable quel que soit le sujet : il contient les règles du prof, la grille, le feedback de l'entraînement, la méthode de travail et du code prêt à l'emploi.

---

## 0. Instructions pour Claude (à lire en premier)

1. Lis ce fichier en entier, puis le sujet.
2. Relie chaque demande du sujet à un critère de la grille (section 2).
3. Propose en moins de 10 minutes : la liste des fonctionnalités, l'arborescence des fichiers, le nom du projet (celui du sujet). Attends la validation de Rayane.
4. Demande à Rayane de connecter **tout le dossier du projet** dès le début (pas un sous-dossier), pour pouvoir lire, modifier et tester les fichiers directement.
5. Produis ensuite le code **par blocs** (pas fichier par fichier), teste, et explique chaque bloc en 1 ou 2 phrases pour que Rayane puisse le défendre.
6. Applique la checklist finale (section 8) avant le rendu.
7. Ton : franc, concis, en français, sans flatterie. Signale clairement un conflit entre deux règles au lieu de trancher en silence.

---

## 1. Contexte de l'épreuve

- **BC01** : concevoir et réaliser des interfaces utilisateur adaptatives et interactives front-end.
- Épreuve **individuelle**, **4 heures**, sur ordinateur, **sans framework** (HTML, CSS, JavaScript natif en modules).
- **Livrable** : le code produit.
- **IA autorisée** par le prof. La déclarer dans le README (section « Utilisation de l'IA »). Rayane doit comprendre et savoir expliquer chaque partie du code.
- Compétences évaluées : C1 à C5.

---

## 2. Grille d'évaluation (11 critères × 5 points = 55)

Niveaux : 0 (non traité), 2 (insuffisant), 3 (suffisant, améliorable), **5 (professionnel)**.

| Critère | Ce qu'il faut pour 5/5 |
|---|---|
| **Cr1.1 W3C** | 0 erreur au validateur (validator.w3.org) sur **toutes** les pages. Aucun fichier en 404 (favicon, images). |
| **Cr1.2 Accessibilité** | Sémantique correcte, `alt` partout (`alt=""` si décoratif ou doublon du texte), ARIA juste, focus visible, tout faisable au clavier, 0 alerte axe / Lighthouse ≥ 95. Pas de lien vers une section cachée. |
| **Cr1.3 Clarté du code** | Indentation propre, petits commentaires utiles, **une seule langue pour les noms** (anglais), une responsabilité par fichier, fichiers < 150 lignes. |
| **Cr2.1 Cohérence du design** | Tokens CSS, mêmes header / nav / footer sur **toutes** les pages, boutons secondaires bien contrastés, **une seule police** (ex. Poppins 400 et 700 uniquement). |
| **Cr2.2 Expérience utilisateur** | Navigation identique partout, règle des 3 clics, messages clairs (chargement, « aucun résultat », erreur qui disparaît quand ça remarche), bouton retour sans rechargement. |
| **Cr3.1 Responsive** | Mobile-first, rien ne déborde, testé en 375 / 768 / 1440 px, grille à 2 colonnes en mobile, menu burger en mobile. |
| **Cr4.1 Fonctionnalités** | **Toutes** les fonctionnalités du sujet, **y compris les animations** (transitions, `@keyframes`, menu animé), validation de formulaire. |
| **Cr4.2 Compatibilité** | API standard uniquement, toute promesse gérée (`.catch()`), test Chrome + Firefox. |
| **Cr4.3 ECMAScript** | Modules ES, `async/await`, `const/let`, spread, fonctions fléchées, template literals. |
| **Cr5.1 AJAX** | `fetch` sans rechargement de page, `response.ok` vérifié, `try/catch`. |
| **Cr5.2 Performance** | Debounce 300 ms, **pas de double requête** (annuler le debounce au `submit`), **annulation des requêtes périmées** (`AbortController`), petit cache, requêtes groupées quand c'est possible. |

---

## 3. Règles permanentes du prof

### HTML et sémantique
- La balise dit ce que la chose **est**, la classe dit à quoi elle **ressemble**.
- `header`, `main`, `footer` présents. **Un seul** `<h1>` par page, aucun niveau de titre sauté.
- `<section>` uniquement si elle a un titre (sinon `<div>`). `<article>` pour un élément autonome (une carte).
- Listes de résultats en `<ul>/<li>` (ou `<ol>` si l'ordre compte).
- `<button>` = agit dans la page. `<a href>` = emmène ailleurs. **Jamais de div cliquable.**
- Toute saisie dans un `<form>` avec un `<label for="...">` lié à l'input.
- Test : désactiver le CSS, la page doit rester lisible de haut en bas.

### Accessibilité (ARIA)
- Pas d'ARIA vaut mieux que du mauvais ARIA. Un vrai `<button>` plutôt qu'un `role="button"`.
- `aria-pressed` : bouton à deux états (favori, activer/désactiver), mis à jour à chaque clic.
- `aria-expanded` : bouton qui ouvre ou ferme (burger), mis à jour à chaque clic, **Échap referme**.
- `aria-label` : seulement si aucun texte visible (bouton icône).
- `aria-live="polite"` : zone de message (chargement, nombre de résultats, erreur).
- `aria-current` : élément actif (page en cours, onglet ou élément sélectionné).
- `alt` sur chaque image, `alt=""` si décorative ou si le texte voisin dit déjà la même chose.
- Classe `sr-only` pour un texte lu mais invisible.
- Les 3 fautes graves : `outline: none` sans remplacement, une div cliquable, un état montré par la couleur seule.

### Architecture
```
nom-du-projet/
├── index.html
├── css/  reset.css  tokens.css  layout.css  components.css  (responsive.css)
└── js/   main.js  api.js  render.js  format.js  (+ un fichier par responsabilité)
```
1. **Un seul script** dans le HTML : `<script type="module" src="js/main.js"></script>`.
2. `api.js` ne touche **jamais** au DOM : il reçoit un paramètre, il renvoie des données.
3. `render.js` ne fait **jamais** de `fetch` : il reçoit un objet, il renvoie un élément sans l'insérer.
4. **Aucune variable globale** : l'état de l'app vit dans un seul objet `state` dans `main.js`.
5. Un fichier de plus de **150 lignes** est à couper.
- `layout.css` = où sont placés les gros blocs. `components.css` = à quoi ressemble chaque élément réutilisable.
- Variables CSS nommées par **rôle** (`--bg`, `--text`, `--accent`), jamais par couleur. Espacements et rayons en tokens (`--space-md`, `--radius-md`).
- Grille de cartes : `display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;` (en desktop).

### JavaScript imposé
- Données de l'API insérées avec `createElement` + `textContent`. **Jamais `innerHTML`** pour des données (pour vider un élément : `replaceChildren()`).
- `createCard(item)` crée et renvoie l'élément, l'insertion se fait ailleurs (`list.appendChild(card)`).
- Id stocké avec `card.dataset.id = ...` (attention : `dataset` renvoie toujours une **chaîne**, convertir avec `Number()` avant un `includes`).
- **Délégation** : un seul écouteur sur la liste, `event.target.closest(".like-button")` puis `return`, sinon `closest(".card")`.
- Bouton à deux états : `const pressed = btn.getAttribute("aria-pressed") === "true"; btn.setAttribute("aria-pressed", String(!pressed));` puis changer aussi le texte ou l'icône (jamais la couleur seule).
- `encodeURIComponent(term)` dans l'URL. `if (!response.ok) throw new Error(...)`. Zéro résultat n'est pas une erreur, c'est un état à afficher.
- Tri sur une **copie** : `[...items].sort((a, b) => a.x - b.x)`.
- `localStorage` : `JSON.stringify` à l'écriture, `JSON.parse` dans un `try/catch` avec repli sur `[]` à la lecture, pas de doublons (`includes` avant `push`).
- Toute méthode qui renvoie une promesse (ex. `media.play()`) a son `.catch()`.
- Fonctions de mise en forme pures dans `format.js` (ex. durée en `m:ss` avec `padStart(2, "0")`).

### Serveur et outils
- Jamais en `file://` : Live Server (VS Code) ou `py -m http.server 8000`, adresse en `http://`.
- F12 : Console (erreurs), Elements (DOM réel), Network (requêtes, statut 200/404), Lighthouse (accessibilité).

---

## 4. Feedback de l'entraînement E1 (≈ 15/20) – à ne plus refaire

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
| Message d'erreur resté rouge | `classList.remove("error")` au début de chaque requête. |
| « 0 résultats trouvés » affiché tel quel | Message dédié : « Aucun résultat ». |
| Une carte par ligne en mobile | Mobile-first, `minmax(150px, 1fr)` en mobile → 2 colonnes. Breakpoint 768 px. |
| Entrée = 2 requêtes | Annuler le debounce au `submit`. |
| Réponse lente qui écrase une récente | `AbortController`. |
| Pas de README | README avec documentation technique **et** déclaration de l'IA. |

---

## 5. Façon de travailler de Rayane

- Code **simple mais propre** : pas de syntaxe tordue, mais bien nommé, bien découpé. Le niveau « professionnel » de la grille passe par la clarté, pas par la complexité.
- Peu de classes, des noms courts et clairs.
- Petits commentaires en français, naturels, seulement là où ils aident.
- Garder **exactement** les noms imposés par le prof (`createCard`, `search`, `debounce`, `debouncedSearch`, etc.).
- Expliquer chaque bloc produit en 1 ou 2 phrases.
- Renommer une fonction ou un fichier : faire Ctrl+F pour corriger **tous** les appels et imports, dans tous les fichiers.
- Rayane veut comprendre : répondre clairement à ses questions de compréhension.

---

## 6. Méthode le jour J (4 heures)

| Temps | Étape |
|---|---|
| 0:00 – 0:15 | Lire le sujet, le relier à la grille. Claude propose fonctionnalités + arborescence + nom. Validation. |
| 0:15 – 0:30 | Créer le dossier (nom en minuscules avec tirets), le connecter, lancer Live Server. Poser HTML, reset, tokens, layout. |
| 0:30 – 2:15 | Fonctionnalités JS par blocs : `api.js` → `render.js` → `main.js` → le reste. **Tester dans le navigateur après chaque bloc** (console ouverte). |
| 2:15 – 3:00 | CSS : composants, **animations**, responsive mobile-first. |
| **≈ 3:00** | **Déposer une première version de secours.** |
| 3:00 – 3:30 | Tests : W3C sur chaque page, Lighthouse / axe, 375 / 768 / 1440 px, parcours complet au clavier, Firefox. |
| 3:30 – 3:50 | README. |
| 3:50 – 4:00 | Checklist finale, zip, rendu. |

Règle d'or : ne jamais écrire plus de 10 lignes sans tester.

---

## 7. Pièges déjà rencontrés (et diagnostic rapide)

| Symptôme | Cause probable |
|---|---|
| `Cannot GET /js/xxx.js` | Faute dans le nom du fichier (vécu : `palyer.js`) ou mauvais dossier. |
| `Cannot read properties of null` | Le sélecteur JS ne correspond plus au HTML (`#menu` alors que le bouton a `class="toggle"`). |
| Tout le JS est mort | Un seul import cassé ou une erreur de syntaxe (vécu : `}é`) bloque tout le module. |
| `xxx is not defined` | Fonction renommée ou supprimée mais encore appelée. |
| Espacements à 0 alors que les couleurs marchent | Variable CSS inexistante ou mal écrite dans `tokens.css`. |
| Le CSS modifié ne change rien | Cache (Ctrl+Maj+R) ou Live Server lancé sur un autre dossier. |
| Message « impossible de contacter le serveur » | Le `catch` attrape **toute** erreur : ajouter `console.error(error)` pour voir la vraie. |

---

## 8. Checklist finale avant rendu

- [ ] Nom du site et du dossier = ceux du sujet, aucune marque réelle.
- [ ] Toutes les fonctionnalités du sujet présentes.
- [ ] Animations : survol cartes et boutons, apparition des résultats, menu, `prefers-reduced-motion`.
- [ ] Header / nav / footer / favicon identiques sur toutes les pages, aucun 404 (onglet Network).
- [ ] 0 erreur W3C sur chaque page.
- [ ] Lighthouse accessibilité ≥ 95, parcours complet au clavier, focus visible.
- [ ] Un seul `h1` par page, pas de niveau sauté.
- [ ] Aucun `innerHTML` avec des données. Aucune variable globale.
- [ ] Noms de code tous en anglais, fichiers < 150 lignes.
- [ ] Une seule police, boutons secondaires contrastés.
- [ ] Testé en 375, 768 et 1440 px, 2 colonnes en mobile.
- [ ] Messages : chargement, aucun résultat, erreur (et retrait de la classe `error`).
- [ ] Debounce, pas de double requête, `AbortController`, `play().catch()`.
- [ ] README complet avec la déclaration d'usage de l'IA.
- [ ] Console vide d'erreurs.

---

## 9. Boîte à outils (code validé, à adapter au sujet)

### Police (une seule, 2 graisses)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap" rel="stylesheet">
```

### Tokens
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

  --space-sm: 10px;
  --space-md: 20px;
  --space-lg: 40px;

  --radius-sm: 6px;
  --radius-md: 10px;

  --font: "Poppins", system-ui, sans-serif;
  --speed: 0.2s;
}
```

### Focus visible et boutons secondaires contrastés
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

### Grille mobile-first (2 colonnes en mobile)
```css
.result {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: var(--space-md);
  list-style: none;
  padding: 0;
}

@media (min-width: 768px) {
  .result {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
}
```

### Menu burger animé (mobile-first)
HTML (identique sur toutes les pages) :
```html
<button class="toggle" type="button" aria-label="Menu" aria-expanded="false" aria-controls="main-nav">☰</button>
<nav class="nav" id="main-nav" aria-label="Navigation principale">
  <ul>
    <li><a href="index.html">Accueil</a></li>
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
JS (`menu.js`, importé par `main.js` avec `import "./menu.js";` et chargé seul sur les pages sans `main.js`) :
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

### API : fetch avec erreur HTTP, annulation et cache
```js
const cache = new Map();
let controller;

export async function getJSON(url) {
  if (cache.has(url)) return cache.get(url);

  // annule la requête précédente si elle n'est pas finie
  if (controller) controller.abort();
  controller = new AbortController();

  const response = await fetch(url, { signal: controller.signal });
  if (!response.ok) throw new Error("Erreur HTTP " + response.status);
  const data = await response.json();
  cache.set(url, data);
  return data;
}
```
Dans le `catch` de `main.js`, ignorer l'annulation :
```js
} catch (error) {
  if (error.name === "AbortError") return;
  showMessage("Erreur : impossible de contacter le serveur.", true);
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

### Messages (chargement, aucun résultat, erreur)
```js
function showMessage(text, isError) {
  message.textContent = text;
  if (isError) message.classList.add("error");
  else message.classList.remove("error");
}
```

### localStorage
```js
export function readFavorites() {
  try {
    return JSON.parse(localStorage.getItem("favorites")) || [];
  } catch (error) {
    return [];
  }
}

export function toggleFavorite(favorites, id) {
  if (favorites.includes(id)) favorites.splice(favorites.indexOf(id), 1);
  else favorites.push(id);
  localStorage.setItem("favorites", JSON.stringify(favorites));
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
- css/ : reset, tokens, layout, components, responsive
- js/ : main (point d'entrée), api, render, ...

## Choix techniques
- Modules ES, fetch + async/await, debounce 300 ms, AbortController, localStorage...
- Accessibilité : ARIA, navigation clavier, prefers-reduced-motion

## Tests réalisés
W3C, Lighthouse/axe, 375 / 768 / 1440 px, Chrome et Firefox.

## Utilisation de l'IA
Projet réalisé avec l'aide de Claude (Anthropic), autorisé par l'enseignant :
[ce pour quoi elle a servi]. Le code a été relu, testé et compris.
```
