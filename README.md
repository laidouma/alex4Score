# Alex4 - TP

DACLIN Emma - LAIDOUNI Manel - RANTIN Maëna

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



## Etape 3 : Utilisation de scanmem pour le score

Dans `scanmem` :
- On attache le processus :
  ```scanmem
  pid 54226  # Remplacez par le PID d'Alex4
  ```
- Entrez votre score actuel pour affiner la recherche :

  ![image](https://github.com/user-attachments/assets/45d70116-468a-4d92-b322-0903711eae8c)

  On change le score sur alex4 et on relance la recherche.

  ![image](https://github.com/user-attachments/assets/80af02d0-dc93-4ed5-adee-92eaf509860d)

  On obtient une adresse : `0x557a12022c48`
  
![image](https://github.com/user-attachments/assets/2c8c94f7-c030-4237-8a49-51c412662d5b)



## Etape 4 : Injection de Score dans notre code
Fonction modify_memory(process, address, new_value).
