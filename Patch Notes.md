1.2 à venir

1.Intelligence artificielle résolvant le 2048, assigné à la touche "5" du pavé numérique.

1.1 Notes de mise à jour 19/01/2018

1.Création d'un retour en arrière jusqu'au début du jeu, considérer comme temporairement cheat, assigné à la touche "4" du pavé numérique.

2.Nouvelle fonction de colorisation intervenant à la fin de chaque action. Suppression des colorisations isolées.

3.Sur ton idée, définition d'un objectif adaptatif à la taille de la grille(4-2048,5-4096,6-8192...), création de la variable WinNumber pour définir l'objectif à atteindre.

4.Création d'une variable TotalCases=grille * grille  pour éviter au programme de le recalculer à chaque appel (#optimisation).

5.Colorisation de tous les nombres >2048 dans la couleur de 2048 (rouge pétant).
