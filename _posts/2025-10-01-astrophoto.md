---
title: Astrophotographie
date: 2025-10-01 00:00:00 +0000
description: Réalisation d’un setup d'astrophotographie du ciel profond de A à Z
categories: [Projets personels, CAO disponible]
tags: []     # TAG names should always be lowercase
math: true
image:
  path: /assets/astrophoto/andromeda.webp
---

# Objectif

Ce projet a pour objectif de concevoir un setup complet d’astrophotographie du ciel profond, performant et financièrement raisonnable. L’idée est de construire une solution capable d’assurer l’alignement, le suivi et le pilotage d'un appareil photo, afin d’obtenir des images nettes et exploitables des objets célestes.

Le projet sera présenté en plusieurs parties, chacune abordant un élément essentiel du dispositif :

- `Le système d’alignement polaire :` indispensable pour orienter correctement la monture par rapport à l’axe de rotation de la Terre et garantir un suivi précis.

- `Le système de suivi :` au cœur du setup, il compense la rotation terrestre et maintient la cible centrée pendant les longues poses nécessaires à l’imagerie du ciel profond.

- `Le boîtier de contrôle :` il assurera le pilotage de la monture, la gestion du suivi et la commande de l’appareil photo.

## Rappel du fonctionnement de l’astrophotographie

L’astrophotographie du ciel profond repose sur un principe simple : capter et accumuler un maximum de lumière provenant d’objets situés à des dizaines de milliers, voire des millions d’années-lumière. Contrairement à la photographie classique, où les sujets sont lumineux et les temps de pose relativement courts, l’astrophotographie nécessite d’exposer le capteur sur de longues durées afin d’augmenter le rapport signal/bruit.

Un objet du ciel profond (nébuleuse, galaxie, amas…) émet très peu de photons. Pour obtenir une image exploitable, le capteur doit ces photons pendant une longue durée (de quelques minutes à plusieurs heures). 

`Le signal enregistré est proportionnel au nombre de photons collectés, donc au temps de pose`

Plus le temps de pose est long, plus l’objet devient visible. Le bruit associé à la lumière elle-même, appelé bruit photonique, obéit à une loi de Poisson : lorsqu’on multiplie le temps de pose par 10, le signal est multiplié par 10, mais le bruit photonique n’augmente que d’un facteur Racine(10).

$$
\begin{equation}
   Signal= Φ * t
\end{equation}
$$

$$
\begin{equation}
   Bruit= Φ * \sqrt{t}
\end{equation}
$$

Autrement dit, le rapport signal/bruit s’améliore avec la racine carrée du temps d’exposition, ce qui rend les longues poses particulièrement efficaces pour révéler les objets ténus du ciel profond.

## Le mouvement de la Terre : la source du problème

Durant la pose, la Terre tourne autour de son axe à une vitesse angulaire approximative de :

$$
\begin{equation}
   ωTerre = {2π \over 24h} ≈ {15"arc \over sec}
   \end{equation}
$$

![Desktop View](/assets/astrophoto/arcseconddiagram.webp)
_Explication des minutes et secondes d'arc_

(La durée de rotation exacte de la terre étant 23h 56min 4,091s (1 jour sidéral), la vrai vitesse de rotation de la terre est de 15.0410687 secondes d'arc / sec)


Sans compensation, ce mouvement provoque un déplacement du champ sur le capteur, créant un filé d’étoiles au lieu de points lumineux. Pour éviter cela, il faut suivre la rotation terrestre avec une monture motorisée.


![Desktop View](/assets/astrophoto/startrail.webp)
_Exemple d'une pose longue sans suivi du ciel (Source : Reign Abarintos)_


## Le suivi équatorial : compenser la rotation terrestre

Une monture équatoriale permet d’aligner un de ses axes (l’axe d'ascension droite) parallèlement à l’axe de rotation terrestre. Une fois correctement orientée (via un alignement polaire), une seule motorisation suffit à compenser la rotation apparente du ciel.

Si la monture suit le ciel avec une vitesse angulaire égale à celle de la Terre, alors les étoiles restent immobiles sur le capteur, permettant des poses longues de plusieurs minutes sans filé.

## Alignement polaire - Table équatoriale

L’alignement polaire consiste à orienter l’axe de rotation de la monture équatoriale de manière parfaitement parallèle à l’axe de rotation de la Terre. Cet ajustement est essentiel, car seul un axe correctement aligné permet à la monture de compenser la rotation terrestre en n’utilisant qu’un moteur en ascension droite. Un mauvais alignement entraîne un suivi imparfait, des dérives progressives et un allongement des étoiles sur les poses longues.

![Desktop View](/assets/astrophoto/miseenstation.webp)
_Exemple de la mise en station d'une monture équatoriale_

Pour réaliser la « mise en station », ou alignement polaire, nous allons fabriquer un module appelé table équatoriale. Ce dispositif permet de pointer précisément le pôle nord céleste (autrement dit l'axe de rotation de la terre) en ajustant la monture selon deux axes :

- L’altitude : réglage vertical (haut/bas),
- L’azimut : réglage horizontal (gauche/droite).

1. Pré-alignement rapide au laser

La première étape consiste à orienter grossièrement la monture vers le pôle céleste.
Une visée laser alignée avec l’axe de la monture permet de pointer directement la région de l’étoile polaire.
Cet ajustement n’a pas besoin d’être précis (1 à 2° d'erreur) : il sert simplement à placer la monture dans la bonne zone du ciel pour faciliter la suite.

![Desktop View](/assets/astrophoto/miseenstationlaser.webp)
_Alignement polaire grossier avec un laser (Source : Peter Zelinka)_

2. Alignement polaire précis : méthode des trois points

Le réglage fin est ensuite réalisé via une méthode d’astrométrie, le principe est le suivant :

La monture pointe successivement trois zones du ciel. À chaque position, une image est capturée puis analysée : le logiciel identifie les étoiles présentes en les comparant à une base de données et, grâce à cette correspondance, calcule les coordonnées exactes du point visé.

Le logiciel compare la position où la monture devrait se trouver (calculée à partir de la base de données) avec la position réellement observée. L’écart entre ces deux points correspond à l’erreur de mise en station. L’utilisateur corrige alors cette erreur en ajustant les vis d’azimut et d’altitude jusqu’à ce que l’alignement soit suffisamment précis (souvent inférieur à quelques dizaines d’arcsecondes).

### Conception 3D de la table équatoriale

Vous pouvez consultez un 3D intéractif ici : 
<https://ironshift.github.io/static/3DPolarAdjustmentUnit>



Voici la table équatoriale en action suivant l'axe de L’altitude :

![Desktop View](/assets/astrophoto/polarfindergif.gif)
![Desktop View](/assets/astrophoto/polarfinder1.webp)
![Desktop View](/assets/astrophoto/polarfinder2.webp)
![Desktop View](/assets/astrophoto/polarfinder3.webp)

## Suivi du ciel - Monture harmonique

La monture harmonique sera entraînée par un moteur pas à pas, ce qui permet un contrôle précis de la position de l’appareil photo. Le moteur retenu est un modèle 400 pas par tour, offrant une meilleure résolution angulaire et donc une finesse de suivi accrue.

Les drivers moteurs utilisés permettent en outre un pilotage en micro-pas jusqu’au 1/64 de pas, ce qui améliore la fluidité du mouvement et réduit les effets de saccades lors du suivi.

La chaîne de transmission complète est donc composée des éléments suivants :
- Moteur pas à pas : 400 pas par tour
- Réducteur planétaire : 5:1,
- Réducteur harmonique : 100:1.

La résolution totale obtenue sera donc de : 400×64×5×100=12 800 000 micro-pas / tour

Un tour complet correspond à : 360° = 1 296 000 secondes d'arc

La résolution angulaire par micro-pas est donc :

$$
\begin{equation}
   Resolution = {1 296 000 \over 12 800 000} ≈ 0.10125 "
   \end{equation}
$$

Pour rappel, le ciel se déplace à 15"arc / secondes. la résolution est donc largement suffisante pour assurer un suivi précis du ciel.

### Conception 3D de la monture harmonique

Vous pouvez consultez un 3D intéractif ici : 
<https://ironshift.github.io/static/3DPowerTrain>

![Desktop View](/assets/astrophoto/Powertrain1.webp)
![Desktop View](/assets/astrophoto/Powertrain2.webp)
![Desktop View](/assets/astrophoto/Powertrain3.webp)


## Le boîtier de contrôle


### Conception 3D du boitier de contrôle

Vous pouvez consultez un 3D intéractif ici : 
<https://ironshift.github.io/static/3DControlBox>

![Desktop View](/assets/astrophoto/controlbox01.webp)
![Desktop View](/assets/astrophoto/controlbox02.webp)
![Desktop View](/assets/astrophoto/controlbox03.webp)
![Desktop View](/assets/astrophoto/controlbox04.webp)
![Desktop View](/assets/astrophoto/controlbox05.webp)

