---
title: Opérateurs d'égalité
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], Equals method
- class library design guidelines [.NET Framework], equality operator
- equality operator (==) [.NET Framework]
- Equals method
- == operator (equality) [.NET Framework]
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 27550a8fd8292029cad9c2e699374a190b1a532e
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48839353"
---
# <a name="equality-operators"></a>Opérateurs d'égalité
Cette section traite de surcharge les opérateurs d’égalité et fait référence à `operator==` et `operator!=` en tant que les opérateurs d’égalité.  
  
 **X DO NOT** un des opérateurs d’égalité et pas dans l’autre surcharge.  
  
 **✓ DO** vous assurer que <xref:System.Object.Equals%2A?displayProperty=nameWithType> et les opérateurs d’égalité ont exactement la même sémantique et des caractéristiques similaires.  
  
 Cela signifie souvent que `Object.Equals` doit être remplacée lorsque les opérateurs d’égalité sont surchargés.  
  
 **X AVOID** lever des exceptions à partir des opérateurs d’égalité.  
  
 Par exemple, retourner false si l’un des arguments est null au lieu de lever `NullReferenceException`.  
  
## <a name="equality-operators-on-value-types"></a>Opérateurs d’égalité sur les Types valeur  
 **✓ DO** surcharger les opérateurs d’égalité sur les types valeur, si l’égalité est explicite.  
  
 Dans la plupart des langages de programmation, il n’existe aucune implémentation par défaut de `operator==` pour les types valeur.  
  
## <a name="equality-operators-on-reference-types"></a>Opérateurs d’égalité sur les Types référence  
 **X AVOID** la surcharge des opérateurs d’égalité sur les types référence mutables.  
  
 De nombreux langages ont des opérateurs d’égalité intégrés pour les types référence. Les opérateurs intégrés implémentent généralement l’égalité de référence et de nombreux développeurs sont surpris lorsque le comportement par défaut est modifié à l’égalité de valeur.  
  
 Ce problème est atténué pour les types référence immuable, car l’immuabilité rend beaucoup plus difficile à remarquer la différence entre une égalité de référence et l’égalité des valeurs.  
  
 **X AVOID** surcharge des opérateurs d’égalité sur les types référence si l’implémentation est beaucoup plus lente que celui de l’égalité des références.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Tous droits réservés.*  
  
 *Réimprimé avec l’autorisation de Pearson Education, Inc. et extrait de [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) par Krzysztof Cwalina et Brad Abrams, publié le 22 octobre 2008 par Addison-Wesley Professional dans le cadre de la série sur le développement Microsoft Windows.*  
  
## <a name="see-also"></a>Voir aussi

- [Règles de conception de .NET Framework](../../../docs/standard/design-guidelines/index.md)  
- [Indications relatives à l’utilisation](../../../docs/standard/design-guidelines/usage-guidelines.md)
