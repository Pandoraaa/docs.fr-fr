---
title: LINQ et types génériques (C#)
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], generic types
- generic types [LINQ]
- generics [LINQ]
ms.assetid: 660e3799-25ca-462c-8c4a-8bce04fbb031
ms.openlocfilehash: 45bc5cbbdd1c0721797aed38636892e731c2883f
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43513884"
---
# <a name="linq-and-generic-types-c"></a>LINQ et types génériques (C#)
Les requêtes [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] sont basées sur des types génériques, qui ont été introduits dans la version 2.0 du [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]. Vous ne devez pas avoir une connaissance approfondie des génériques avant de commencer à écrire des requêtes. Il peut cependant être important de comprendre deux concepts de base :  
  
1.  Quand vous créez une instance d’une classe de collection générique comme <xref:System.Collections.Generic.List%601>, vous remplacez le « T » par le type des objets contenus dans la liste. Par exemple, une liste de chaînes est exprimée sous la forme `List<string>`, et une liste d’objets `Customer` est exprimée sous la forme `List<Customer>`. Une liste générique est fortement typée et offre de nombreux avantages par rapport aux collections qui stockent leurs éléments en tant que <xref:System.Object>. Si vous essayez d’ajouter un `Customer` à un `List<string>`, vous obtenez une erreur à la compilation. Il est facile d’utiliser des collections génériques, car vous ne devez pas effectuer un cast de type à l’exécution.  
  
2.  <xref:System.Collections.Generic.IEnumerable%601> est l’interface qui permet l’énumération des classes de collection génériques avec l’instruction `foreach`. Les classes de collection génériques prennent en charge <xref:System.Collections.Generic.IEnumerable%601> de la même façon que les classes de collection non génériques telles que <xref:System.Collections.ArrayList> prennent en charge <xref:System.Collections.IEnumerable>.  
  
 Pour plus d’informations sur les génériques, consultez [Génériques](../../../../csharp/programming-guide/generics/index.md).  
  
## <a name="ienumerablet-variables-in-linq-queries"></a>Variables IEnumerable<T\> dans les requêtes LINQ  
 Les variables de requête [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] sont de type <xref:System.Collections.Generic.IEnumerable%601> ou d’un type dérivé tel que <xref:System.Linq.IQueryable%601>. Quand vous voyez une variable de requête typée en `IEnumerable<Customer>`, cela signifie simplement que la requête génère à l’exécution une séquence de zéro ou plusieurs objets `Customer`.  
  
 [!code-csharp[csLINQGettingStarted#34](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_1.cs)]  
  
 Pour plus d’informations, consultez [Relations des types dans des opérations de requête LINQ](../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
## <a name="letting-the-compiler-handle-generic-type-declarations"></a>Laisser le compilateur gérer les déclarations de types génériques  
 Si vous préférez, vous pouvez éviter une syntaxe générique en utilisant le mot clé [var](../../../../csharp/language-reference/keywords/var.md). Le mot clé `var` indique au compilateur d’inférer le type d’une variable de requête en examinant la source de données spécifiée dans la clause `from`. L’exemple suivant génère le même code compilé que l’exemple précédent :  
  
 [!code-csharp[csLINQGettingStarted#35](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_2.cs)]  
  
 Le mot clé `var` est utile quand le type de la variable est évident ou quand il n'est pas particulièrement important de spécifier explicitement des types génériques imbriqués, comme ceux qui sont produits par des requêtes de groupe. D’une façon générale, si vous utilisez `var`, sachez qu’il peut rendre votre code plus difficile à lire par d’autres développeurs. Pour plus d’informations, consultez [Variables locales implicitement typées](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## <a name="see-also"></a>Voir aussi

- [Bien démarrer avec LINQ en C#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)  
- [Génériques](../../../../csharp/programming-guide/generics/index.md)
