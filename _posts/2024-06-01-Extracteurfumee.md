---
title: Extrateur de fumées portable
date: 2024-06-01 00:00:00 +0000
description: Réalisation d’un extracteur de fumée de soudure
categories: [Projets personels]
tags: []     # TAG names should always be lowercase
math: true
image:
  path: /assets/Extracteur_fumee/Extracteurfumee03.webp
---

# Objectif

Lors de la soudure d’électronique, des vapeurs nocives sont émises, notamment à cause du flux (résine de colophane) et des particules de métaux comme le plomb, l’étain ou d’autres alliages. Ces fumées représentent un risque réel pour la santé : elles peuvent irriter les yeux et les voies respiratoires, et provoquer, à long terme, de l’asthme ou des maladies respiratoires chroniques. 

Le plomb, en particulier, est un neurotoxique bien documenté : son inhalation répétée peut entraîner des effets graves (troubles neurologiques, atteintes rénales, problèmes reproductifs…). 

Pour minimiser ces dangers, l’extraction des fumées à la source est une mesure de prévention largement recommandée. 

L’objectif de ce projet est donc de concevoir un système portable, alimenté par batterie, capable d’extraire et de filtrer efficacement les vapeurs de soudure même en environnement clos, avec une puissance d’extraction réglable.

## La filtration

La filtration idéale doit combiner plusieurs étapes pour capter à la fois les particules et les vapeurs chimiques :
1. Filtration des particules fines
- Filtre HEPA (High Efficiency Particulate Air) : capture les particules solides très fines (≥0,3 µm).

2. Filtration des vapeurs chimiques
- Filtres à charbon actif : absorbe les composés organiques volatils (COV) issus du flux (résine, colophane, solvants).
- Peut être combiné avec des filtres spécialisés pour les fumées de soudure contenant du plomb ou d’autres métaux lourds.

Pour ce modèle portable, nous utiliserons uniquement un filtre à charbon actif. Bien que l’idéal pour une protection complète inclurait également un filtre HEPA pour capturer les particules fines de soudure, celui-ci créera une résistance à l’air trop importante, ce qui “étoufferait” le flux d’air. Pour capter efficacement les fumées, il faudrait alors se tenir à moins de 5 cm de l’extracteur, ce qui serai peu pratique. Nous nous limiterons donc à un filtre à charbon actif, qui offre un bon compromis entre filtration des vapeurs et puissance d’aspiration dans un format portable.

## Les composants électroniques :

- Ventilateur 24 V

Le choix s’est porté sur un ventilateur à forte pression statique, essentielle pour maintenir un flux d’air efficace à travers le filtre à charbon actif. Une pression statique élevée permet de surmonter la résistance du filtre et d’assurer un bon compromis entre débit d’air et puissance d’aspiration, garantissant que les fumées de soudure soient captées même à distance raisonnable.

- BMS 2S (référence HX-2S-JH20)

Un système de gestion de batterie (BMS) pour deux cellules en série sera intégré afin d’assurer la sécurité et la longévité des accumulateurs Li-ion. Il inclut les protections suivantes :

1. Protection contre la charge excessive
2. Protection contre la décharge excessive
3. Protection contre les courts-circuits
4. Protection contre la surintensité

- Module USB-C → 9 V

Le module permet de recharger la batterie via un port USB‑C standard, pratique pour une utilisation nomade et une recharge facile. Il utilise le protocole USB Power Delivery (USB PD) : lorsqu’il est connecté à un chargeur compatible, il échange des informations pour demander une tension de sortie spécifique, ici 9 V.

- Convertisseur Buck-Boost 5 – 32 V (référence XL6009 RED)

Ce convertisseur permet de régler la tension de sortie indépendamment de la tension d’entrée :

Mode buck : abaisse la tension lorsque la tension d’entrée est supérieure à la tension souhaitée.

Mode boost : augmente la tension lorsque la tension d’entrée est inférieure à la tension souhaitée.

Cette souplesse garantit un fonctionnement stable du ventilateur et du circuit électronique, même lorsque la batterie se décharge.

- Voltmètre en façade

Indique la tension en sortie du convertisseur pour suivre la tension d'alimentation du ventilateur.

- Potentiomètre pour le convertisseur Buck-Boost

Permet de régler finement la tension de sortie et, par conséquent, la vitesse du ventilateur, offrant un contrôle de la puissance d’extraction selon les besoins.

## Modélisation 3D

Modélisation réalisée sous SolidWorks

L’objectif est de concevoir un boîtier le plus compact possible, tout en étant compatible avec des filtres à charbon standard de forme carrée.

![Desktop View](/assets/Extracteur_fumee/Extracteurfumee06.webp)
![Desktop View](/assets/Extracteur_fumee/Extracteurfumee07.webp)

## Assemblage des composants


![Desktop View](/assets/Extracteur_fumee/Extracteurfumee05.webp)
_Assemblage de toute l'électronique_

![Desktop View](/assets/Extracteur_fumee/Extracteurfumee04.webp)
_Installation des filtres charbon actif_

![Desktop View](/assets/Extracteur_fumee/Extracteurfumee01.webp)
_Fermeture de la facade_

![Desktop View](/assets/Extracteur_fumee/Extracteurfumee02.webp)
_Premier allumage_

## Résultats

Le résultat final est très satisfaisant. Comme on peut le constater sur la photo ci-dessous, l’aspiration est largement suffisante, même avec deux étages de filtration au charbon actif.

![Desktop View](/assets/Extracteur_fumee/Extracteurfumee03.webp)

## Post Mortem

Si c’était à refaire, la conception de l’électronique serait repensée. Le module utilisé pour la recharge des batteries LiPo présente certaines limitations. En effet, une batterie LiPo se recharge normalement en courant constant jusqu’à atteindre sa tension nominale (4,2 V par cellule), puis passe en mode tension constante, où le courant diminue progressivement jusqu’à stabiliser complètement la batterie.

Le module actuel ne gère pas parfaitement ce profil de charge : bien que cela ne soit pas dramatique pour une utilisation ponctuelle, il peut entraîner une charge moins optimale et une usure prématurée des cellules sur le long terme.

Pour mes prochains projets, la gestion des batteries sera totalement repensée, avec un circuit de charge dédié LiPo respectant strictement le cycle courant‑constant / tension‑constante (CC/CV). Cela garantira une sécurité maximale, une durée de vie optimisée des batteries et une meilleure fiabilité globale du système.