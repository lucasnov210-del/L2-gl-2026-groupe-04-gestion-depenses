# 💰 Gestion des dépenses personnelles

Mini-projet **Vue.js 3 + Vite** — **Groupe 4** (Projet 4), L2 Génie Informatique, ISSTM.

Application permettant d'enregistrer et de suivre ses dépenses. Les données sont conservées dans le `localStorage` du navigateur (aucun backend).

## Membres du groupe

| N° | Nom et prénoms | N° d'inscription |
|----|----------------|------------------|
| 1 | RAZAFINDRAVINA Lucia | 13ISST24-1707FGCI/Ginfo |
| 2 | ZAFY MARICETTE Romuna | 13ISST24-1572FGCI/Ginfo |
| 3 | TIANJARA Wendy Géraldo | 12ISST23-1407FGCI/GInfo |
| 4 | TSARALAZA Luciano Carlos | 11ISST22-1080FGCI/Ginfo |
| 5 | Rakotonandrasana Jojo | 13ISST24-1538FGCI/GInfo |
| 6 | TAHIANJANAHARY Rolland Andry | 13ISST24-1800FGCI/Ginfo |
| 7 | RAVELONANDRASANA Themie Nilsen | 13ISST24-1822FGCI/Ginfo |
| 8 | HANITRINIAINA Emelia Brunah | 13ISST24-1743FGCI/Ginfo |
| 9 | Rakotonindrina Deraina Mamihasina Sylvio | 13ISST24-1723FGCI/GInfo |
| 10 | VELONDRAZANA Fazilah | 13ISST24-1578FGCI/GInfo |
| 11 | RANAIVOJAONA Bridgette Elysia | 13ISST24-1583FGCI/GInfo |
| 12 | RAKOTOMANGA Maminiaina Jedidia | 13ISST24-1653FGCI/GInfo |
| 13 | RAZAFIMANDIMBY Franthony | 13ISST24-1731FGCI/GInfo |

## Fonctionnalités réalisées

- ✅ Ajouter une dépense (description, **catégorie**, **montant**, date) avec validation
- ✅ Modifier une dépense (le formulaire se remplit, bouton *Enregistrer* / *Annuler*)
- ✅ Supprimer une dépense (avec confirmation)
- ✅ Afficher le **total** (du filtre courant + total général)
- ✅ **Filtrer par catégorie**
- ✅ Sauvegarde automatique dans `localStorage`

## Notions Vue.js utilisées

| Notion | Où |
|--------|----|
| `v-model` | `ExpenseForm.vue` (champs), `App.vue` → `ExpenseFilter` (`v-model="selectedCategory"`) |
| `v-for` | `ExpenseList.vue`, `ExpenseForm.vue` / `ExpenseFilter.vue` (options) |
| `v-if` / `v-else` | `ExpenseList.vue` (liste vide), `ExpenseForm.vue` (erreur, bouton Annuler), `ExpenseTotal.vue` |
| Événements (`emit`) | `save`, `cancel`, `edit`, `delete`, `update:modelValue` |
| `props` | `expense`, `expenses`, `total`, `editingId`, `active`… |
| `ref()` / `reactive()` / `computed` / `watch` | `App.vue`, `ExpenseForm.vue` |

## Structure

```
src/
├── App.vue                    # état global + orchestration
├── main.js
├── style.css
├── components/
│   ├── ExpenseForm.vue        # ajout / modification
│   ├── ExpenseFilter.vue      # filtre par catégorie
│   ├── ExpenseTotal.vue       # total affiché
│   ├── ExpenseList.vue        # tableau des dépenses
│   └── ExpenseItem.vue        # une ligne du tableau
└── utils/
    ├── expenses.js            # logique pure (ajout, modif, suppression, filtre, total)
    └── storage.js             # lecture / écriture localStorage
tests/expenses.test.mjs        # tests de la logique métier
```

## Installation

Prérequis : [Node.js](https://nodejs.org) 18 ou plus.

```bash
git clone https://github.com/<compte>/12-gl-2026-groupe-04-gestion-depenses.git
cd 12-gl-2026-groupe-04-gestion-depenses
npm install
npm run dev      # http://localhost:5173
npm test         # tests de la logique métier
npm run build    # version de production (dossier dist/)
```

## Captures d'écran

> À ajouter après `npm run dev` (dossier `docs/`) :

![Liste des dépenses](docs/capture-liste.png)
![Ajout / modification](docs/capture-formulaire.png)
![Filtre par catégorie](docs/capture-filtre.png)

## Contribution de chaque membre

| Membre | Contribution |
|--------|--------------|
| RAZAFINDRAVINA Lucia | `ExpenseForm.vue` (formulaire d'ajout) |
| ZAFY MARICETTE Romuna | `ExpenseForm.vue` (mode modification, bouton Annuler) |
| TIANJARA Wendy Géraldo | `ExpenseList.vue` (tableau, message liste vide) |
| TSARALAZA Luciano Carlos | `ExpenseItem.vue` (ligne, boutons Modifier / Supprimer) |
| Rakotonandrasana Jojo | `ExpenseFilter.vue` (filtre par catégorie) |
| TAHIANJANAHARY Rolland Andry | `ExpenseTotal.vue` (total et total général) |
| RAVELONANDRASANA Themie Nilsen | `App.vue`, structure du projet, dépôt GitHub |
| HANITRINIAINA Emelia Brunah | `style.css` (interface) |
| Rakotonindrina Deraina Mamihasina Sylvio | `utils/expenses.js` (logique métier, validation) |
| VELONDRAZANA Fazilah | `utils/storage.js` (sauvegarde localStorage) |
| RANAIVOJAONA Bridgette Elysia | `tests/` (tests de la logique métier) |
| RAKOTOMANGA Maminiaina Jedidia | README (installation, captures d'écran) |
| RAZAFIMANDIMBY Franthony | Tests manuels dans le navigateur et démonstration |

## Git / GitHub

Dépôt du groupe, collaborateur invité : **@GasyCoder**. Chaque membre travaille avec ses propres commits (messages clairs : `Ajout formulaire dépense`, `Correction filtre catégorie`, `Amélioration interface`…).
