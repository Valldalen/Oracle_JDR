# ORACLE — Moteur de Jeu de Rôle Narratif Local
 
> Un moteur de jeu de rôle solo propulsé par un modèle de langage local via Ollama. Aucune connexion internet requise pour jouer — tout tourne sur votre machine.
 
![ORACLE Screenshot](https://via.placeholder.com/800x400/0d0b08/c8955a?text=ORACLE+%E2%80%94+RPG+Local)
 
---
 
## Prérequis
 
### 1. Installer Ollama
 
Téléchargez et installez Ollama depuis le site officiel :
 
**[https://ollama.com/download](https://ollama.com/download)**
 
Ollama est disponible sur Windows, macOS et Linux.
 
---
 
### 2. Télécharger le modèle recommandé
 
ORACLE est optimisé pour **Gemma 4** de Google. C'est le modèle recommandé pour la qualité narrative et la cohérence de la narration.
 
```bash
ollama pull gemma4
```
 
> D'autres modèles fonctionnent également (Llama 3, Mistral, Dolphin…). Vous pouvez les sélectionner dans l'interface au démarrage.
 
---
 
### 3. Lancer Ollama avec les autorisations CORS
 
> ⚠️ **Étape obligatoire** — sans cette commande, l'application ne peut pas communiquer avec Ollama depuis un fichier HTML local.
 
**Windows (PowerShell) :**
```powershell
$env:OLLAMA_ORIGINS="*"; ollama serve
```
 
**macOS / Linux (Terminal) :**
```bash
OLLAMA_ORIGINS="*" ollama serve
```
 
Laissez ce terminal ouvert pendant toute la session de jeu.
 
> **Astuce Windows** — pour ne plus avoir à le faire à chaque fois, définissez la variable de façon permanente :
> ```powershell
> [System.Environment]::SetEnvironmentVariable("OLLAMA_ORIGINS", "*", "User")
> ```
> Redémarrez ensuite Ollama normalement depuis le menu démarrer.
 
---
 
## Installation & Lancement
 
ORACLE est un **fichier HTML unique** — aucune installation, aucun serveur, aucune dépendance npm.
 
1. Téléchargez le fichier `rpg_ollama.html`
2. Ouvrez-le dans votre navigateur (double-clic ou glisser-déposer)
3. C'est tout
 
> **Navigateur recommandé** : Chrome ou Edge (meilleur support de l'export PDF et de l'API YouTube IFrame).
 
---
 
## Fonctionnalités
 
### 🎭 Configuration de la partie
 
| Fonctionnalité | Description |
|---|---|
| **Genres narratifs** | 8 genres prédéfinis (Horreur, Fantasy, Sci-Fi, Polar, Lovecraft, Post-Apo, Western, Libre) |
| **Mode Solo / Duo** | Jouez seul ou à deux personnages simultanément |
| **Style du MJ** | Bienveillant, Impartial ou Impitoyable |
| **Difficulté** | Narratif (sans échecs durs), Standard, Hardcore (mort possible) |
| **Ton narratif** | Slider de "Descriptif / poétique" à "Rythmé / tendu" |
| **Style d'écriture** | 7 styles prédéfinis (Classique, Poétique, Poe, Camus, Conte oral, Journalistique, Pulp) + champ libre |
| **Police** | 6 combinaisons typographiques (Gothique, Garamond, Playfair, Spectral, Fraktur, Machine à écrire) |
| **Contexte de départ** | Champ optionnel pour orienter l'ouverture de l'histoire |
| **Modèle Ollama** | Sélection automatique des modèles disponibles, température réglable |
 
### ⚔️ Gameplay
 
| Fonctionnalité | Description |
|---|---|
| **Jets de dés D20** | Automatiques avant chaque action, résultat intégré dans la narration |
| **Suggestions d'actions** | 3 actions cliquables générées après chaque réponse du MJ |
| **Mémoire longue** | Compression automatique de l'historique après 10 échanges pour garder la cohérence |
| **Mort du personnage** | En mode Hardcore, le personnage peut mourir définitivement |
 
### 📖 Narration
 
| Fonctionnalité | Description |
|---|---|
| **Arc narratif secret** | Le MJ conçoit une fin dès le début et y amène progressivement le joueur |
| **Phases narratives** | Exposition → Tension → Climax → Dénouement, détectées automatiquement |
| **Timeline visuelle** | Barre de progression de l'arc narratif en haut de l'écran |
| **Jauge de tension** | Indicateur visuel qui évolue avec les phases |
| **Chapitres automatiques** | Titres générés par le modèle, séparateurs visuels dans le fil narratif |
 
### 📒 Journal de bord
 
Panneau latéral rétractable avec 5 onglets :
 
- **Lieux** — tous les lieux découverts, avec résumé de session
- **PNJ** — personnages rencontrés avec leur attitude (ami / neutre / hostile)
- **Objets** — objets et indices collectés
- **Dés** — historique complet de tous les jets de la session
- **Chap.** — liste des chapitres avec titres et numéros de tour
 
### 👤 Fiche de personnage
 
Panneau dédié généré automatiquement par le modèle au démarrage : description narrative et 4 stats évolutives (Courage, Discrétion, Intuition, Charme — adaptées au genre).
 
### 💾 Sauvegarde & Export
 
| Fonctionnalité | Description |
|---|---|
| **Sauvegarde localStorage** | Sessions stockées dans le navigateur, liste visible dès l'écran d'accueil |
| **Export JSON** | Fichier de sauvegarde téléchargé automatiquement à chaque sauvegarde (persiste après fermeture) |
| **Chargement JSON** | Reprise d'une session depuis un fichier, accessible depuis l'écran d'accueil et en cours de partie |
| **Export HTML** | L'aventure exportée en roman HTML mis en page, téléchargeable |
| **Export PDF** | Impression en PDF via la boîte de dialogue du navigateur, avec pied de page "ORACLE — Jeu de Rôle Narratif" |
 
### 🎨 Interface
 
| Fonctionnalité | Description |
|---|---|
| **Thème clair / sombre** | Basculement en un clic, mémorisé entre les sessions |
| **Streaming en temps réel** | Les réponses s'affichent mot par mot avec curseur animé |
| **Mode duo** | Deux champs de saisie distincts, jets de dés indépendants |
 
---
 
## Architecture technique
 
ORACLE est un **fichier HTML autonome** (~85 Ko) sans dépendances externes côté serveur.
 
- **Frontend** : HTML5 / CSS3 / JavaScript vanilla (ES2022)
- **Polices** : Google Fonts (chargées dynamiquement selon la sélection)
- **IA** : API REST Ollama (`http://localhost:11434/api/chat`) en streaming
- **Persistance** : `localStorage` + export/import JSON
- **PDF** : `window.print()` avec CSS `@media print` et règles `@page`
 
### Flux de communication
 
```
Navigateur (rpg_ollama.html)
        │
        │  POST /api/chat (streaming NDJSON)
        ▼
Ollama (localhost:11434)
        │
        │  Inférence locale
        ▼
Modèle (gemma4 ou autre)
```
 
### Structure des métadonnées
 
À chaque réponse, le MJ émet un bloc JSON sur la dernière ligne pour alimenter le journal, la timeline et les chapitres :
 
```json
{"m":{"phase":"exposition","lieux":["La Forêt Noire"],"pnj":[{"nom":"Elara","attitude":"ami","derniere":"nous a guidés"}],"objets":["Vieille clé rouillée"],"mort":false}}
```
 
---
 
## Résolution de problèmes
 
### "Impossible de joindre Ollama"
 
1. Vérifiez qu'Ollama est lancé avec `OLLAMA_ORIGINS="*"` (voir section Prérequis)
2. Vérifiez que le port 11434 n'est pas bloqué par un pare-feu
3. Sur Windows, vérifiez que Ollama n'est pas déjà lancé en tâche de fond sans la variable d'environnement
 
### "Fichier de sauvegarde corrompu"
 
- Utilisez toujours les fichiers `.json` téléchargés par le bouton SAUVER
- Le `localStorage` est effacé si vous videz le cache du navigateur — préférez les fichiers JSON pour les sauvegardes importantes
 
### "Le modèle ne répond pas en français"
 
Certains modèles plus légers ont du mal à maintenir le français sur de longues sessions. Gemma 4 est recommandé pour sa maîtrise du français. Vous pouvez aussi essayer `mistral` ou `llama3.1`.
 
### "L'export PDF affiche 'about:blank' en pied de page"
 
Ce comportement dépend du navigateur. Chrome et Edge affichent correctement "ORACLE — Jeu de Rôle Narratif". Sur Firefox, le pied de page HTML de bas de document est toujours visible.
 
---
 
## Modèles testés
 
| Modèle | Qualité narrative | Vitesse | Français | Notes |
|---|---|---|---|---|
| `gemma4` ⭐ | Excellente | Moyenne | Excellent | Recommandé |
| `llama3.1:8b` | Bonne | Rapide | Bon | Bon compromis |
| `mistral` | Bonne | Rapide | Très bon | Solide |
| `dolphin3` | Très bonne | Moyenne | Bon | Moins censuré |
| `gemma2:27b` | Très bonne | Lente | Excellent | Si vous avez la RAM |
 
---
 
 
## Remerciements
 
- [Ollama](https://ollama.com) pour le moteur d'inférence local
- [Google Gemma](https://ai.google.dev/gemma) pour le modèle recommandé
- Les polices [Google Fonts](https://fonts.google.com) : Cinzel, IM Fell English, Cormorant Garamond, Playfair Display, Spectral, UnifrakturMaguntia, Special Elite
 
---
 
*ORACLE — Toutes vos aventures restent sur votre machine.*
