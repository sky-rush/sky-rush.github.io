# SkyRush

**Version:** 2026.01.17.4  
**Créateur:** liveweeeb  
**Plateforme:** Windows (net8.0-windows)  
**Moteur:** Raylib-cs 6.0.0

---

## 📖 Description

SkyRush est un jeu de plateforme 3D en première personne où vous devez sauter de plateforme en plateforme pour augmenter votre score. Plus vous progressez, plus le jeu devient difficile avec des plateformes plus petites, plus éloignées et plus variées.

---

## 🎯 Objectif

Sauter de plateforme en plateforme sans tomber dans le vide. Chaque nouvelle plateforme visitée augmente votre score. Le jeu se termine si vous tombez en dessous de -10 unités.

---

## 🕹️ Contrôles

### Déplacement
- **W / Z** - Avancer
- **S** - Reculer
- **A / Q** - Gauche
- **D** - Droite
- **Souris** - Regarder autour

### Actions
- **Espace** - Sauter
- **Shift Gauche** - Sprint (augmente la vitesse)
- **Ctrl Gauche** - S'accroupir (stabilité sur plateformes glissantes)

### Interface
- **H** - Afficher l'aide
- **ESC** - Pause / Menu
- **F3** - Afficher les informations de debug

---

## 🎨 Types de Plateformes

### 🟠 Plateforme Orange (Normale)
- Plateforme standard
- Stable et sûre
- Couleur: Orange

### 🔵 Plateforme Bleue (Glissante)
- Surface glissante qui fait dériver le joueur
- **Astuce:** Accroupissez-vous (Ctrl) pour rester stable
- Apparaît après score 3
- Probabilité: 10% → 25% max

### 🟤 Plateforme Marron (Mouvante)
- Se déplace entre deux points
- Attention au timing !
- Apparaît après score 5
- Probabilité: 0% → 35% max

### ⚪ Plateforme Grise
- Plateforme déjà visitée
- Ne donne plus de points

---

## 📊 Système de Difficulté Progressive

Le jeu devient progressivement plus difficile en fonction de votre score :

### Distance entre plateformes
- **Début:** 3.5 - 6.0 mètres
- **Maximum:** 5.5 - 8.5 mètres

### Hauteur des sauts
- **Début:** 0.2 - 1.0 mètre
- **Maximum:** 0.8 - 2.0 mètres

### Taille des plateformes
- **Début:** 2.5 - 4.0 unités
- **Minimum:** 1.8 - 3.0 unités

### Plateformes spéciales
- **Glissantes:** 10% → 25% (après score 3)
- **Mouvantes:** 0% → 35% (après score 5)

---

## 🎵 Audio

### Musique
- Musique de fond en boucle
- Volume réglable dans les options
- Contrôle: 0% - 100%

### Effets Sonores
- Son spatial 3D lors de l'atterrissage
- Volume réglable indépendamment
- Pan audio selon la position

---

## ⚙️ Options

### 🎹 Touches
- Configuration complète des touches
- Bouton de réinitialisation aux valeurs par défaut
- Sauvegarde automatique

### 🔊 Volumes
- Volume musique (0% - 100%)
- Volume effets sonores (0% - 100%)
- Sliders interactifs

### 🖥️ Graphisme
- Limite FPS: 30, 60, 120, 144, 240
- Plein écran automatique
- Anti-aliasing MSAA 4x
- VSync activé

---

## 🔄 Système de Mise à Jour

- Vérification automatique au démarrage
- Dialogue de mise à jour obligatoire si nouvelle version disponible
- Téléchargement via navigateur
- URL dynamique depuis GitHub

---

## 🏗️ Architecture Technique

### Structure du Projet
```
SkyRush/
├── Core/              # Système principal
│   ├── Game.cs
│   ├── GameInitializer.cs
│   ├── ConfigManager.cs
│   ├── ResourceLoader.cs
│   └── DiscordRPC.cs
├── Game/              # Logique de jeu
│   ├── GameLogic.cs
│   ├── PlatformSpawner.cs
│   ├── States/        # États du jeu
│   │   ├── GameState.cs
│   │   ├── GameStateUpdater.cs
│   │   ├── OptionsState.cs
│   │   ├── PausedState.cs
│   │   ├── HelpState.cs
│   │   └── GameOverState.cs
│   └── Rendering/     # Rendu
│       ├── GameRenderer.cs
│       ├── UIRenderer.cs
│       └── BackgroundElements.cs
├── Entities/          # Entités
│   ├── Player.cs
│   └── Platform.cs
└── Managers/          # Gestionnaires
    ├── AudioManager.cs
    ├── InputManager.cs
    └── UpdateManager.cs
```

### Technologies
- **Langage:** C# 12
- **Framework:** .NET 8.0
- **Moteur graphique:** Raylib-cs 6.0.0
- **Rendu:** OpenGL via Raylib
- **Audio:** Raylib Audio System

### Fonctionnalités Techniques
- Physique 3D personnalisée
- Caméra première personne
- Son spatial 3D
- Génération procédurale de plateformes
- Système de sauvegarde de configuration
- Assets embarqués dans l'exe
- Extraction automatique des ressources

---

## 💾 Fichiers de Configuration

### Emplacement
`%APPDATA%\SkyRush\`

### Fichiers
- `config.txt` - Configuration générale (FPS, volumes)
- `keys.txt` - Configuration des touches

### Format config.txt
```
fps=60
volume=0.5
sfxVolume=0.7
```

### Format keys.txt
```
W
S
A
D
Space
LeftShift
LeftControl
```

---

## Physique du Joueur

### Vitesse
- **Marche:** 5 unités/s
- **Sprint:** 8 unités/s
- **Accroupi:** 2.5 unités/s

### Saut
- **Force:** 7 unités/s
- **Gravité:** 20 unités/s²
- **Hauteur max:** ~2.5 unités

### Caméra
- **Sensibilité:** 0.2
- **FOV:** 90°
- **Limite verticale:** ±89°

---

## 🌟 Fonctionnalités Spéciales

### Effet de Glissement
- Les plateformes bleues appliquent une force de glissement
- S'accroupir réduit l'effet de 80%
- Force proportionnelle à la vitesse

### Plateformes Mouvantes
- Mouvement sinusoïdal entre deux points
- Distance: 3-5 unités
- Vitesse: 1.5 unités/s
- Le joueur suit le mouvement de la plateforme

### Spawn Intelligent
- Évite les collisions entre plateformes mouvantes
- Distance minimale de sécurité: 4 unités
- Angle de spawn aléatoire (0-360°)

---

## 🐛 Debug

### Mode Debug (F3)
- FPS actuel
- Position du joueur (X, Y, Z)
- Nombre de plateformes actives
- Plateforme la plus proche en surbrillance

### Console
- Logs de démarrage
- Vérification de mise à jour
- Erreurs de spawn

---

## 📦 Distribution

### Fichier Unique
- Tous les assets embarqués dans l'exe
- Extraction automatique au démarrage
- Dossier temporaire: `%TEMP%\SkyRush_Assets\`

### Taille
- Exe: ~2-3 MB
- Assets inclus:
  - back_1.png (écran de chargement)
  - icon.ico (icône de l'application)
  - jump.mp3 (son de saut)
  - musique_1.mp3 (musique de fond)

---

## 🎨 Interface Utilisateur

### Écran de Chargement
- Logo "liveweeeb present"
- Titre "SkyRush"
- Version affichée
- Durée: 5 secondes
- Effet de fade in/out

### Menu Principal
- Fond animé avec hexagones
- Boutons: JOUER, OPTIONS, QUITTER
- Notification de mise à jour si disponible
- Crédits en bas

### HUD en Jeu
- Score en haut à gauche
- Nombre de plateformes
- Viseur central (croix)
- Vignette lors de l'accroupissement
- Aide des contrôles en bas

---

## 🏆 Conseils de Jeu

1. **Regardez toujours la prochaine plateforme** avant de sauter
2. **Utilisez le sprint** pour les sauts longs
3. **Accroupissez-vous** sur les plateformes bleues
4. **Anticipez le mouvement** des plateformes marron
5. **Ne paniquez pas** - prenez votre temps pour viser
6. **Utilisez la hauteur** - sautez depuis le bord pour plus de distance

---

## 📝 Crédits

**Développeur:** liveweeeb  
**Moteur:** Raylib (Ramon Santamaria)  
**Année:** 2026  
**Licence:** © 2026 liveweeeb

---

## 🔗 Liens

- **GitHub:** https://github.com/liveweeeb13/SkyRush
- **Mise à jour:** https://liveweeeb13.github.io/skyrush.txt
- **Support:** Contact via GitHub

---

## 📋 Changelog

### v2026.01.17.4
- Système de mise à jour automatique
- Assets embarqués dans l'exe
- Réorganisation du code
- Options avec 3 catégories
- Amélioration de la difficulté progressive

### Versions précédentes
- v2026.01.17.3 - Optimisations diverses
- v2026.01.17.2 - Ajout des plateformes mouvantes
- v2026.01.17.1 - Version initiale

---

**Bon jeu ! 🚀**
