# 🐛 Debug Exit-Intent Popup

## ✅ Checklist de diagnostic

### 1. Vérifier que le fichier HTML est à jour
- Ouvrir `index.html`
- Chercher `id="exit-intent-popup"` (devrait être présent)
- Vérifier que `DEBUG_MODE = true` (ligne ~2241)

### 2. Vérifier que le CSS est chargé
- Ouvrir `styles.css`
- Chercher `.exit-popup` (devrait être présent)
- Vérifier les styles d'affichage

### 3. Tester dans le navigateur

**Méthode 1 : Mode Debug automatique**
1. Ouvrir le site
2. Ouvrir la console (F12)
3. Le popup devrait s'afficher après 3 secondes
4. Vérifier les logs dans la console

**Méthode 2 : Test manuel**
1. Ouvrir le site
2. Ouvrir la console (F12)
3. Taper : `testExitPopup()`
4. Appuyer sur Entrée
5. Le popup devrait apparaître immédiatement

**Méthode 3 : Exit intent réel**
1. Désactiver le mode debug (`DEBUG_MODE = false`)
2. Naviguer sur le site
3. Déplacer la souris vers le haut (sortie de la fenêtre)
4. Le popup devrait apparaître

### 4. Vérifier la console

Vous devriez voir :
```
🔧 MODE DEBUG ACTIVÉ - Le popup s'affichera dans 3 secondes
🎯 Tentative d'affichage du popup...
✓ Element popup trouvé: [object HTMLDivElement]
exitIntentShown: false
hasExitPopupBeenShown: false
✅ Affichage du popup !
```

### 5. Problèmes courants

**Le popup ne s'affiche pas du tout**
- ✅ Vérifier que `DEBUG_MODE = true`
- ✅ Vider le cache du navigateur (Ctrl+Shift+R)
- ✅ Vérifier qu'il n'y a pas d'erreurs JavaScript dans la console

**Le popup s'affiche mais disparaît**
- ✅ Vérifier les styles CSS (`.exit-popup.active`)
- ✅ Vérifier le z-index (devrait être 9999)
- ✅ Vérifier que `opacity` passe bien à 1

**Le popup est invisible**
- ✅ Inspecter l'élément (F12 > Elements)
- ✅ Vérifier que `display: none` n'est pas appliqué
- ✅ Vérifier que `opacity: 0` n'est pas forcé

**Les boutons ne fonctionnent pas**
- ✅ Vérifier la console pour les erreurs
- ✅ Vérifier que les fonctions sont bien définies globalement
- ✅ Tester `window.exitPopupBookCall` dans la console

## 🔧 Commandes de debug

Ouvrez la console (F12) et utilisez :

```javascript
// Afficher le popup immédiatement
testExitPopup()

// Fermer le popup
closeExitPopup()

// Vérifier si l'élément existe
document.getElementById('exit-intent-popup')

// Vérifier les classes
document.getElementById('exit-intent-popup').className

// Forcer l'affichage
document.getElementById('exit-intent-popup').classList.add('active')

// Vérifier les styles
getComputedStyle(document.getElementById('exit-intent-popup'))

// Supprimer le cookie (pour retester)
document.cookie = 'exitPopupShown=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;'
```

## 🎯 Test complet étape par étape

### Étape 1 : Vérification de base
```javascript
// Dans la console
console.log('Element:', document.getElementById('exit-intent-popup'));
console.log('Classes:', document.getElementById('exit-intent-popup')?.className);
console.log('Style display:', getComputedStyle(document.getElementById('exit-intent-popup')).display);
console.log('Style opacity:', getComputedStyle(document.getElementById('exit-intent-popup')).opacity);
```

### Étape 2 : Test d'affichage manuel
```javascript
// Dans la console
const popup = document.getElementById('exit-intent-popup');
popup.classList.add('active');
console.log('Classes après ajout:', popup.className);
console.log('Opacity après ajout:', getComputedStyle(popup).opacity);
```

### Étape 3 : Vérifier le CSS
```css
/* Devrait être dans styles.css */
.exit-popup {
    opacity: 0;
    pointer-events: none;
}

.exit-popup.active {
    opacity: 1;
    pointer-events: all;
}
```

## 🚀 Solution rapide

Si rien ne fonctionne, essayez cette solution d'urgence :

**Dans la console du navigateur :**
```javascript
// 1. Forcer l'affichage
const popup = document.getElementById('exit-intent-popup');
if (popup) {
    popup.style.display = 'flex';
    popup.style.opacity = '1';
    popup.style.pointerEvents = 'all';
    popup.style.zIndex = '9999';
    console.log('✅ Popup forcé à s\'afficher');
} else {
    console.error('❌ Popup introuvable');
}
```

## 📝 Informations système

Pour un diagnostic complet, fournissez :
- Navigateur : Chrome / Firefox / Safari / Edge + version
- Système : Windows / Mac / Linux
- Messages d'erreur dans la console
- Screenshot de l'inspecteur (élément #exit-intent-popup)

## 🔍 Vérification des fichiers

**index.html** devrait contenir :
- Ligne ~1663 : `<div id="exit-intent-popup" class="exit-popup">`
- Ligne ~2241 : `const DEBUG_MODE = true;`
- Ligne ~2238 : `const exitPopup = document.getElementById('exit-intent-popup');`

**styles.css** devrait contenir :
- Ligne ~1188 : `.exit-popup {`
- Ligne ~1201 : `.exit-popup.active {`

## ⚡ Mode Debug permanent

Pour laisser le mode debug activé :
1. Garder `DEBUG_MODE = true`
2. Le popup s'affichera toujours après 3 secondes
3. Pas de cookie enregistré
4. Logs détaillés dans la console

Pour désactiver en production :
1. Changer `DEBUG_MODE = false` (ligne ~2241)
2. Le popup fonctionnera normalement
3. Cookie de 7 jours activé
4. Déclenchement sur exit intent

## 📞 Support

Si le problème persiste :
1. Copier tous les messages de la console
2. Faire un screenshot de l'inspecteur
3. Me les envoyer avec :
   - Navigateur utilisé
   - Étapes suivies
   - Comportement observé

---

**Note :** Avec `DEBUG_MODE = true`, le popup devrait s'afficher automatiquement 3 secondes après le chargement de la page, même sans action de votre part.

