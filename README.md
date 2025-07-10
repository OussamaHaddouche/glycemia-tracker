# Glycemia Tracker - Application Offline-First avec SolidJS + Firebase

## ✨ Objectif

Créer une application **offline-first** pour suivre la glycémie au quotidien, principalement pour un usage personnel (ex : pour un proche diabétique), avec stockage local et synchronisation vers Firebase.

---

## 🤖 Fonctionnalités principales

### MVP (Minimum Viable Product)

* [ ] Ajouter une mesure de glycémie (valeur, contexte, notes)
* [ ] Historique des mesures avec recherche et filtre
* [ ] Graphique de l'évolution de la glycémie
* [ ] Statistiques simples (moyenne, max, min, écarts)
* [ ] Choix de l'unité (mg/dL ou mmol/L)
* [ ] Fonctionne hors ligne avec cache local (IndexedDB)
* [ ] Synchronisation auto avec Firebase Firestore
* [ ] Export des données (CSV / JSON)
* [ ] PWA installable

### Fonctionnalités avancées (Post-MVP)

* [ ] Rappels de mesures (matin, soir)
* [ ] Alertes visuelles hypo / hyperglycémie
* [ ] Tags personnalisables (repas, sport, stress...)
* [ ] Corrélations automatiques (ex : glycémie post-pizza)
* [ ] Partage de données (lien temporaire ou PDF)

---

## 📊 Plages de glycémie (mg/dL)

| Contexte       | Normal | Élevé (Hyper) | Bas (Hypo) |
| -------------- | ------ | ------------- | ---------- |
| A jeun         | 70-100 | >126          | <70        |
| 2h après repas | <140   | >180          | -          |

---

## 📒 Stack technique

### Frontend

* **SolidJS** (via Vite)
* **Kobalte** (bibliothèque de composants UI accessible et adaptée à SolidJS)
* **TailwindCSS** (UI rapide et responsive)
* **Chart.js** (graphiques de glycémie)
* **IndexedDB** (stockage offline local)
* **Vite Plugin PWA** (installable + offline)
* **Lucide Icons** (icônes SVG légères et modernes)
* **BiomeJs** (outil moderne de linting et formatting JavaScript/TypeScript)
* **solid-transition-group** (gestion simple et puissante des animations d’apparition/disparition dans SolidJS)

### Backend (Cloud Sync)

* **Firebase**

  * Firestore (base de données NoSQL)
  * Auth (facultatif)
  * Firestore persistence offline (via SDK)

---

## 📆 Structure des pages

### ✅ Accueil (`/`)

* Dernière mesure (valeur, couleur, heure)
* Graphique glycémie (jour/semaine)
* Moyenne journalière, nb mesures, % dans plage normale

### ➕ Ajouter une mesure (`/add`)

* Valeur glycémie (mg/dL ou mmol/L)
* Date & heure (auto ou manuelle)
* Contexte (liste : à jeun, après repas, sport, etc.)
* Notes libres

### 📅 Historique (`/history`)

* Liste des mesures
* Filtres (date, contexte, hypo/hyper)
* Modification / suppression

### 📊 Statistiques (`/stats`)

* Moyenne, min, max, écart-type
* Nb de mesures par jour
* Graphiques supplémentaires (histogramme, heatmap)

### ⚙️ Paramètres (`/settings`)

* Unité par défaut (mg/dL / mmol/L)
* Plages personnalisées (normal, hypo, hyper)
* Export CSV / JSON
* Gestion Firebase (auth, reset)

---

## 🛁 Structure de dossier (Vite + SolidJS)

```
src/
├── components/
│   ├── AddForm.tsx
│   ├── EntryCard.tsx
│   ├── GlycemiaChart.tsx
├── lib/
│   ├── firebase.ts       // init Firebase
│   ├── db.ts             // IndexedDB sync
│   ├── glycemyStore.ts   // Signal/store central
│   ├── converters.ts     // unités mg/dL ⇄ mmol/L
├── pages/
│   ├── Home.tsx
│   ├── Add.tsx
│   ├── History.tsx
│   ├── Stats.tsx
│   └── Settings.tsx
├── App.tsx
└── main.tsx
```

---

## ⚡ Étapes de développement

1. ✅ Init projet Vite + SolidJS + Tailwind
2. ✅ Configurer Firebase + Firestore
3. ✅ Créer base des composants + routing
4. ✅ Implémenter stockage local (IndexedDB)
5. ✅ Ajouter formulaire de mesure
6. ✅ Afficher historique + graphique
7. ✅ Ajouter calculs statistiques simples
8. ✅ Mettre en place export JSON / CSV
9. ✅ Ajouter gestion unités + conversions
10. ✅ Intégrer Firebase sync (online/offline)
11. ✅ Ajouter installation PWA

---

## 🔎 Calculs utiles (JS/TS)

### Moyenne

```ts
const avg = arr.reduce((a, b) => a + b, 0) / arr.length;
```

### Conversion

```ts
function mgToMmol(mg: number) {
  return +(mg * 0.0555).toFixed(1);
}
function mmolToMg(mmol: number) {
  return Math.round(mmol / 0.0555);
}
```

---

## 🔧 Donnée type

```ts
type GlycemiaEntry = {
  id: string;
  value: number;
  unit: 'mg/dL' | 'mmol/L';
  datetime: Date;
  context: 'fasting' | 'after_meal' | 'before_meal' | 'sport' | 'bedtime';
  notes?: string;
};
```

---

## 🚀 Idées futures (si besoin)

* OCR de mesures depuis photo
* Intégration capteurs Bluetooth
* Export PDF pour médecin
* UI vocale pour accessibilité
* Version mobile native (via Capacitor)

---

## ☕ Auteur

Projet personnel de **Oussama** pour sa mère, afin de créer une application simple, fiable, et efficace pour le suivi glycémique. Made with SolidJS ♥.
