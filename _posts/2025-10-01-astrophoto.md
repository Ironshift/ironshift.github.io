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

![Desktop View](/assets/nyan.gif)