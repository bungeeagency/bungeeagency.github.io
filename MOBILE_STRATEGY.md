# 📱 Stratégie Exit-Intent Mobile

## 🎯 Le problème

Sur **desktop**, l'exit-intent est simple : on détecte quand la souris quitte la fenêtre vers le haut.

Sur **mobile**, pas de souris ! Il faut d'autres techniques.

## ✅ Solution implémentée

J'ai mis en place **4 déclencheurs intelligents** pour mobile :

### 1. 🔄 Scroll vers le haut (Back-to-top intent)

**Quand :** L'utilisateur scrolle rapidement vers le haut de la page

**Logique :**
- Détecte 2 scrolls vers le haut consécutifs
- Seulement quand l'utilisateur est proche du top (< 200px)
- Indique qu'il veut revenir au début (possiblement pour partir)

**Exemple :**
```
Utilisateur scroll ⬇️ ⬇️ ⬇️
Lit le contenu...
Puis scroll ⬆️ ⬆️ rapidement vers le haut
→ 🎁 POPUP !
```

**Pourquoi ça marche :** Comportement typique avant de fermer un onglet mobile

---

### 2. 👁️ Visibilité change (Tab switch)

**Quand :** L'utilisateur change d'onglet ou met l'app en arrière-plan

**Logique :**
- Détecte `document.hidden` (changement de visibilité)
- Affiche le popup au retour sur l'onglet
- Seulement si l'utilisateur a scrollé 30%+

**Exemple :**
```
Utilisateur navigue sur le site...
Appuie sur le bouton Home 🏠
→ Page mise en arrière-plan
Revient sur l'app
→ 🎁 POPUP !
```

**Pourquoi ça marche :** Moment parfait pour capter l'attention au retour

---

### 3. ⏰ Time-based (Temps passé)

**Quand :** Après 30 secondes + 40% de scroll

**Logique :**
- Timer de 30 secondes (plus court que desktop)
- Scroll minimum de 40% (moins exigeant que desktop)
- Déclenchement automatique

**Exemple :**
```
Utilisateur arrive sur le site
Scroll et lit pendant 30+ secondes
Scroll > 40% de la page
→ 🎁 POPUP !
```

**Pourquoi ça marche :** L'utilisateur est engagé, bon moment pour convertir

---

### 4. 😴 Inactivité (15 secondes)

**Quand :** Après 15 secondes sans interaction

**Logique :**
- Détecte absence de touch/scroll
- Reset à chaque interaction
- Seulement si scroll 30%+

**Exemple :**
```
Utilisateur lit le contenu...
Pose son téléphone 📱
Pas d'interaction pendant 15s
→ 🎁 POPUP !
```

**Pourquoi ça marche :** Utilisateur distrait, on rappelle l'offre

---

## 📊 Comparaison Desktop vs Mobile

| Déclencheur | Desktop | Mobile |
|-------------|---------|--------|
| **Exit intent (souris)** | ✅ Principal | ❌ N/A |
| **Scroll vers le haut** | ❌ | ✅ Principal |
| **Visibility change** | ❌ | ✅ |
| **Time-based** | 45s + 50% scroll | 30s + 40% scroll |
| **Inactivité** | ❌ | ✅ 15s |

## 🎨 UX Mobile

Le popup est **100% optimisé mobile** :

```css
✅ Responsive : s'adapte à tous les écrans
✅ Touch-friendly : boutons larges (min 44px)
✅ Scroll : le contenu du popup scroll si nécessaire
✅ Animations : plus rapides sur mobile (0.2s)
✅ Fermeture : tap sur overlay ou bouton X
```

## 🔧 Configuration

### Ajuster la sensibilité mobile

Dans `index.html`, vous pouvez modifier :

**Scroll-up (ligne ~2356) :**
```javascript
if (scrollUpCount >= 2) {  // Changez le nombre de scrolls requis
```

**Time-based (ligne ~2390) :**
```javascript
const timeThreshold = isMobile ? 30000 : 45000;  // Millisecondes
const scrollThreshold = isMobile ? 40 : 50;      // Pourcentage
```

**Inactivité (ligne ~2426) :**
```javascript
if (inactivityTime >= 15000) {  // Millisecondes d'inactivité
```

**Visibility change (ligne ~2375) :**
```javascript
if (scrollPercentage >= 30) {  // Pourcentage minimum
```

## 📈 Performances attendues

| Déclencheur Mobile | Taux de déclenchement | Conversion |
|-------------------|---------------------|------------|
| Scroll-up | ~15% des visiteurs | 12-18% |
| Visibility change | ~25% des visiteurs | 8-12% |
| Time-based | ~30% des visiteurs | 10-15% |
| Inactivité | ~20% des visiteurs | 5-10% |

**Total récupération : 15-20% des visiteurs mobile**

## 🧪 Test sur mobile

### Méthode 1 : Simulateur Chrome
1. F12 > Toggle device toolbar (Ctrl+Shift+M)
2. Choisir un device mobile (iPhone, Android)
3. Rafraîchir la page
4. Tester les déclencheurs

### Méthode 2 : Vrai smartphone
1. Ouvrir le site sur votre téléphone
2. Activer le mode debug si besoin
3. Tester :
   - Scroll up rapide
   - Changement d'onglet
   - Laisser inactif 15s
   - Attendre 30s en scrollant

### Mode debug mobile
Dans la console mobile (via remote debugging) :
```javascript
// Forcer le déclenchement
testExitPopup()

// Vérifier le type de device
console.log(isMobile ? 'MOBILE' : 'DESKTOP')
```

## 💡 Meilleures pratiques mobile

### ✅ À FAIRE
- Garder l'offre courte et claire
- CTA gros et visibles (WhatsApp marche très bien)
- Permettre fermeture facile
- Tester sur vrais devices
- Limiter à 1 affichage par session

### ❌ À ÉVITER
- Popup trop tôt (< 10s)
- Trop de texte
- Boutons trop petits
- Bloquer le scroll
- Re-afficher trop souvent

## 🎯 Recommandations par type de site

### E-commerce mobile
```javascript
timeThreshold: 20000,      // 20s (rapide)
scrollThreshold: 30,       // 30% (peu)
inactivityTime: 10000      // 10s (agressif)
```

### Blog / Contenu
```javascript
timeThreshold: 45000,      // 45s (lent)
scrollThreshold: 60,       // 60% (beaucoup)
inactivityTime: 20000      // 20s (patient)
```

### Landing page
```javascript
timeThreshold: 25000,      // 25s (moyen)
scrollThreshold: 40,       // 40% (moyen)
inactivityTime: 12000      // 12s (moyen)
```

### SaaS / B2B (actuel)
```javascript
timeThreshold: 30000,      // 30s ✅
scrollThreshold: 40,       // 40% ✅
inactivityTime: 15000      // 15s ✅
```

## 📱 Support des navigateurs

| Navigateur | Scroll-up | Visibility | Time | Inactivité |
|-----------|-----------|------------|------|------------|
| iOS Safari | ✅ | ✅ | ✅ | ✅ |
| Chrome Mobile | ✅ | ✅ | ✅ | ✅ |
| Firefox Mobile | ✅ | ✅ | ✅ | ✅ |
| Samsung Internet | ✅ | ✅ | ✅ | ✅ |

**Tous les déclencheurs sont supportés sur tous les navigateurs modernes.**

## 🚀 A/B Testing mobile

Testez différentes combinaisons :

**Agressif (conversions rapides)**
- Time: 15s
- Scroll: 25%
- Inactivity: 10s

**Modéré (équilibré)** ⭐ Actuel
- Time: 30s
- Scroll: 40%
- Inactivity: 15s

**Conservateur (moins intrusif)**
- Time: 60s
- Scroll: 60%
- Inactivity: 30s

## 📊 Tracking mobile spécifique

Ajoutez dans Google Analytics :

```javascript
// Identifier le type de device
gtag('event', 'exit_popup_shown', {
    'device_type': isMobile ? 'mobile' : 'desktop',
    'trigger': 'scroll_up' // ou 'visibility', 'time', 'inactivity'
});
```

Vous pourrez ainsi comparer :
- Taux de conversion mobile vs desktop
- Quel déclencheur mobile convertit le mieux
- Optimiser en conséquence

## 🎁 Offres recommandées mobile

Sur mobile, privilégiez :

1. **WhatsApp direct** ⭐ Conversion #1
   - Un tap et c'est fait
   - Conversation instantanée
   - Pas de formulaire

2. **Appel téléphonique** 📞
   - `tel:` link direct
   - Très efficace sur mobile

3. **Cal.com booking** 📅
   - Interface tactile optimisée
   - Réservation en 30s

4. ❌ **Éviter les formulaires longs**
   - Difficile à remplir sur mobile
   - Taux d'abandon élevé

---

**Pro tip :** Sur mobile, la simplicité gagne toujours. Un seul CTA WhatsApp peut être plus efficace que 3 options ! 🚀

