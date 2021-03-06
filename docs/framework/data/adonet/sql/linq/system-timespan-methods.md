---
title: System.TimeSpan, méthodes
ms.date: 03/30/2017
ms.assetid: 9333fee8-1454-4374-855b-8c14c002f48f
ms.openlocfilehash: 2cb7201c113fe72ce03d0308ab8f97dca585e602
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33358315"
---
# <a name="systemtimespan-methods"></a>System.TimeSpan, méthodes
La prise en charge des membres pour <xref:System.TimeSpan?displayProperty=nameWithType> dépend beaucoup des versions du .NET Framework et de Microsoft SQL Server que vous utilisez.  
  
 Lorsqu'une méthode, une propriété ou un opérateur n'est pas pris en charge, cela implique que LINQ to SQL ne peut pas traduire le membre à des fins d'exécution sur SQL Server. Vous pouvez toujours utiliser ces membres dans votre code, ceux-ci devant toutefois être évalués avant la traduction de la requête en données Transact-SQL ou après l'extraction des résultats de la base de données.  
  
## <a name="previous-limitations"></a>Limites précédentes  
 Lorsque vous utilisez LINQ to SQL avec des versions du .NET Framework antérieures au .NET Framework 3.5 SP1, vous ne pouvez pas mapper les champs de base de données SQL Server à <xref:System.TimeSpan?displayProperty=nameWithType>. Toutefois, les opérations sur <xref:System.TimeSpan> sont prises en charge car des valeurs <xref:System.TimeSpan> peuvent être retournées par la soustraction <xref:System.DateTime> ou introduites dans une expression sous forme de variable littérale ou liée.  
  
## <a name="supported-systemtimespan-method-support"></a>Prise en charge de la méthode System.TimeSpan  
 Les méthodes, propriétés et opérateurs pris en charge par LINQ to SQL suivants peuvent être utilisés dans les requêtes LINQ to SQL. Une fois mappés dans le modèle objet ou le fichier de mappage externe, LINQ to SQL vous permet d'appeler un grand nombre des membres <xref:System.TimeSpan?displayProperty=nameWithType> à l'intérieur des requêtes LINQ to SQL.  
  
|Méthodes <xref:System.TimeSpan> prises en charge|Opérateurs <xref:System.TimeSpan> pris en charge|Propriétés <xref:System.TimeSpan> prises en charge|  
|------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.TimeSpan.Compare%2A>|<xref:System.TimeSpan.op_Equality%2A>|<xref:System.TimeSpan.Days%2A>|  
|<xref:System.TimeSpan.CompareTo%28System.TimeSpan%29>|<xref:System.TimeSpan.op_GreaterThan%2A>|<xref:System.TimeSpan.Hours%2A>|  
|<xref:System.TimeSpan.Duration%2A>|<xref:System.TimeSpan.op_GreaterThanOrEqual%2A>|<xref:System.TimeSpan.MaxValue>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%2CSystem.TimeSpan%29>|<xref:System.TimeSpan.op_Inequality%2A>|<xref:System.TimeSpan.Milliseconds%2A>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%29>|<xref:System.TimeSpan.op_LessThan%2A>|<xref:System.TimeSpan.Minutes%2A>|  
||<xref:System.TimeSpan.op_LessThanOrEqual%2A>|<!--zz <xref:System.TimeSpan.MinValue%2A>-->|  
  
> [!NOTE]
>  La capacité à mapper <xref:System.TimeSpan?displayProperty=nameWithType> à une colonne `TIME` SQL à l'aide de LINQ to SQL requiert .NET Framework 3.5 SP1 et version ultérieure. Le type de données `TIME` SQL est uniquement disponible à partir de Microsoft SQL Server 2008.  
  
### <a name="addition-and-subtraction"></a>Addition et soustraction  
 Contrairement au type <xref:System.TimeSpan?displayProperty=nameWithType> SQL, le type `TIME` CLR prend en charge l'addition et la soustraction. De ce fait, les requêtes LINQ to SQL génèrent des erreurs en cas de tentative d'addition et de soustraction lorsqu'elles sont mappées au type `TIME` SQL. Vous trouverez d’autres considérations pour l’utilisation des types de date et d’heure SQL dans [le mappage de Type SQL-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Concepts relatifs aux requêtes](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)  
 [Création du modèle objet](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)  
 [Mappage de type SQL-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)  
 [Fonctions et types de données](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
