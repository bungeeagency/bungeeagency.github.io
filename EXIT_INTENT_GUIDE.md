# 🎯 Guide des Exit-Intent Popups

## 📊 Vue d'ensemble

Les exit-intent popups détectent quand un visiteur s'apprête à quitter votre site et affichent une offre de dernière chance pour le retenir. C'est une technique prouvée pour récupérer **15-20% des visiteurs** qui auraient quitté sans conversion.

## ✨ Fonctionnalités implémentées

### 1. Détection intelligente
- ✅ **Exit intent** : Détecte quand la souris quitte la fenêtre vers le haut
- ✅ **Time-based** : Affiche après 45 secondes si l'utilisateur a scrollé 50%+
- ✅ **Non-invasif** : S'affiche maximum 1 fois par visite
- ✅ **Cookie persistence** : Ne ré-affiche pas pendant 7 jours

### 2. Design moderne (shadcn)
- 🎨 Design cohérent avec le reste du site
- ✨ Animations fluides et professionnelles
- 📱 100% responsive (mobile + desktop)
- 🌈 Icône gradient avec effet pulse

### 3. Offre attractive
- 🎁 **Consultation gratuite de 15 minutes**
- ✅ 3 bénéfices clairement listés
- 📞 2 CTA : Cal.com booking + WhatsApp
- 👥 Preuve sociale en bas

### 4. Tracking intégré
- 📊 Google Analytics events automatiques
- 📈 Track : affichage, fermeture, conversions

## 🎨 Personnalisation

### Changer l'offre principale

Dans `index.html`, ligne ~1690 :

```html
<h4 class="exit-popup-offer-title">
    Consultation gratuite de 15 minutes
</h4>
<p class="exit-popup-offer-desc">
    Discutons de votre projet sans engagement...
</p>
```

**Exemples d'offres alternatives :**
- "Premier mois à -50%" (pour SaaS)
- "Devis gratuit en 24h"
- "Guide gratuit : 10 erreurs à éviter"
- "Audit SEO offert"

### Modifier les déclencheurs

Dans `index.html`, ligne ~2314 :

```javascript
// Délai avant affichage (actuellement 45 secondes)
if (timeOnPage >= 45000) {  // Changez cette valeur

// Pourcentage de scroll requis (actuellement 50%)
if (scrollPercentage >= 50) {  // Changez cette valeur
```

**Recommandations :**
- **Sites e-commerce** : 30 secondes, 30% scroll
- **Blog / Contenu** : 60 secondes, 70% scroll
- **Landing page** : 20 secondes, 40% scroll
- **SaaS** : 45 secondes, 50% scroll (actuel)

### Changer la durée du cookie

Ligne ~2248 :

```javascript
expiryDate.setDate(expiryDate.getDate() + 7); // 7 jours
```

Changez en :
- `+ 1` : 1 jour (plus agressif)
- `+ 14` : 2 semaines
- `+ 30` : 1 mois (moins agressif)

### Personnaliser les couleurs

Dans `styles.css`, ligne ~1294 :

```css
.exit-popup-badge {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

Changez par vos couleurs de marque :
```css
background: linear-gradient(135deg, #votre-couleur-1 0%, #votre-couleur-2 100%);
```

## 📈 Optimisation des conversions

### A/B Testing recommandé

Testez différentes variantes :

**Variante 1 : Urgence**
```html
<h3>⏰ Dernière chance !</h3>
<p>Offre limitée : seulement 3 places disponibles ce mois</p>
```

**Variante 2 : Valeur**
```html
<h3>🎁 Cadeau exclusif</h3>
<p>Recevez notre guide gratuit avant de partir</p>
```

**Variante 3 : FOMO (Fear of Missing Out)**
```html
<h3>🚀 Rejoignez 50+ entreprises</h3>
<p>Qui ont déjà transformé leur présence digitale</p>
```

### Meilleures pratiques

1. **Titre accrocheur** : Utilisez des emojis et un message fort
2. **Offre claire** : Valeur évidente en 3 secondes
3. **CTA visible** : Boutons contrastés et explicites
4. **Preuve sociale** : Stats, témoignages, logos clients
5. **Exit facile** : Toujours permettre de fermer facilement

## 📊 Métriques à suivre

Dans Google Analytics, vous pouvez tracker :

```javascript
// Événements automatiquement trackés :
- exit_intent_shown       // Nombre d'affichages
- exit_popup_book_call    // Clics sur "Réserver"
- exit_popup_whatsapp     // Clics sur WhatsApp
```

### Calcul du taux de conversion

```
Taux de conversion = (Conversions depuis popup) / (Affichages popup) × 100
```

**Benchmarks :**
- ❌ Mauvais : < 5%
- ✅ Bon : 10-15%
- 🚀 Excellent : > 20%

## 🔧 Configuration avancée

### Désactiver sur mobile

Si vous voulez désactiver sur mobile (ligne ~2297) :

```javascript
// Detect exit intent
if (window.innerWidth > 768) {  // Ajoutez cette condition
    document.addEventListener('mouseleave', (e) => {
        // ... code existant
    });
}
```

### Afficher seulement sur certaines pages

```javascript
function showExitPopup() {
    // N'afficher que sur la homepage
    if (window.location.pathname !== '/') return;
    
    if (!exitIntentShown && !hasExitPopupBeenShown()) {
        // ... code existant
    }
}
```

### Ajouter un compte à rebours

Dans le HTML du popup :

```html
<div class="exit-popup-countdown">
    <i class="fas fa-clock mr-2"></i>
    Offre valable encore <span id="countdown">10:00</span> minutes
</div>
```

Puis en JavaScript :

```javascript
let countdown = 600; // 10 minutes en secondes
setInterval(() => {
    countdown--;
    const minutes = Math.floor(countdown / 60);
    const seconds = countdown % 60;
    document.getElementById('countdown').textContent = 
        `${minutes}:${seconds.toString().padStart(2, '0')}`;
}, 1000);
```

## 🎯 Templates d'offres

### Pour agence web

```
✅ Audit gratuit de votre site actuel
✅ Recommandations d'amélioration
✅ Devis personnalisé sans engagement
```

### Pour SaaS

```
✅ Essai gratuit de 14 jours
✅ Onboarding personnalisé
✅ Support premium inclus
```

### Pour e-commerce

```
✅ -10% sur votre première commande
✅ Livraison gratuite
✅ Garantie satisfait ou remboursé
```

### Pour consultant

```
✅ Session découverte de 30 min offerte
✅ Analyse de votre situation
✅ Plan d'action personnalisé
```

## 🚫 Erreurs à éviter

1. ❌ **Trop intrusif** : Ne pas bloquer l'écran complètement
2. ❌ **Trop fréquent** : Respecter le cookie (minimum 24h)
3. ❌ **Offre faible** : Proposer une vraie valeur
4. ❌ **Trop de champs** : Maximum 2-3 actions possibles
5. ❌ **Design incohérent** : Garder le style du site

## 📱 Test mobile

Sur mobile, l'exit-intent classique ne fonctionne pas (pas de souris). À la place :
- ✅ Time-based trigger (45s + scroll)
- ✅ Scroll-based (quand remonte en haut de page)

## 🔒 Conformité RGPD

L'exit-intent popup utilise uniquement un cookie technique (non-tracking). Pas besoin de consentement spécifique, mais :

1. Mentionnez-le dans votre politique de cookies
2. Permettez toujours de fermer facilement
3. Ne forcez pas l'email si pas nécessaire

## 📞 Support

Besoin d'aide pour personnaliser votre exit-intent popup ?
- 📧 Email : contact@agencebungee.fr
- 💬 WhatsApp : 06 95 11 92 97

---

**Pro tip :** Testez différentes offres et mesurez ce qui convertit le mieux pour votre audience ! 🚀

