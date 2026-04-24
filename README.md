# GPS Tracker — Application Web Progressive (PWA)

## Fonctionnement

Application 100% JavaScript qui :
- Récupère ta position GPS toutes les ~3 secondes
- Trace ton parcours en temps réel sur une carte (OpenStreetMap)
- Sauvegarde le tracé en local (même si tu fermes l'app)
- Fonctionne sur Android via Chrome, sans installation sur le Play Store

---

## Fichiers

```
gps-tracker/
├── index.html     ← Application principale
├── manifest.json  ← Manifest PWA (icône, nom, thème)
└── sw.js          ← Service Worker (cache offline)
```

---

## Installation sur Android (2 méthodes)

### Méthode 1 — Via un serveur local (réseau Wi-Fi)

1. **Sur ton PC**, installe un serveur HTTP simple :
   ```bash
   # Avec Python (déjà installé sur la plupart des PC)
   cd gps-tracker
   python -m http.server 8080

   # Ou avec Node.js
   npx serve .
   ```

2. **Trouve l'IP de ton PC** :
   - Windows : `ipconfig` dans cmd → cherche "Adresse IPv4" (ex: 192.168.1.10)
   - Mac/Linux : `ifconfig` ou `ip addr`

3. **Sur ton téléphone Android**, ouvre Chrome et va sur :
   ```
   http://192.168.1.10:8080
   ```

4. **Installer comme app** : Dans Chrome, appuie sur ⋮ → "Ajouter à l'écran d'accueil"

### Méthode 2 — Via GitHub Pages (hébergement gratuit)

1. Crée un compte [GitHub](https://github.com)
2. Crée un repository public `gps-tracker`
3. Upload les 3 fichiers dedans
4. Va dans Settings → Pages → Source: `main` → Save
5. Ton app sera dispo sur `https://ton-pseudo.github.io/gps-tracker`

> ⚠️ **Important** : Le GPS via navigateur nécessite **HTTPS** ou **localhost**. GitHub Pages fournit HTTPS gratuitement.

---

## Utilisation

1. Ouvre l'app dans Chrome
2. Autorise l'accès à la localisation quand Chrome le demande
3. Appuie sur **▶ Démarrer**
4. Bouge ! Ton tracé s'affiche en vert sur la carte
5. Appuie sur **■ Arrêter** pour mettre en pause
6. Le tracé est sauvegardé automatiquement
7. **✕** efface le tracé

---

## Fonctionnalités

- ✅ Tracé GPS en temps réel (toutes les 3 secondes)
- ✅ Carte interactive zoomable (OpenStreetMap)
- ✅ Compteur de points, distance totale, précision GPS
- ✅ Sauvegarde locale (localStorage) — tracé persistant
- ✅ Application installable sur l'écran d'accueil Android
- ✅ Fonctionne hors-ligne après le premier chargement (Service Worker)
- ✅ Interface sombre optimisée mobile

---

## Notes techniques

- **GPS polling** : utilise `watchPosition` avec filtre à 3 secondes côté JS
- **Carte** : Leaflet.js + tuiles OpenStreetMap (gratuit, sans clé API)
- **Distance** : calculée avec la formule de Haversine (distance sphérique)
- **Stockage** : `localStorage` — les données restent sur le téléphone
- **Précision GPS** : activé en mode haute précision (`enableHighAccuracy: true`)
