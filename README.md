# 📍 LAB-10 | LocalisationSmartphone — Tracking GPS en temps réel

Une application Android démontrant la **géolocalisation GPS** avec `LocationManager` et l'envoi automatique des coordonnées vers un serveur PHP via **Volley**, avec gestion des permissions Android à l'exécution.

---

## ✨ Fonctionnalités

- 📡 **Localisation GPS en temps réel** via `LocationManager`
- 🗺️ **Affichage des coordonnées** : latitude, longitude, altitude, précision
- 📤 **Envoi automatique HTTP POST** à chaque changement de position
- 🔐 **Gestion des permissions** GPS à l'exécution (`onRequestPermissionsResult`)
- 🆔 **Identifiant unique** Android (`ANDROID_ID`) compatible Android 10+
- 🕐 **Horodatage** automatique de chaque position envoyée
- ⚠️ **Gestion des états du provider** GPS (disponible, indisponible, hors service)

---

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Langage | Java |
| UI | XML Layouts |
| Architecture | MVC |
| Géolocalisation | `LocationManager` / `LocationListener` |
| Requêtes HTTP | Volley |
| Identifiant appareil | `Settings.Secure.ANDROID_ID` |
| Serveur back-end | PHP + MySQL |
| Émulateur réseau | 10.0.2.2 (localhost hôte) |

---

## 📁 Architecture du projet

```bash
com.example.localisationsmartphone
├── MainActivity.java              # Contrôleur — GPS + envoi Volley
└── res/
    ├── layout/
    │   └── activity_main.xml          # Vue — affichage des coordonnées
    └── xml/
        └── network_security_config.xml  # Config sécurité réseau HTTP
```

---

## 📦 Dépendances

```gradle
dependencies {
    implementation 'com.android.volley:volley:1.2.1'
}
```

---

## 🔑 Permissions requises

```xml
<!-- AndroidManifest.xml -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

---

## 🧠 Concepts Android abordés

- 📌 **Permissions à l'exécution** avec `ActivityCompat.requestPermissions()`
- 📌 **Callback de permission** via `onRequestPermissionsResult()`
- 📌 **Géolocalisation** avec `LocationManager` et `LocationListener`
- 📌 **Événements GPS** : `onLocationChanged`, `onProviderEnabled`, `onProviderDisabled`, `onStatusChanged`
- 📌 **Requêtes HTTP POST** avec **Volley** (`StringRequest`)
- 📌 **Identifiant Android** unique avec `Settings.Secure.ANDROID_ID`
- 📌 **Horodatage** avec `SimpleDateFormat`
- 📌 **Configuration réseau** avec `network_security_config.xml`

---

## 🔄 Fonctionnement

1. L'application démarre → `MainActivity` vérifie si la permission GPS est accordée
2. **Si non accordée** → popup de demande de permission → réponse dans `onRequestPermissionsResult()`
3. **Si accordée** → `demarrerLocalisation()` enregistre un `LocationListener` via `LocationManager`
4. À chaque changement de position → `onLocationChanged()` récupère lat, lon, alt, précision
5. Les coordonnées s'affichent dans le `TextView` + Toast à l'écran
6. `addPosition()` envoie un **POST HTTP** via Volley avec lat, lon, date et `ANDROID_ID`
7. Le serveur PHP insère la position en base et retourne une confirmation

---

## 🔗 Analogie Architecture Android ↔ Web

| Composant Android | Équivalent Web |
|---|---|
| `LocationManager` | API Geolocation du navigateur (`navigator.geolocation`) |
| `LocationListener` | Callback `watchPosition()` en JavaScript |
| `onLocationChanged()` | `position => { ... }` (handler de position) |
| `onRequestPermissionsResult()` | Prompt de permission navigateur |
| `Volley + getParams()` | `fetch()` + `FormData()` JS |
| `ANDROID_ID` | Session token / cookie d'identification |
| `SimpleDateFormat` | `new Date().toISOString()` en JavaScript |
| `network_security_config.xml` | `.htaccess` / CORS config |

---

## 📱 Interface

- **Écran principal** :
  - `TextView` affichant en temps réel :
    - Latitude
    - Longitude
    - Altitude
    - Précision (en mètres)
  - Toast de confirmation à chaque envoi au serveur

---

## 🔧 Configuration requise

> Le serveur PHP doit tourner sur la machine hôte.
> Depuis l'émulateur Android, `10.0.2.2` pointe automatiquement vers `localhost` (127.0.0.1) de votre PC.

```
URL du web service : http://10.0.2.2/localisation/createPosition.php
Méthode            : POST
Paramètres         : latitude, longitude, date_position, imei (ANDROID_ID)
Réponse attendue   : Confirmation texte du serveur PHP
```

---

## 📱 Demo:

https://github.com/user-attachments/assets/0fa0d92f-6878-47b0-8163-3c7eb1798b6e

---

## 🎯 Objectif pédagogique

Ce laboratoire démontre comment utiliser les capteurs Android pour collecter et transmettre des données en temps réel :

- La gestion des **permissions dangereuses** à l'exécution sur Android 6+
- L'utilisation de **`LocationManager`** pour écouter les mises à jour GPS
- L'envoi périodique de données géographiques vers un **back-end PHP**
- La différence entre `ACCESS_FINE_LOCATION` (GPS précis) et `ACCESS_COARSE_LOCATION` (réseau)
- L'utilisation de **`ANDROID_ID`** comme identifiant unique compatible Android 10+

---

## 👨‍💻 Auteur

**Mourad EL OUATIK** | Réalisé dans le cadre du **Lab 10 Android** | Programmation & Sécurité des Applications Mobile
