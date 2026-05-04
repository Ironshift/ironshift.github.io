---
title: Réducteur Cycloïdal
date: 2025-05-01 00:00:00 +0000
description: Modélisation mécanique et animation 3D d'un réducteur cycloïdal
categories: [CAO disponible, Animation 3D]
tags: []     # TAG names should always be lowercase
math: true
image:
  path: /assets/reducteur_cycloidal/CycloidalDrive01.webp
---

# Objectif

L'objectif de ce projet est la conception complète d'un réducteur cycloïdal, un mécanisme réputé pour son rapport de réduction élevé dans un volume compact et un jeu mécanique (backlash) faible. 

Le projet se décline en trois axes majeurs :

1. Théorie et Modélisation : Définition des équations mathématiques qui régissent les courbes cycloïdales.
2. Animation : Création d'une animation photo-réaliste sous KeyShot.
3. Validation Physique : Passage de la CAO au monde réel avec la fabrication du prototype.

## Théorie et Modélisation

Contrairement aux engrenages classiques, le mouvement repose ici sur un disque aux courbes épi- ou hypocycloïdales roulant à l'intérieur d'un cercle de galets.

Contrairement aux engrenages classiques, la réduction ne repose pas sur des dents qui s'engrènent, mais sur un mouvement d'oscillation contrôlé :

- `Came excentrique` L'arbre d'entrée est muni d'une came excentrique. En tournant, elle ne transmet pas directement une rotation au disque, mais un mouvement d'oscillation circulaire.

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive02.webp)
_Une came excentrique montée sur un moteur pas à pas de taille NEMA 23_

- `Disque cycloïde` Sous l'impulsion de cet excentrique, le disque cycloïdal (pièce bleue) vient rouler à l'intérieur d'un cercle de galets fixes (axes jaunes). À cause de la différence entre le nombres d'axes (31) et le disque cycloïdal (30), ce dernier tourne très lentement sur lui-même dans le sens opposé à l'entrée.

$$
\begin{equation}
X = R \cos(t) - Rr \cos\left(t + \arctan\left({\sin((1-N)t) \over {R \over EN} - \cos((1-N)t)}\right)\right) - E \cos(Nt)
\end{equation}
$$

$$
\begin{equation}
Y = -R \sin(t) + Rr \sin\left(t + \arctan\left({\sin((1-N)t) \over {R \over EN} - \cos((1-N)t)}\right)\right) + E \sin(Nt)
\end{equation}
$$

Dans notre exemple, nous prendrons les paramètres suivants :
- Rayon du cercle primitif (R) : 24,80 mm
- Rayon des galets (Rr​) : 1,50 mm
- Excentricité (E) : 0,75 mm
- Nombre de galets (N) : 31

Le rapport de réduction avec ces paramétres sera de N-1 soit 30:1

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive03.webp)
_Tracé du profil cycloïdal_

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive04.webp)
_Animation de la rotation du disque cycloïdal_

- `Oscillation vers rotation` Pour récupérer un mouvement utilisable (donc de rotation pur), un étage de broches de sortie traverse les cinq perçages dans le disque. Ces broches "filtrent" l'oscillation et ne transmettent que la rotation à l'arbre de sortie (CF [Animation](#animation))

### Conception 3D du réducteur

Vous pouvez consultez un 3D intéractif ici : 
<https://ironshift.github.io/static/3DCycloidalDrive>

## Animation

Pour sublimer la mécanique du réducteur, j'ai utilisé KeyShot, un moteur de rendu basé sur le ray-tracing en temps réel. Ce logiciel permet d'appliquer des matériaux aux propriétés physiques proches du réel et de simuler des environnements lumineux complexes pour obtenir un résultat photo-réaliste.

L'enjeu ici était de synchroniser parfaitement les rotations de l'excentrique avec le mouvement orbital du disque pour mettre en évidence la réduction de vitesse.

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive05.webp)
_Animation sous KeyShot 2023_

La haute fidélité visuelle demande une puissance de calcul considérable. voici les paramètres de l'export :

- Moteur de rendu :	Mode GPU (NVIDIA RTX 3080)
- Résolution : 4K UHD (3840×2160 px)
- FPS : 60 images par seconde
- Volume de calcul : 2400 images individuelles
- Poids brut : 40 Go (avant compression MP4)
- Temps d'export : 13 heures et 25 minutes

{% include embed/youtube.html id='dRT5a-yM1lU ' %}

## Validation Physique

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive06.webp)
_Assemblage du prototype imprimé en 3D_

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive07.gif)
_Fonctionnement interne du prototype_

## Conclusion

Le résultat est un réducteur efficace et vraiment compact. L'impression 3D montre toutefois ses limites sur un format aussi petit : on observe quelques défauts d'excentricité qui se ressentent sur l'arbre de sortie.

Pour la suite, une évolution intéressante serait de passer sur un système à double disque inversé à 180°. Cela permettrait de compenser naturellement le balourd de l'excentrique et d'équilibrer le mécanisme, ce qui est indispensable pour une utilisation à haute vitesse sans vibrations.

Cependant, cela implique une conception plus complexe, notamment au niveau de l'assemblage de l'excentrique (arbre à double cames opposées).

![Desktop View](/assets/reducteur_cycloidal/CycloidalDrive08.webp)
_Première itération d'un réducteur à double disque cycloïdal_