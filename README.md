# 📦 ACIT ThermACEC - Repo OTA

Dépôt de distribution des firmwares OTA (Over-The-Air) pour le projet **ACIT ThermACEC**.

## 📋 Description

Ce repo contient les firmwares compilés et les manifests JSON pour les mises à jour OTA des cartes ESP32-C6 du projet ThermACEC.

## 📁 Structure

```
ACIT_ACCU_ThermACEC_OTA/
├── stable/                          # Channel stable (production)
│   ├── manifest.json                # Manifest JSON avec métadonnées
│   ├── acit_thermacec_vX.Y.Z_YYYYMMDD.bin  # Firmwares
│   └── ...
├── beta/                            # Channel beta (tests) - à venir
│   ├── manifest.json
│   └── ...
└── README.md                        # Ce fichier
```

## 🔧 Channels

### Stable
- **Production** : Releases testées et validées
- **URL manifest** : `https://raw.githubusercontent.com/jdu-acit/ACIT_ACCU_ThermACEC_OTA/main/stable/manifest.json`
- **Utilisation** : Cartes en production

### Beta (à venir)
- **Tests** : Releases en cours de validation
- **URL manifest** : `https://raw.githubusercontent.com/jdu-acit/ACIT_ACCU_ThermACEC_OTA/main/beta/manifest.json`
- **Utilisation** : Cartes de test

## 📄 Format du manifest JSON

```json
{
  \"app\": \"thermacec\",
  \"channel\": \"stable\",
  \"version\": \"X.Y.Z\",
  \"url\": \"https://raw.githubusercontent.com/jdu-acit/ACIT_ACCU_ThermACEC_OTA/main/stable/acit_thermacec_vX.Y.Z_YYYYMMDD.bin\",
  \"size\": 1234567,
  \"sha256\": \"abc123...\",
  \"mandatory\": false,
  \"build_date\": \"YYYYMMDD\",
  \"generated_at\": \"YYYY-MM-DDTHH:MM:SS\"
}
```

## 🚀 Publication d'une nouvelle version

La publication est automatisée via le script Python du repo principal :

```bash
# Dans le repo ACIT_ThermACEC
python tools/build_and_publish.py
```

Le script :
1. 🧹 Nettoie le build
2. 📈 Incrémente la version
3. 🔨 Compile le firmware avec ESP-IDF
4. 📤 Copie le firmware vers ce repo OTA
5. 📝 Génère le manifest.json
6. 📌 Commit et push automatique

## 🔐 Sécurité

- ✅ **HTTPS obligatoire** : `raw.githubusercontent.com`
- ✅ **SHA256** : Calculé et stocké dans le manifest
- ✅ **Certificats validés** : ESP32 vérifie les certificats
- ✅ **Taille vérifiée** : Avant téléchargement
- ✅ **Repo public** : Pas de token requis

## 📊 Historique des versions

Les firmwares sont conservés dans le repo pour traçabilité. Pas de limite de versions stockées.

## 🔗 Liens

- **Repo principal** : [ACIT_ThermACEC](https://github.com/jdu-acit/ACIT_ThermACEC)
- **Documentation OTA** : Voir `docs/ota/` dans le repo principal
- **Script de publication** : `tools/build_and_publish.py` dans le repo principal

## 📝 Notes

- Les firmwares sont nommés selon le pattern : `acit_thermacec_vX.Y.Z_YYYYMMDD.bin`
- Le manifest est automatiquement mis à jour à chaque publication
- Les cartes ESP32-C6 vérifient automatiquement les mises à jour selon l'intervalle configuré (défaut: 1h)

## 🛠️ Configuration ESP32

Dans le firmware, l'URL du manifest est configurée dans `components/ota_update/Kconfig` :

```
CONFIG_OTA_UPDATE_DEFAULT_URL=\"https://raw.githubusercontent.com/jdu-acit/ACIT_ACCU_ThermACEC_OTA/main/stable/manifest.json\"
```

Cette URL peut être modifiée à runtime via NVS ou l'interface web.

---

**Projet** : ACIT ThermACEC  
**Auteur** : jdu-acit  
**Licence** : Propriétaire
