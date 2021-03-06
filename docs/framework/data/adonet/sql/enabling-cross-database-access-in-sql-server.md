---
title: Activation de l'accès entre bases de données dans SQL Server
ms.date: 03/30/2017
ms.assetid: 10663fb6-434c-4c81-8178-ec894b9cf895
ms.openlocfilehash: 7018a500f777935d35bac0010c07258a313b08fe
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43742109"
---
# <a name="enabling-cross-database-access-in-sql-server"></a>Activation de l'accès entre bases de données dans SQL Server
Le chaînage des propriétés des bases de données croisées se produit lorsqu'une procédure dans une base de données repose sur des objets appartenant à une autre base de données. La chaîne des propriétés des bases de données croisées fonctionne de la même manière que le chaînage des propriétés dans une seule base de données, sauf qu'une chaîne de propriétés continue nécessite le mappage de tous les propriétaires d'objets au même compte de connexion. Si l'objet source de la base de données source et les objets cibles des bases de données cibles appartiennent au même compte de connexion, SQL Server ne vérifie pas les autorisations sur les objets cibles.  
  
## <a name="off-by-default"></a>Désactivé par défaut  
 Le chaînage des propriétés des bases de données est désactivé par défaut. Microsoft vous recommande de désactiver le chaînage des propriétés des bases de données croisées, car il vous expose aux risques de sécurité suivants :  
  
-   Les propriétaires et les membres de base de données des rôles de base de données `db_ddladmin` ou `db_owners` peuvent créer des objets appartenant à d'autres utilisateurs. Ces objets peuvent potentiellement viser des objets dans d'autres bases de données. Cela signifie que si vous activez le chaînage des propriétés des bases de données croisées, vous devez faire totalement confiance aux utilisateurs dans toutes les bases de données.  
  
-   Les utilisateurs avec l'autorisation CREATE DATABASE peuvent créer de nouvelles bases de données et attacher les bases de données existantes. Si le chaînage des propriétés des bases de données croisées est activé, ces utilisateurs peuvent accéder à des objets dans d'autres bases de données pour lesquels ils n'ont pas de privilèges à partir des bases de données qu'ils ont récemment créées ou attachées.   
  
## <a name="enabling-cross-database-ownership-chaining"></a>Activation du chaînage des propriétés des bases de données croisées  
 L'activation du chaînage des propriétés des bases de données croisées doit être réservée aux environnements dans lesquels vous pouvez faire totalement confiance aux utilisateurs disposant de privilèges élevés. Vous pouvez configurer l'activation au cours de l'installation pour l'ensemble des bases de données, ou de manière sélective pour des bases de données spécifiques à l'aide des commandes [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `sp_configure` et `ALTER DATABASE`.  
  
 Pour configurer de manière sélective le chaînage des propriétés des bases de données croisées, utilisez `sp_configure` afin de désactiver cette option pour le serveur. Puis, utilisez la commande ALTER DATABASE avec SET DB_CHAINING ON afin de configurer le chaînage des propriétés des bases de données croisées uniquement pour les bases de données qui le nécessitent.  
  
 L'exemple suivant active le chaînage des propriétés des bases de données pour toutes les bases de données :  
  
```  
EXECUTE sp_configure 'show advanced', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'cross db ownership chaining', 1;  
RECONFIGURE;  
```  
  
 L'exemple suivant active le chaînage des propriétés des bases de données de bases de données spécifiques :  
  
```  
ALTER DATABASE Database1 SET DB_CHAINING ON;  
ALTER DATABASE Database2 SET DB_CHAINING ON;  
```  
  
### <a name="dynamic-sql"></a>Code SQL dynamique  
 Le chaînage des propriétés des bases de données croisées ne fonctionne pas dans les cas où des instructions SQL créées dynamiquement sont exécutées sauf si le même utilisateur existe dans les deux bases de données. Il est possible de contourner cette restriction dans SQL Server en créant une procédure stockée qui accède aux données dans une autre base de données et en signant la procédure avec un certificat qui existe dans les deux bases de données. De cette manière, les utilisateurs ont accès aux ressources de base de données utilisées par la procédure sans que l'accès ou les autorisations de base de données leur soient octroyés.  
  
## <a name="external-resources"></a>Ressources externes  
 Pour plus d'informations, voir les ressources ci-dessous.  
  
|Ressource|Description|  
|--------------|-----------------|  
|[Extension de l’emprunt d’identité de base de données à l’aide de EXECUTE AS](https://msdn.microsoft.com/library/ms188304\(SQL.105\).aspx) et [Cross DB Ownership Chaining Option](/sql/database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option)documentation en ligne SQL Server.|Rubriques décrivent comment configurer le chaînage des bases de données croisées pour une instance de SQL Server.|  
  
## <a name="see-also"></a>Voir aussi  
 [Sécurisation des applications ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 [Vue d’ensemble de la sécurité SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)  
 [Gestion des autorisations avec les procédures stockées dans SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)  
 [Écriture de code SQL dynamique sécurisé dans SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)  
 [Signature de procédures stockées dans SQL Server](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)  
 [Fournisseurs managés ADO.NET et centre de développement DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
