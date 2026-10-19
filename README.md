# Monthly Transport Planner (Planning Transport Mensuel)

A web application to plan daily transport operations, price each job and track margins, with data stored online (Supabase) and one-click exports (Excel, image, print).

Built with **plain HTML, CSS and JavaScript** (no framework, no build step).

## Features

**Daily planning**
- Editable table, one day at a time (date picker and previous/next buttons)
- Each row: associate or subcontractor, job site, equipment, client, client contact, instructions, driver, site / order / delivery-note numbers, hours
- Copy and paste a whole day, add or delete rows, duplicate detection, colour marking of rows
- Filters by associate, client, job site and equipment
- Undo / redo (`Ctrl+Z` / `Ctrl+Y`)

**Pricing and margins**
- Client rate, supplement and index, plus subcontractor rate, supplement and index, per row
- Automatic totals and margins (client side, subcontractor side, net margin)
- Configuration screens for clients (with groups and categories), associates / subcontractors, drivers and client phone contacts
- Price-revision indices configurable per category (annual and monthly values)

**Export**
- Monthly **Excel** file (`xlsx-js-style`)
- **Copy the planning as an image** to the clipboard (`html2canvas`), in two versions: with order numbers, or up to the client supplement column
- **Print** layout

**Data**
- Online storage with **Supabase** and email / password login (`base.js`)
- Full configuration backup and restore
- Data integrity check with automatic repair

## Tech stack

| Area | Technology |
|---|---|
| Front end | HTML5, CSS3, vanilla JavaScript |
| Database and auth | Supabase (`@supabase/supabase-js` 2.x) |
| Export | `xlsx-js-style` 1.2.0, `html2canvas` 1.4.1 |

## Project structure

```
├── index.html    # Page structure, toolbar, config panels, help modal
├── styles.css    # Styling (screen and print)
├── script.js     # Application logic: planning table, pricing, config, exports, undo/redo
├── base.js       # Supabase layer: replaces localStorage with an online database + login
└── image.avif    # Login screen background
```

`base.js` intercepts the browser storage calls used by `script.js`, so the application logic stays unchanged while the data lives in Supabase.

## Getting started

1. **Clone the repository**
   ```bash
   git clone https://github.com/hlandais9051/scheduling.git
   cd scheduling
   ```
2. **Create a Supabase project** and add your own credentials at the top of `base.js` (`SUPABASE_URL` and the public / publishable key).
3. **Create the tables** the app expects:
   - `config` (`cle`, `valeur`, `maj`): key / value storage for all settings
   - `lignes_planning` (`date_jour`, `position`, `donnees`, …): one record per planning row
   - a SQL function `remplacer_jour` that replaces all rows of one day
4. **Enable Row Level Security** on every table and allow access to authenticated users only.
5. **Create a user** (Supabase → Authentication) to log in with.
6. **Run it locally** with any static server:
   ```bash
   python -m http.server 8000
   ```
   then open <http://localhost:8000>.

## Notes

- The public Supabase key is designed to be exposed in a browser, but it is only safe if Row Level Security is correctly configured.

## Author

**Hugo Landais**, engineering student at ISEN Nantes, [LinkedIn](https://www.linkedin.com/in/hugolandais)

---

## 🇫🇷 Version française

# Planning Transport Mensuel

Application web pour planifier les opérations de transport au quotidien, chiffrer chaque prestation et suivre les marges, avec stockage en ligne (Supabase) et exports en un clic (Excel, image, impression).

Développée en **HTML, CSS et JavaScript pur** (sans framework, sans étape de compilation).

### Fonctionnalités

**Planning journalier**
- Tableau modifiable, jour par jour (calendrier et boutons précédent / suivant)
- Chaque ligne : associé ou affrété, chantier, matériel, client, contact client, consigne, chauffeur, numéros de chantier / commande / bon, heures
- Copier-coller d'une journée entière, ajout et suppression de lignes, détection de doublons, marquage des lignes par couleur
- Filtres par associé, client, chantier et matériel
- Annuler / rétablir (`Ctrl+Z` / `Ctrl+Y`)

**Tarifs et marges**
- Tarif, supplément et indice côté client, et côté affrété, pour chaque ligne
- Totaux et marges calculés automatiquement (côté client, côté affrété, marge nette)
- Écrans de configuration : clients (groupes et catégories), associés / affrétés, chauffeurs, téléphones des clients
- Indices de révision des prix paramétrables par catégorie (valeurs annuelles et mensuelles)

**Exports**
- **Excel** mensuel (`xlsx-js-style`)
- **Copie du planning en image** dans le presse-papiers (`html2canvas`), en deux versions : avec les numéros de commande, ou jusqu'à la colonne supplément client
- Mise en page pour l'**impression**

**Données**
- Stockage en ligne avec **Supabase** et connexion par e-mail et mot de passe (`base.js`)
- Sauvegarde et restauration complètes de la configuration
- Vérification de l'intégrité des données avec réparation automatique

### Installation

1. Clone le dépôt, puis crée un projet **Supabase**.
2. Renseigne ton URL et ta clé publique en haut de `base.js`.
3. Crée les tables `config` et `lignes_planning` et la fonction SQL `remplacer_jour` (voir la section anglaise ci-dessus).
4. Active la **Row Level Security** sur chaque table, avec un accès réservé aux utilisateurs connectés.
5. Crée un utilisateur (Supabase → Authentication).
6. Lance un serveur statique, par exemple `python -m http.server 8000`, puis ouvre <http://localhost:8000>.

### Remarques

- La clé publique Supabase est faite pour être visible dans un navigateur, mais elle n'est sûre que si la Row Level Security est bien configurée.
