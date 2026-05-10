---
title: Machine de traction portative
date: 2019-10-01 00:00:00 +0000
description: Conception et fabrication d'une machine de traction portative adaptée à la tomographie aux rayons X.
categories: [Études]
tags: []     # TAG names should always be lowercase
math: true
image:
  path: /assets/machine_traction/vueeclatee.webp
---

# Contexte

En science des matériaux, pour comprendre pourquoi un matériau casse, on utilise souvent un tomographe (un scanner à rayons X). Le problème est que pour voir l'intérieur d'une pièce pendant qu'on tire dessus, il faut une machine de traction capable de rentrer à l'intérieur du scanner mais également qui soit transparente aux rayons X.

L'objectif de ce projet de fin d'étude était de concevoir une machine miniature capable de :

- Développer une force de traction de 5 000 N.
- Une course de 10 mm
- Tenir dans un cylindre de la taille d'une bouteille d'eau de 1L.
- Être "transparente" aux rayons X pour ne pas masquer l'échantillon.
- La capacité de tester des éprouvettes plates (0,8 mm à 2 mm d'épaisseur) et cylindriques (4 mm de diamètre).  

# Théorie

## Capteur de force

L'essai de traction consiste à mesurer le degré de résistance à la rupture d'un matériau et son comportement élastique en appliquant un effort uniaxial.

Il permet de déterminer des paramètres clés comme le module de Young ($E$), la limite d'élasticité ($R_{e}$) et la résistance à la traction ($R_{m}$).  La mécanique de notre machine repose sur des formules classiques :
- Contrainte : $\sigma=\frac{F}{S_{0}}$   
- Module de Young : $E=\frac{F}{S}*\frac{1}{\frac{\Delta L}{L_{0}}}$   

Pour mesurer l'effort appliqué, nous avons sélectionné un capteur de force en forme de S (type CZL301), capable de supporter 5000 N (avec une surcharge jusqu'à 7500 N). Ce capteur utilise un pont de Wheatstone composé de jauges de contrainte. La variation de tension, qui permet de déduire la force, se calcule ainsi:  

$$V_{G}=U*(\frac{R_{2}}{R_{1}+R_{2}}-\frac{R_{4}}{R_{3}+R_{4}})$$

Son principal inconvénient était son grand encombrement axial. Pour pallier ce problème et optimiser l'espace, nous avons utilisé le corps du capteur lui-même pour réaliser la fonction de glissière, le contraignant ainsi à un seul degré de liberté (translation).  


![Desktop View](/assets/machine_traction/capteurdeforce.webp)
_Capteur de force en S utilisé comme glissière linéaire_

## Eprouvettes

Pour que les résultats d'un essai de traction soient exploitables et comparables, on ne peut pas tester n'importe quelle forme. Il est impératif d'utiliser des éprouvettes normalisées. Pour ce projet, la machine a été dimensionnée pour accueillir deux géométries spécifiques, en suivant les recommandations de la norme ISO 6892-1.

- Éprouvettes plates : Les épaisseurs compatibles avec notre machine de traction iront de 0,8 mm à 2 mm.

![Desktop View](/assets/machine_traction/eprouvettesplate.webp)

- Éprouvettes cylindriques : l’éprouvette cylindrique retenue aura un diamètre de 4 mm. Un diamètre supérieur aurait un encombrement trop important en hauteur. Un diamètre plus faible serait difficile à usiner dans certaines matières.

![Desktop View](/assets/machine_traction/eprouvettescylindrique.webp)


## Motorisation & transmission

**Motorisation :** Pour piloter la traction de manière constante, nous avons optés pour un moteur pas à pas couplé à un réducteur épicycloïdal. Cela nous permetra d'obtenir une excellente résolution de déplacement tout en ayant un couple suffisant (4,71 N.m)

**Transmission :** Une tige filetée M12 transmet l'effort au capteur. Une butée à billes est intégrée pour encaisser les efforts axiaux importants à la place du moteur, qui n'est absolument pas dimentionné pour.

## Chambre de traction

Dans une machine de traction conventionnelle, la partie supérieure est fixée à un bâti rigide tandis que la partie inférieure, motorisée, assure le déplacement. Ce type d'architecture "en portique" est impossible à intégrer dans un tomographe en raison de l'encombrement extrême.

![Desktop View](/assets/machine_traction/machinesdetractioncommerce.webp)
_Machine de traction conventionnelle du commerce_

Pour résoudre ce problème, nous avons remplacé le bâti traditionnel par un tube en PMMA usiné par nos soin. Ce tube remplit deux fonctions :

- Transmission d'effort : Il referme la boucle de force en reliant les deux extrémités de la machine. Pendant que le moteur tire sur l'éprouvette, le tube encaisse l'effort en compression.

- Transparence aux rayons X : Le PMMA a été choisi pour sa faible densité. Il laisse passer le flux de photons sans perturber l'image, permettant d'observer la matière au cœur du tube comme s'il était invisible.

# Simulation numérique

Avant de passer à la fabrication, il est crucial de valider le dimensionnement de chaque composant. Nous avons utilisé la simulation en déformation statique pour soumettre les éléments critiques (éprouvettes, tube PMMA, mors, etc) aux contraintes maximales de l'essai (5 000 N). L'objectif est double : s'assurer que la machine ne rompra pas et vérifier que les micro-déformations de la structure ne viendront pas fausser la précision de nos mesures de traction.

## L'importance de la convergence de maillage

Pour obtenir des résultats fiables en simulation, le choix du maillage est déterminant. Plus le maillage est fin, plus le calcul est précis mais encore faut t'il qu'il converge. Nous avons donc réalisé une étude de convergence de maillage : en augmentant progressivement le nombre d'éléments jusqu'à ce que les résultats de contraintes et de déplacements ne varient plus. Cette étape est indispensable pour garantir que les résultats obtenus ne dépendent pas du découpage informatique, mais reflètent bien la réalité physique du montage.

![Desktop View](/assets/machine_traction/convergencemaillage.webp)
_Convergence de maillage sur l'éprouvette plate_

## Eprouvettes

Les simulations sous une charge de 5 000 N confirment le bon dimensionnement de nos échantillons :

- Éprouvettes plates : Elles atteignent toutes leur point de rupture. C’est un excellent point pour le projet, car cela permettra d'observer l'intégralité du processus de dégradation et de cassure du matériau dans le tomographe.

- Éprouvette cylindrique : Plus résistante, elle entre dans le domaine plastique (déformation irréversible) mais ne parvient pas jusqu'à la rupture sous cet effort.

- Course mécanique : Avec une élongation prévue bien inférieure à 10 mm, la course maximale de la machine est largement suffisante pour accompagner la déformation de tous les types d'éprouvettes jusqu'à la fin de l'essai.

![Desktop View](/assets/machine_traction/simulationEprouvette.webp)


## Optimisation du cylindre PMMA

Le tube en PMMA est l’élément le plus critique de la structure : il doit être assez fin pour ne pas être trop encombrant, mais assez rigide pour supporter 5 000 N en compression sans fausser la mesure de traction.

L'enjeu est de limiter l'accourcissement du tube. Nos simulations montrent qu'avec un diamètre externe de 50 mm (épaisseur de 7,5 mm), le tube s'écrase de 0,08 mm. Comparé aux 0,14 mm de déformation de l'éprouvette la plus fine, cela générerait une erreur de mesure de 54%.

Choix technique :
Pour garantir la précision de l'essai, nous avons opté pour un diamètre externe de 70 mm. Cette configuration réduit le déplacement structurel à seulement 0,03 mm. Cette déformation résiduelle, est prédictible et peut être compensée logiciellement pour obtenir une courbe de traction exacte en prenant en compte l'écrasement du PMMA.

![Desktop View](/assets/machine_traction/simulationPMMA.webp)
![Desktop View](/assets/machine_traction/simulationsPMMA.webp)

# Mise en pratique

## Usinage

![Desktop View](/assets/machine_traction/eprouvettesplate2.webp)
_Poinçonnage de trois éprouvettes plates ; les éprouvettes seront ensuite limées afin d’éviter toute amorce de rupture._

![Desktop View](/assets/machine_traction/poinçonnage.webp)
_Programme de poinçonnage des éprouvettes plates_

![Desktop View](/assets/machine_traction/eprouvettescylindrique2.webp)
_Usinage d'une éprouvette cylindrique au tour traditionnel_

![Desktop View](/assets/machine_traction/vueeclatee.webp)
_Vue éclatée de l'assemblage complet_

![Desktop View](/assets/machine_traction/piecesusinees.webp)
_Intégralité des pièces non assemblées_

# Résultat 

Les tests finaux, illustrés dans la vidéo ci-dessous, confirment la robustesse de la conception.

![Desktop View](/assets/machine_traction/tractionvideo.gif)
_Essai de traction réel (vitesse x3) sur une éprouvette acier plate de 2mm_

Le prototype actuel constitue une plateforme robuste et prête pour les étapes suivantes. La suite du développement, qui sera reprise par le prochain groupe d'élèves, se concentrera sur :

- L'intégration électronique : Conception et fabrication d'un boîtier sur mesure pour regrouper proprement les cartes de commande et l'alimentation.

- Mise en pratique : Réalisation des premiers essais réels in situ directement à l'intérieur du tomographe pour valider l'acquisition d'images sous contrainte.

Projet réalisé par : J. Gillet & C. Le Chalony.