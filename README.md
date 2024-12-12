## Capteur - Projet IoT embarqué

Ce projet utilise le framework Mbed OS pour le développement d'une application IoT avec la carte ZEST_CORE_FMLR-72. L'application intègre des fonctionnalités de capteur et de communication LoRaWAN, ainsi qu'une visualisation sur le tableau de bord Thingsboard.

## Prérequis

### Matériel requis
- Carte ZEST_CORE_FMLR-72.
- J-Link (EDU Mini ou équivalent) pour le flash.

### Logiciels installés
- Python 3.x (avec pip).
- Mbed CLI.
- GCC ARM Compiler (version compatible).

### Clonage du dépôt

```bash
git clone https://github.com/Spoyty/see_capteurs_pour_lembarque.git
cd see_capteurs_pour_lembarque
```

## Installation des dépendances

### 1. Initialisation du programme Mbed

Cette étape est nécessaire pour s'assurer que le projet est initialisé comme un programme Mbed, ce qui permet de gérer correctement les dépendances et les bibliothèques associées.

```bash
mbed new .
```

### 2. Ajout des bibliothèques nécessaires

Ajoutez les bibliothèques nécessaires pour intégrer les fonctionnalités spécifiques à la carte ZEST_CORE_FMLR-72.

```bash
mbed add https://github.com/catie-aq/mbed_zest-core-fmlr-72
```

### 3. Mise à jour des sous-modules Mbed

Mettez à jour les sous-modules pour télécharger toutes les dépendances et bibliothèques nécessaires au bon fonctionnement du projet.

```bash
mbed deploy
```

### 4. Création et activation d'un environnement virtuel Python

Créez un environnement virtuel pour isoler les dépendances Python, garantissant ainsi une compatibilité entre les différentes versions des bibliothèques utilisées.

```bash
python -m venv mbed_virtual
```

Activez l'environnement virtuel :

```bash
source mbed_virtual/bin/activate
```

## Compilation et flash

### 1. Configurer la cible et l'outil de compilation

Définissez la cible matérielle et la chaîne d'outils de compilation pour garantir que le programme est compilé de manière optimale pour la carte utilisée.

```bash
mbed target ZEST_CORE_FMLR-72
mbed toolchain GCC_ARM
```

### 2. Compiler le programme

Compilez le programme pour générer le fichier binaire qui sera ensuite flashé sur la carte.

```bash
mbed compile
```

Vous obtiendrez un fichier binaire dans le répertoire suivant :

```bash
BUILD/ZEST_CORE_FMLR-72/GCC_ARM/capteur.bin
```

### 3. Flasher le programme

Utilisez J-Link pour flasher l'application sur la carte. Cela permet de transférer le programme compilé vers le matériel.

```bash
sixtron_flash
```

## Capteur - Projet IoT embarqué

Ce projet inclut deux parties principales :
1. **Le projet principal** : intégration complète du capteur de particules avec LoRaWAN et tableau de bord Thingsboard.
2. **Exercices pratiques** : prise en main des fonctionnalités de base de la carte et des bibliothèques utilisées.

### Organisation des fichiers

- `main.cpp` : fichier principal du projet IoT.
- `main.txt` : fichier centralisé contenant tous les exercices. Les utilisateurs peuvent commenter ou décommenter les sections pertinentes pour exécuter un exercice spécifique.

## Nouvelle stratégie pour les exercices

Les exercices pratiques sont désormais centralisés dans le fichier `main.txt`. Cette approche offre plusieurs avantages :

- **Centralisation du code** : Tous les exercices sont regroupés en un seul fichier, ce qui simplifie la navigation.
- **Clarté et pédagogie** : Chaque exercice est isolé dans une section distincte avec des commentaires explicatifs.
- **Facilité d'utilisation** : Il suffit de commenter ou décommenter une section dans `main.txt` pour changer d'exercice sans manipuler plusieurs fichiers ou branches Git.

### Exemple d'utilisation

Pour exécuter un exercice :
1. Ouvrez `main.txt` dans votre éditeur de texte.
2. Commentez toutes les sections sauf celle de l'exercice souhaité.
3. Copiez le code de l'exercice dans `main.cpp`.
4. Compilez et flashez le programme comme indiqué ci-dessus.

Exemple de commande pour compiler et flasher :
```bash
mbed compile && sixtron_flash
```

## Exercices pratiques

Les exercices inclus dans `main.txt` couvrent différentes fonctionnalités :

### Exercice 1 : Contrôle d'une LED avec interruption

Cet exercice utilise la bibliothèque Mbed OS pour contrôler une LED en réponse à un bouton poussoir. Le code utilise des interruptions pour basculer l'état d'une LED à chaque appui ou relâchement du bouton.

#### Fonctionnement

1. **Initialisation des objets :**
   - Un bouton est configuré comme une entrée avec interruptions (`InterruptIn`).
   - Une LED est configurée comme une sortie numérique (`DigitalOut`).

2. **Gestion des interruptions :**
   - Une fonction `flip` bascule l'état de la LED à chaque événement d'interruption.

3. **Boucle principale :**
   - Une boucle infinie maintient le programme actif avec une temporisation de 250 ms.

#### Explications

- L'interruption gère automatiquement les événements du bouton sans bloquer la boucle principale.
- Cette approche permet une réponse rapide et efficace sans nécessiter une surveillance active.

### Exercice 2 : Mesure du temps d'appui sur un bouton

Cet exercice utilise un Timer pour mesurer la durée d'appui sur un bouton et afficher le résultat.

#### Fonctionnement

1. **Initialisation des objets :**
   - Un bouton est configuré avec interruptions (`InterruptIn`).
   - Une LED est utilisée pour indiquer l'état d'appui.
   - Un Timer mesure la durée d'appui.

2. **Gestion des interruptions :**
   - `flip_time` démarre le Timer et change l'état de la LED.
   - `flop_time` arrête le Timer et enregistre la durée.

3. **Affichage des résultats :**
   - La durée est affichée en millisecondes dans la boucle principale.

#### Explications

- Le Timer fournit une mesure précise de la durée d'appui.
- La gestion des interruptions assure une transition fluide entre l'appui et le relâchement du bouton.

### Exercice 3 : Modification de la fréquence de clignotement

Cet exercice utilise un Ticker pour modifier dynamiquement la période de clignotement d'une LED via un bouton.

#### Fonctionnement

1. **Initialisation des objets :**
   - Un bouton configure une interruption pour ajuster la période du Ticker.
   - Une LED est contrôlée par le Ticker.

2. **Gestion des interruptions :**
   - `change_period` ajuste la période du Ticker à chaque appui sur le bouton.

3. **Clignotement de la LED :**
   - Le Ticker bascule l'état de la LED à intervalles définis.

#### Explications

- L'utilisation d'un Ticker simplifie la gestion des intervalles périodiques.
- La fonction `change_period` permet un contrôle interactif et en temps réel.

### Exercice 4 : Gestion de threads avec mutex

Cet exercice implémente un système de "Ping-Pong" entre deux threads en utilisant un Mutex pour synchroniser les accès.

#### Fonctionnement

1. **Initialisation :**
   - Deux threads (`tPing` et `tPong`) alternent leurs tâches.
   - Une LED clignote dans le thread principal pour indiquer l'activité.

2. **Synchronisation :**
   - Un Mutex garantit qu'un seul thread accède à la ressource partagée (la console) à la fois.

3. **Boucle principale :**
   - La LED du thread principal clignote indépendamment des threads "Ping" et "Pong".

#### Explications

- Le Mutex évite les conflits lors de l'accès simultané à la console.
- Cette approche illustre la gestion des ressources partagées dans un environnement multi-threadé.

---

Chaque exercice est décrit avec un code commenté dans `main.txt` et peut être facilement extrait pour être exécuté indépendamment.
