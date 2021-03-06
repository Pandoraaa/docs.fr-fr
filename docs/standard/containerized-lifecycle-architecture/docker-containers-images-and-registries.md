---
title: Conteneurs, images et registres Docker
description: Cycle de vie des applications Docker en conteneur avec la plateforme et les outils Microsoft
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: ff5a1f3e4b09ac9f7ea600d3f127523b96fcce55
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37106361"
---
# <a name="docker-containers-images-and-registries"></a>Conteneurs, images et registres Docker

Lorsque vous utilisez Docker, vous créez une application ou le service et le package il et ses dépendances dans une image de conteneur. Une image est une représentation statique de l’application ou du service, de leur configuration et de leurs dépendances.

Pour exécuter l’application ou le service, l’image de l’application est instancié pour créer un conteneur, qui est exécuté sur l’hôte Docker. Les conteneurs sont initialement testés sur une machine ou un environnement de développement.

Stocker des images dans un Registre, qui agit comme une bibliothèque d’images. Vous avez besoin d’un Registre lors du déploiement vers orchestrators de production. Docker gère un registre public via [Docker Hub](https://hub.docker.com/). D’autres fournisseurs proposent des registres pour différentes collections d’images. Les entreprises peuvent également gérer un registre privé local pour stocker leurs propres images Docker.

Figure 1-4 indique comment les images et les registres dans Docker se rapportent à d’autres composants. Elle montre également les divers registres des autres fournisseurs.

![](./media/image4.png)

Classification de la figure 1-4 : de Docker termes et concepts

En plaçant des images dans un Registre, vous pouvez stocker les bits d’application statique et immuable, y compris toutes leurs dépendances, au niveau d’une infrastructure. Vous pouvez version puis et déployer des images dans plusieurs environnements et donc fournissent une unité de déploiement cohérent.

Les registres de l’image privée, hébergé localement ou dans le cloud, sont recommandés pour les situations suivantes :

-   Vous ne voulez pas partager vos images publiquement pour des raisons de confidentialité.

-   Vous souhaitez limiter la latence du réseau entre vos images et l’environnement de déploiement choisi. Par exemple, si votre environnement de production est Azure, vous souhaiterez probablement stocker vos images dans le Registre de conteneur Azure afin que la latence du réseau sera minime. De la même manière, si votre environnement de production est local, vous souhaiterez peut-être disposer d’un service Docker Trusted Registry local dans le même réseau local.

>[!div class="step-by-step"]
[Précédent](docker-terminology.md)
[Suivant](Docker-application-lifecycle/index.md)
