# 🚀 Relai XHTTP Netlify

> Projet simple de relai avec Netlify Edge Function  
> Créé par **Mirza**

---

## 🇺🇸 Guide en anglais

Version anglaise : [README.md](./README.md)

---

## ⚠️ Avertissement important

Utilisez ce projet uniquement avec votre propre domaine/serveur ou avec une autorisation explicite.

---

## ✨ Fonctionnalités

- Relai via Netlify Edge Function
- Configuration simple
- Compatible avec le site Netlify et Netlify CLI
- Domaine cible défini via une variable d'environnement
- Prise en charge du domaine cible avec port

---

## 📦 Structure du projet

```txt
.
├── netlify/
│   └── edge-functions/
│       └── relay.js
├── public/
│   └── index.html
├── netlify.toml
├── package.json
├── README.md
└── README_FA.md
```

---

## 🍴 Déployer via un Fork de ce dépôt

> Cette méthode fonctionne, mais elle n'est **pas recommandée** pour la plupart des utilisateurs.  
> Méthode recommandée : téléchargez/copiez le projet et déployez votre propre version.

## 🔐 Variable d'environnement requise

Vous devez définir :

```txt
TARGET_DOMAIN=https://votre-domaine.com:443
```

### Important

Le domaine **doit inclure le port**.

Exemples corrects :

```txt
https://example.com:443
https://sub.example.com:443
https://api.example.com:8443
```

Exemples incorrects :

```txt
https://example.com
example.com:443
http://example.com:443
localhost:443
127.0.0.1:443
```

---

## 🚀 Déployer via le site Netlify

Utilisez ce projet directement.

### 1. Importer le projet

Rendez-vous sur Netlify :

```txt
https://app.netlify.com
```

Puis :

```txt
Add new project → Import an existing project
```

Sélectionnez votre dépôt.

---

### 2. Paramètres de build

Utilisez :

| Paramètre | Valeur |
|---|---|
| Build command | `npm run build` |
| Publish directory | `public` |

---

### 3. Ajouter la variable d'environnement

Allez dans :

```txt
Site configuration → Environment variables → Add variable
```

Ajoutez :

```txt
Key: TARGET_DOMAIN
Value: https://votre-domaine.com:443
```

Exemple :

```txt
TARGET_DOMAIN=https://example.com:443
```

---

### 4. Redéployer

Après avoir ajouté `TARGET_DOMAIN`, redéployez :

```txt
Deploys → Trigger deploy → Deploy site
```

---

## 🍴 Déployer via un Fork de ce dépôt

> Cette méthode fonctionne, mais elle n'est **pas recommandée** pour la plupart des utilisateurs.  
> Méthode recommandée : téléchargez/copiez le projet et déployez votre propre version.

### Pourquoi le fork n'est-il pas recommandé ?

- Votre projet reste lié à l'historique du dépôt d'origine
- Les options de fork/mise à jour peuvent perturber les débutants
- Si vous souhaitez un projet personnel propre, copier les fichiers est préférable

### Si vous souhaitez tout de même utiliser le Fork

1. Ouvrez ce projet sur GitHub
2. Cliquez sur **Fork**
3. Choisissez votre compte GitHub
4. Une fois le fork créé, accédez à Netlify
5. Cliquez sur :

```txt
Add new project → Import an existing project → GitHub
```

6. Sélectionnez votre dépôt forké
7. Utilisez ces paramètres de build :

| Paramètre | Valeur |
|---|---|
| Build command | `npm run build` |
| Publish directory | `public` |

8. Ajoutez la variable d'environnement :

```txt
TARGET_DOMAIN=https://votre-domaine.com:443
```

9. Déployez le site

Après chaque modification de `TARGET_DOMAIN`, redéployez toujours.

---

## 💻 Déployer avec Netlify CLI

### 1. Installer Netlify CLI

```bash
npm install -g netlify-cli
```

---

### 2. Aller dans le dossier du projet

```bash
cd chemin/vers/le/projet
```

---

### 3. Se connecter

```bash
netlify login
```

---

### 4. Lier le projet

Si votre site existe déjà sur Netlify :

```bash
netlify link
```

Si vous souhaitez que la CLI crée le site :

```bash
netlify init
```

---

### 5. Définir TARGET_DOMAIN

La valeur doit inclure le port :

```bash
netlify env:set TARGET_DOMAIN "https://votre-domaine.com:443" --scope functions --context production
```

Exemple :

```bash
netlify env:set TARGET_DOMAIN "https://example.com:443" --scope functions --context production
```

---

### 6. Vérifier les variables d'environnement

```bash
netlify env:list
```

ou :

```bash
netlify env:get TARGET_DOMAIN --context production
```

---

### 7. Déployer

```bash
netlify deploy --prod
```

---

## 🧪 Utilisation

| URL ouverte | Redirigée vers |
|---|---|
| `https://votre-site.netlify.app/` | `https://votre-domaine.com:443/` |
| `https://votre-site.netlify.app/path` | `https://votre-domaine.com:443/path` |
| `https://votre-site.netlify.app/api/test` | `https://votre-domaine.com:443/api/test` |

---

## 🔗 Exemple de configuration

Remplacez les espaces réservés par vos propres valeurs.

```txt
vless://UUID@xxxxx=SNi:443?encryption=none&security=tls&sni=xxx&fp=chrome&alpn=h2%2Chttp%2F1.1&insecure=0&allowInsecure=0&type=xhttp&host=VOTRE_DOMAINE_NETLIFY&path=VOTRE_CHEMIN&mode=auto&extra=%7B%22xPaddingBytes%22%3A%22100-1000%22%7D#net
```

### Remplacez ces valeurs

| Espace réservé | Signification |
|---|---|
| `UUID` | Votre UUID |
| `VOTRE_DOMAINE_NETLIFY` | Votre domaine Netlify, par exemple `votre-site.netlify.app` |
| `VOTRE_CHEMIN` | Le chemin de votre backend |

Utilisez ces adresses SNI pour votre configuration :

```txt
kubernetes.io
helm.sh
letsencrypt.org
```

---

## 🐞 Débogage

### Consulter les logs de déploiement

```txt
Site → Deploys → Latest deploy → View logs
```

### Consulter les logs de l'Edge Function

```txt
Site → Edge Functions → relay → Logs
```

### Vérifier les variables d'environnement

```bash
netlify env:list
netlify env:get TARGET_DOMAIN --context production
```

### Tester votre backend

```bash
curl -I "https://votre-domaine.com:443"
```

Si cette commande échoue, corrigez d'abord votre backend, votre domaine ou votre port.

---

## ❌ Erreurs courantes

| Erreur | Cause | Solution |
|---|---|---|
| `dns error` | Le domaine ne se résout pas | Vérifiez le DNS du domaine |
| `connection refused` | Le port est fermé | Ouvrez le port ou utilisez le bon port |
| `SSL/TLS error` | Problème de certificat ou de SNI | Utilisez le bon domaine et un SSL valide |
| Ancienne adresse toujours utilisée | Ancien déploiement/variable d'env | Redéfinissez la variable et redéployez |
| `404` | Problème de route | Vérifiez `netlify.toml` |

---

## ✅ Liste de vérification rapide

- [ ] `TARGET_DOMAIN` est défini
- [ ] `TARGET_DOMAIN` inclut `https://`
- [ ] `TARGET_DOMAIN` inclut le port
- [ ] Le domaine cible est résolvable publiquement
- [ ] Le port cible est ouvert
- [ ] Vous avez redéployé après avoir modifié la variable d'environnement

---

## 💰 Faire un don

https://reymit.ir/amirshaker

Solana :

```txt
E7S8EBUE5tkY5UaTgDvhaanJMeCi2DxPGYZukJGrJV8J
```

---

## 📢 Canal Telegram

```txt
https://t.me/avaco_cloud
```

---

## 💬 Contact

```txt
@ShakerFPS
```

---

## 👤 Auteur

**amirs**

---

## 📜 Licence

MIT License © amirs
