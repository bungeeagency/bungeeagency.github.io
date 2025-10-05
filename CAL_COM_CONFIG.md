# 📅 Configuration Cal.com pour Bungee Agency

## 🚀 Mise en place rapide

### 1. Créez votre compte Cal.com

1. Allez sur [cal.com](https://cal.com) (gratuit)
2. Créez un compte avec votre email professionnel
3. Configurez votre profil (nom, photo, bio)

### 2. Créez un type d'événement

1. Dans Cal.com, cliquez sur "Event Types"
2. Créez un nouvel événement :
   - **Nom** : "Consultation projet web" (ou "30min")
   - **Durée** : 30 minutes
   - **Description** : "Discutons de votre projet digital"
   - **Lien** : Choisissez un slug court (ex: "consultation", "30min", "demo")

### 3. Configurez vos disponibilités

1. Allez dans "Availability"
2. Définissez vos horaires de travail
3. Ajoutez des buffers si nécessaire (temps entre les rendez-vous)

### 4. Intégrez le calendrier

1. Connectez votre Google Calendar / Outlook
2. Testez la synchronisation

### 5. Configurez le site web

**Dans le fichier `index.html`, ligne ~1914, remplacez :**

```javascript
Cal("openModal", {
    calLink: "votre-compte-cal/30min",  // ⚠️ À MODIFIER
    // ...
});
```

**Par votre vrai lien Cal.com :**

```javascript
Cal("openModal", {
    calLink: "agencebungee/consultation",  // ✅ Votre vrai lien
    // ...
});
```

**Formats possibles :**
- `"votre-username/consultation"`
- `"votre-username/30min"`
- `"team/agence-bungee/demo"`

### 6. Testez !

1. Sauvegardez le fichier
2. Rafraîchissez votre site
3. Complétez le quiz jusqu'à l'étape 4
4. Cliquez sur "Réserver un appel"
5. Vérifiez que le modal Cal.com s'ouvre correctement

## 🎨 Personnalisation avancée

### Changer la couleur de branding

Dans `index.html`, ligne ~1906 :

```javascript
Cal("ui", {
    "styles": {"branding": {"brandColor": "#1e293b"}},  // Changez la couleur
    // ...
});
```

### Ajouter des questions personnalisées

Dans Cal.com :
1. Event Types > Votre événement > "Advanced"
2. Ajoutez des "Booking Questions"
3. Exemple : "Quel est votre budget ?" (sera pré-rempli automatiquement)

### Notifications automatiques

1. Allez dans Settings > Notifications
2. Activez les emails de confirmation
3. Personnalisez les templates d'email

## 📊 Suivre vos réservations

- Tableau de bord Cal.com : tous vos RDV
- Intégration Zapier/Make : envoyer vers un CRM
- Webhook : notification Discord quand quelqu'un réserve

## 🔗 Liens utiles

- [Documentation Cal.com](https://cal.com/docs)
- [API Cal.com](https://cal.com/docs/api)
- [Embed Guide](https://cal.com/docs/core-features/embed)

## ❓ Problèmes courants

### Le modal ne s'ouvre pas
- Vérifiez que le script Cal.com est chargé (ligne 1664)
- Vérifiez que votre lien est correct
- Ouvrez la console (F12) pour voir les erreurs

### Les infos ne sont pas pré-remplies
- Vérifiez que les champs `name` et `email` correspondent aux champs Cal.com
- Les notes sont ajoutées automatiquement

### La couleur ne change pas
- Le "brandColor" doit être un hex code valide (#1e293b)
- Videz le cache du navigateur

## 💡 Conseils d'utilisation

1. **Créez plusieurs types d'événements** :
   - 15min : Premier contact rapide
   - 30min : Consultation projet
   - 60min : Analyse approfondie

2. **Configurez des rappels automatiques** :
   - Email 24h avant
   - SMS 1h avant (avec intégrations)

3. **Ajoutez une page de confirmation** :
   - Instructions pour préparer l'appel
   - Lien Zoom/Google Meet automatique

4. **Statistiques** :
   - Taux de réservation
   - Créneaux les plus populaires
   - Taux de no-show

---

**Besoin d'aide ?** Consultez la [documentation officielle Cal.com](https://cal.com/docs)

