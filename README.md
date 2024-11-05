# Alex4 - TP

## Etape 1 : PID de alex4

![image](https://github.com/user-attachments/assets/18402f68-ddb1-4dc8-94fd-33efc23af4fd)

```bash
pgrep alex4
```
Le PID est le numéro retourné, ici : `54226`.

## Etape 2 : Réalisation du code
**Fonctionnalités**
- La fonction pause_process(pid) attache le débogueur au processus cible et met ce dernier en pause.
- La fonction get_mapping(process) récupère les mappages mémoire du processus, incluant les sections d’adresse de la pile.
- get_stack_mappings(mappings_list) filtre les mappages pour obtenir ceux de la pile, identifiés par le chemin [stack].
- read_stack_content(process, stack_mapping) lit les données de la pile dans une section d’adresse spécifique et les enregistre dans un fichier stack_content.txt.
- modify_memory(process, address, new_value) permet de modifier une valeur en mémoire à une adresse spécifique. Assurez-vous de définir address avec l’adresse mémoire exacte que vous souhaitez modifier et new_value avec la nouvelle valeur.
- La fonction resume_process(debugger, process) relance le processus après modification de la mémoire.


## Etape 3 : 

# Injection de Score pour le Jeu Alex4

Ce projet permet de manipuler et d'injecter un score dans le jeu **Alex4** en utilisant des techniques de manipulation de processus et d'adresses mémoire avec Python, **scanmem**, et **gdb**.

## Fonctionnalités

- **Pause et Reprise du Processus** : Contrôler le processus d'Alex4 avec Python pour observer les effets des modifications de score.
- **Scan de Mémoire** : Identifier les adresses mémoire du score en utilisant **scanmem**.
- **Modification Manuelle du Score** : Changer la valeur de score dans la mémoire en utilisant **gdb**.
- **Enregistrement des Modifications** : Sauvegarder les résultats des manipulations pour analyse.

## Prérequis

- **Python 3**
- **gdb** (GNU Debugger)
- **scanmem**

## Installation

Assurez-vous que tous les outils nécessaires sont installés.

```bash
sudo apt-get install python3 gdb scanmem htop
```

## Étapes d'Utilisation

### 1. Identifier le Processus

Trouvez le PID du processus du jeu Alex4 en utilisant la commande `pgrep`.





### 2. Pause et Reprise du Processus

Utilisez une librairie Python pour mettre le processus en pause et observer ses effets sur le système. Vous pouvez utiliser un script Python similaire à celui-ci pour envoyer des signaux.


### 3. Visualiser les Processus avec htop

Lancez `htop` pour afficher tous les processus et repérez Alex4.

```bash
htop
```

Commandes dans `htop` :
- `F6` : Trier par arbre de processus.
- `F3` : Rechercher un processus spécifique.
- `F9` : Afficher les signaux que vous pouvez envoyer.

### 4. Utiliser scanmem pour le Score

Ouvrez une session `scanmem` et ciblez le processus pour identifier l'adresse mémoire du score.

```bash
sudo scanmem
```

Dans `scanmem` :
- Attachez le processus :
  ```scanmem
  pid 53345  # Remplacez par le PID d'Alex4
  ```
- Entrez votre score actuel pour affiner la recherche :
  ```scanmem
  20  # Exemple de score actuel
  ```
- Changez le score dans le jeu, puis répétez la recherche jusqu'à obtenir une adresse stable.

### 5. Injection de Score avec gdb

Attachez-vous au processus avec **gdb** pour injecter la valeur de score.

```bash
sudo gdb -p 53345
```

Dans `gdb`, une fois attaché :
1. Trouvez l'adresse mémoire du score obtenue avec `scanmem`.
2. Modifiez cette adresse avec la nouvelle valeur :

   ```gdb
   set *(int*)0x[address] = 40  # Remplacez [address] par l'adresse trouvée et 40 par le score souhaité
   ```

3. Quittez gdb avec `detach` puis `quit`.


## Résultats

Les changements de score seront visibles dans le jeu en temps réel.

---
