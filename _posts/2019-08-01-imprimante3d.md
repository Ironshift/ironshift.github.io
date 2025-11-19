---
title: Imprimante 3D
date: 2019-08-01 00:00:00 +0000
description: Conception et réalisation d'une imprimante 3D
categories: [Projets personels, CAO disponible]
tags: []     # TAG names should always be lowercase
math: true
image:
  path: /assets/imprimante_3d/imprimante02.webp
---

# Contexte

En 2018, les imprimantes 3D à ma disposition étaient une Creality CR-10 et une Ultimaker 2+. Malgré leurs qualités, ces deux machines présentaient de nombreux défauts techniques et des limites de fiabilité, nécessitant des ajustements fréquents pour obtenir des impressions correctes.

![Desktop View](/assets/imprimante_3d/creality_cr_10.webp)
_Creality CR-10, imprimande abordable_

![Desktop View](/assets/imprimante_3d/ultimaker2plus.webp)
_Ultimaker 2+, imprimante semi professionnelle_

# Objectif

Concevoir et réaliser une imprimante 3D abordable, fiable et dotée de fonctionnalités avancées, afin de dépasser les limites des modèles disponibles :

- Autonivelage du plateau
- Garantie de la planéité du plateau
- Mesure et compensation des résonances harmoniques de l’imprimante
- Système de transmission CoreXY
- Plateau magnétique flexible

## Première conception

Le système CoreXY est retenu pour la structure de l’imprimante car il offre un déplacement rapide et précis de la tête d’impression tout en limitant la masse en mouvement. Dans cette architecture, les moteurs restent fixes et actionnent la tête via un jeu de courroies croisées. Cette configuration réduit l’inertie, permet des accélérations plus élevées et améliore la qualité globale des impressions à grande vitesse.

![Desktop Vi1ew](/assets/imprimante_3d/corexy.webp)

Avantages du CoreXY :

- Masse mobile réduite : meilleure précision à haute vitesse.
- Cinématique efficace : mouvements X et Y combinés par les deux moteurs.
- Structure compacte et rigide.
- Moins de vibrations transversales qu’un système à plateau mobile.

Inconvénients :

- Montage plus complexe que les systèmes classiques.
- Nécessite un réglage précis des courroies.
- Sensible aux défauts d’alignement mécanique.

Voici un résumé vidéo des différentes transmission existant dans le monde de l'impression 3D, le core XY étant en 2019 extrèmement nouveau mais il ne serai pas étonnant de voir cette transmission se généraliser à toute l'industrie.

{% include embed/youtube.html id='_ramiM3KHYE' %}

L’imprimante sera construite à partir de profilés en aluminium 3030, un choix motivé par leur faible coût, leur rigidité et surtout leur modularité.
Ce type de profilé permet de réaliser une structure solide, facilement ajustable et évolutive, tout en conservant une excellente stabilité mécanique.

Les axes XYZ reposeront sur des tiges en acier de 10 mm, associées à des roulements linéaires. J’ai retenu les douilles IGUS Drylin® R RJ4JP-01, une alternative en polymère offrant un guidage précis, un fonctionnement silencieux et une maintenance minimale, tout en évitant le bruit caractéristique des roulements à billes traditionnels.

![Desktop View](/assets/imprimante_3d/igus_drylin.webp)
_IGUS Drylin® R RJ4JP-01_

![Desktop View](/assets/imprimante_3d/imprimantev1.webp)
_Premiète conception de l'imprimante_


Finalement, après la première conception et le début de l’assemblage, une reconception s’est révélée nécessaire afin de corriger de nombreux défauts. Les guidages IGUS associés aux axes en acier présentaient trop de jeu pour garantir la précision recherchée. Par ailleurs, l’électronique doit être revue : la carte BIGTREETECH TFT35 sera remplacée par une solution plus moderne intégrant des drivers TMC2209 et, surtout, une interface web permettant de piloter l’imprimante à distance, sans dépendre d’une carte SD.

![Desktop View](/assets/imprimante_3d/bttboardtft.webp)
_Bigtreetech TFT 3.5"_

![Desktop View](/assets/imprimante_3d/bttboardskr1.4.webp)
_Bigtreetech SKR 1.4_

## Seconde conception

Dans cette seconde itération, l’imprimante est entièrement repensée pour améliorer le guidage des axes.

Rails linéaires pour tous les axes :
Les guidages sont désormais assurés par des rails linéaires, bien plus rigides et précis que les tiges en acier avec douilles polymères.

![Desktop View](/assets/imprimante_3d/rail01.webp)

Leurs avantages :

- mouvement parfaitement rectiligne, sans jeu latéral ;
- rigidité accrue, idéale pour les accélérations élevées ;
- usure faible et comportement stable dans le temps ;

Remplacement de l’électronique par une Duet 3 Mini 5+

![Desktop View](/assets/imprimante_3d/duet3_mini.webp)


La carte Duet 3 Mini est retenue pour remplacer la solution précédente.
Ses atouts :

- drivers TMC2209 intégrés, silencieux et précis ;
- gestion avancée du courant moteur et interpolation des micro-pas ;
- interface web native via Duet Web Control, permettant de piloter l’imprimante, envoyer les fichiers, suivre les impressions et ajuster les paramètres à distance ;
- configuration centralisée via fichiers texte (pas de compilation), facilitant les réglages.

Nous allons également synchroniser mécaniquement l’axe Z
Une courroie de synchronisation est ajoutée pour relier les deux moteurs de l’axe Z.
Sans ce dispositif, lorsque l’imprimante est éteinte, les moteurs peuvent tourner librement et se désaligner après manipulation. Cela crée un écart entre les deux côtés du plateau, entraînant une perte de parralélisme entre la buse et le plateau.

### Résultats

L’imprimante fonctionne désormais très bien, avec une qualité d’impression très correcte et une vitesse largement au-dessus de celles obtenues avec l’Ultimaker 2+ et la Creality CR-10. Elle offre ainsi un débit d’impression élevé tout en maintenant une précision fiable et constante.

![Desktop View](/assets/imprimante_3d/imprimantev2.webp)

Malgré des performances globales très satisfaisantes, plusieurs défauts subsistent :

- Accessibilité de l’électronique : La carte et les composants associés sont positionnés sous les plaques visibles sur l’image ci-dessus. Toute opération de maintenance nécessite de basculer l’imprimante, ce qui complique l’entretien.
- Rattrapage de jeu sur l’axe Z : L’axe Z est entraîné par deux vis sans fin qui glissent dans des écrous en laiton. Lors du passage de la montée à la descente du plateau, un léger jeu provoque un délai de quelques dixièmes de millimètre avant que le plateau ne commence à se déplacer. Ce phénomène entraîne un défaut d’accumulation de matière lors des premières couches, provoquant le défaut suivant :

![Desktop View](/assets/imprimante_3d/pbpremierecouche.webp)

- L’axe Z, initialement guidé par quatre rails linéaires, s’est avéré trop contraint : la solution était hyperstatique et limitait la fluidité du mouvement.

## Troisième conception

Cette troisième et dernière conception vise à corriger ces défauts tout en ajoutant des fonctionnalités avancées :

- Plateau piloté par trois moteurs indépendants : Cette configuration permet de régler précisément l’angle du plateau par rapport à la buse, assurant une planéité parfaite et une meilleure adhérence des premières couches, même sur de grandes surfaces.

- Capteur de fin de filament : Ce capteur détecte l’épuisement du filament pendant l’impression et permet à l’imprimante de s’arrêter et de prévenir l’utilisateur, évitant ainsi les impressions incomplètes.

- Accéléromètres intégrés : Ces capteurs mesurent les vibrations et la réponse dynamique de l’imprimante, permettant un calibrage précis de la machine en fonction de ses caractéristiques réelles. Cela améliore la qualité d’impression et réduit les défauts liés aux oscillations ou à la résonance.


### Pilotage du plateau

Le plateau repose désormais sur trois points montés sur rotules (une bille posée sur deux axes), ce qui lui permet de se déplacer librement en fonction de la hauteur contrôlée par chaque moteur. Cette configuration autorise un pivotement selon les axes Rx et Ry, garantissant un alignement parfait entre le plateau et la buse et compensant les éventuels défauts de planéité ou d’assemblage.

Par ailleurs, les écrous traditionnels en laiton ont été remplacés par des pièces en POM (plastique auto-lubrifiant). Ces pièces, combinées à une vis de pression réglable, permettent d’appliquer une précontrainte sur les axes Z, supprimant complètement le jeu dans la transmission. Cette modification corrige efficacement les défauts rencontrés sur les premières couches et assure une précision et une régularité optimales dès le démarrage de l’impression.

![Desktop View](/assets/imprimante_3d/plateau3axes.webp)

![Desktop View](/assets/imprimante_3d/plateau3axes2.webp)

Grâce à la configuration à trois moteurs pilotant le plateau, il devient envisageable de réaliser une impression 3D non planaire.
Aujourd’hui, la plupart des imprimantes 3D fonctionnent selon un principe « 2.5D » : le plateau descend couche par couche de manière strictement horizontale, limitant les formes et les finitions possibles.
Avec ce nouveau système, le plateau peut effectuer des mouvements combinés en Rx et Ry, permettant des trajectoires ondulées ou des ajustements fins en cours d’impression. Cela ouvre la voie à des finitions plus précises et des formes complexes, offrant un rendu esthétique et fonctionnel bien supérieur à celui des méthodes traditionnelles :

{% include embed/youtube.html id='B9sdrezl6AU' %}

Pour le moment, voici le résultat obtenu lors de la calibration du plateau.
À 39 secondes exactement, après le palpage du quatrième point, l’imprimante calcule automatiquement les positions idéales des trois moteurs afin que le plateau soit le plus plat possible par rapport aux quatre points détectés. Cette procédure garantit une planéité optimale avant le début de l’impression.

{% include embed/youtube.html id='LgJerOm3Dhw' %}

### Accéléromètre

Fonctionnement de l’Input Shaping

L’Input Shaping est une technique utilisée pour réduire les vibrations et les oscillations d’une machine en mouvement. L’idée principale est d’ajuster la commande envoyée aux moteurs afin de compenser les résonances naturelles de la structure.

Voici le principe :

Mesure de la fréquence de résonance : On identifie les fréquences auxquelles la machine a tendance à vibrer (par exemple, les oscillations du plateau ou de la tête lors des accélérations).

Filtrage du signal de commande : Au lieu d’envoyer directement le mouvement désiré aux moteurs, le signal est « modelé » par un filtre qui découpe ou décale légèrement les commandes pour éviter d’exciter ces fréquences.

Résultat : Les mouvements restent rapides, mais les vibrations qui déforment les impressions sont fortement réduites.

En résumé, l’Input Shaping agit comme un « amortisseur numérique » : il ne modifie pas la mécanique, mais adapte la trajectoire des moteurs pour que la structure ne vibre pas. Cela permet d’augmenter la vitesse d’impression tout en conservant une qualité élevée.

![Desktop View](/assets/imprimante_3d/imputshaping.webp)
_Résultat attendu_

Après l’installation de l’accéléromètre LIS3DSH, la machine peut acquérir les données de vibration lors de mouvements programmés à différentes fréquences. L’objectif est d’identifier les fréquences propres de résonance de l’imprimante (les fréquences auxquelles la structure tend à osciller).

![Desktop Vi1ew](/assets/imprimante_3d/imprimante01.webp)
_Accéléromètre fixé sur la tête d'impression (carte électronique violette)_

- Analyse en domaine fréquentiel :

On applique une transformée de Fourier (FFT) sur les signaux d’accélération pour passer du domaine temporel au domaine fréquentiel. La FFT permet de détecter les pics d’amplitude correspondant aux fréquences de résonance naturelles de l’imprimante.

- Calcul des coefficients pour l’Input Shaping :

Une fois les fréquences de résonance connues, on conçoit un filtre numérique qui module les commandes moteurs.
Le principe est de séparer les impulsions envoyées aux moteurs de façon à annuler l’excitation de la résonance : par exemple, un mouvement est divisé en plusieurs micro-impulsions décalées dans le temps.

![Desktop View](/assets/imprimante_3d/freqavant.webp)
_Analyse fréquencielle AVANT compensation_

![Desktop View](/assets/imprimante_3d/freqapres.webp)
_Analyse fréquencielle APRES compensation_

Après l’application des coefficients calculés pour l’Input Shaping, on observe une réduction très nette des vibrations sur les trois axes de l’imprimante. Cela se traduit par une impression plus stable et une meilleure précision dimensionnelle surtout à des vitesses élevées.

### Positionnement de l'électronique :

L’électronique a été entièrement repensée. Elle reste positionnée dans le bas de l’imprimante, mais l’accès a été grandement facilité : il suffit désormais de retirer quatre panneaux maintenus magnétiquement pour intervenir facilement sur la carte et les composants, simplifiant ainsi la maintenance et le dépannage.

![Desktop Vi1ew](/assets/imprimante_3d/imprimante03.webp)

![Desktop Vi1ew](/assets/imprimante_3d/imprimante04.webp)


## Résultat final :

Vous pouvez consultez un 3D intéractif ici : <https://ironshift.github.io/static/3DImprimante3DV3>

![Desktop Vi1ew](/assets/imprimante_3d/imprimante02.webp)
