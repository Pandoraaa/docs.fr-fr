---
title: "Composition de sous-requ&#234;tes Entity SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 685d4cd3-2c1f-419f-bb46-c9d97a351eeb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Composition de sous-requ&#234;tes Entity SQL
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] est un langage fonctionnel riche.  Le bloc de construction d'[!INCLUDE[esql](../../../../../../includes/esql-md.md)] est une expression.  À la différence du langage SQL classique, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] n'est pas limité à un jeu de résultats tabulaire : [!INCLUDE[esql](../../../../../../includes/esql-md.md)] prend en charge la composition d'expressions complexes pouvant contenir des littéraux, des paramètres ou des expressions imbriquées.  Une valeur de l'expression peut être paramétrée ou composée d'une autre expression.  
  
## Expressions imbriquées  
 Une expression imbriquée peut être placée partout où une valeur du type qu'elle retourne est acceptée.  Par exemple :  
  
```  
-- Returns a hierarchical collection of three elements at top-level.   
-- x must be passed in the parameter collection.  
ROW(@x, {@x}, {@x, 4, 5}, {@x, 7, 8, 9})  
  
-- Returns a hierarchical collection of one element at top-level.  
-- x must be passed in the parameter collection.  
{{{@x}}};  
```  
  
 Une requête imbriquée peut être placée dans une clause de projection.  Par exemple :  
  
```  
-- Returns a collection of rows where each row contains an Address entity.  
-- and a collection of references to its corresponding SalesOrderHeader entities.  
SELECT address, (SELECT DEREF(soh)   
                    FROM NAVIGATE(address, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS soh)   
                    AS salesOrderHeader FROM AdventureWorksEntities.Address AS address  
```  
  
 Dans [!INCLUDE[esql](../../../../../../includes/esql-md.md)], les requêtes imbriquées doivent toujours être placées entre parenthèses :  
  
```  
-- Pseudo-Entity SQL  
( SELECT …  
FROM … )  
UNION ALL  
( SELECT …  
FROM … );  
```  
  
 L'exemple suivant montre comment imbriquer correctement des expressions dans [!INCLUDE[esql](../../../../../../includes/esql-md.md)] : [How to: Order the Union of Two Queries](http://msdn.microsoft.com/fr-fr/853c583a-eaba-4400-830d-be974e735313).  
  
## Requêtes imbriquées dans la projection  
 Les requêtes imbriquées d'une clause de projection peuvent être traduites en requêtes de produit cartésien sur le serveur.  Sur certains serveurs principaux dont SQL Server, cela peut avoir pour conséquences l'augmentation de volume de la table TempDB et une diminution des performances du serveur.  
  
 Vous trouverez ci\-dessous un exemple de ce type de requête :  
  
```  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## Ordre de tri des requêtes imbriquées  
 Dans Entity Framework, une expression imbriquée peut être placée n'importe où dans la requête.  Entity SQL offrant une grande souplesse dans l'écriture des requêtes, il est possible d'écrire une requête qui contient un classement des requêtes imbriquées.  Toutefois, l'ordre d'une requête imbriquée n'est pas conservé.  
  
```  
-- The following query will order the results by last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## Voir aussi  
 [Vue d'ensemble d'Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)