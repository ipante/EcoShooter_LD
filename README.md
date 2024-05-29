# EcoShooter

## Issues 
Problème en lien avec la fonction spawnTrash (présente dans chacun des niveaux), le loop écrit tout de suite après et qui contient la variable offscreenTrashCount, qui est censée compter les objets qui tombent en dehors de l'écran. Dans chaque niveau il y a un MAX_TRASH qui comptabilisent combien d'objets la fonction spawnTrash doit mettre sur l'écran. 
J'ai créé un div(#game-container), dans lequel je colle toujours un premier canvas (mainCanvas), qui a kaboom et où se déroule le jeu. A chaque niveau je colle un deuxième canvas (secondCanvas) dans le div au début du niveau, et je l'enlève avec removeChild quand il y a un changement de niveau (soit si on passe au niveau d'après, soit si on va au gameOver ou au win). 
Les lignes concernées sont répétées de façon identique à chaque niveau: level0 946-980, level1 1510-1547, level2 2044-2078, level3 2589-2622. 
Je pense qu'il y a une superposition entre ce qui est dans MAX_TRASH et offscreenTrashCount: ceci empêche, dans le cas de gameOver si on laisse passer trop d'objets, le fait que le deuxième écran (avec le paysage qui évolue sur la droite) ne peut pas être removed. 
Le message qui apparait alors en tant qu'erreur sur l'écran est "Error. Node.removeChild: The node to be removed is not a child of this node", et dans la console il y a écrit "DOMException: Node.removeChild: The node to be removed is not a child of this node". Je pense que le problème ne soit pas en lien avec le fait d'enlever ou pas le secondCanvas, car le problème se présente de façon irrégulière, mais avec plus de fréquence si il y a beaucoup de différence de nombre entre MAX_TRASH et offscreenTrashCount. 