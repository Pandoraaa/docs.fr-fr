---
title: "Navigation dans la collection de nœuds &#224; l&#39;aide de XPathNavigator | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 1a954b41-7173-40bc-8544-d430f209b1e5
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Navigation dans la collection de nœuds &#224; l&#39;aide de XPathNavigator
Vous pouvez parcourir les nœuds d'un objet <xref:System.Xml.XPath.XPathDocument> ou <xref:System.Xml.XmlDocument> à l'aide des méthodes de navigation entre les collections de nœuds de la classe <xref:System.Xml.XPath.XPathNavigator>.  Vous pouvez parcourir tous ces nœuds ou certaines collections de nœuds retournées par l'une des méthodes de sélection de la classe <xref:System.Xml.XPath.XPathNavigator>.  
  
## Navigation entre les collections de nœuds d'éléments  
 La classe <xref:System.Xml.XPath.XPathNavigator> fournit plusieurs méthodes de navigation entre les nœuds d'élément.  Le tableau suivant indique les méthodes de navigation disponibles et donne une description de leur mode de déplacement, mais ne comprend pas les méthodes permettant de naviguer entre les nœuds d'attribut et d'espace de noms.  
  
 Pour plus d'informations sur la sélection des nœuds dans un objet <xref:System.Xml.XPath.XPathNavigator>, voir [Sélection, évaluation et mise en correspondance de données XML à l'aide de XPathNavigator](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md).  Pour plus d'informations sur la navigation entre les nœuds d'attribut et d'espace de noms, voir [Navigation entre les nœuds d'attribut et d'espace de noms à l'aide de XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md).  
  
|Méthode|Description|  
|-------------|-----------------|  
|<xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers la même position que l'objet <xref:System.Xml.XPath.XPathNavigator> spécifié.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers un nœud enfant du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le premier nœud frère du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le premier nœud enfant du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToFollowing%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers l'élément spécifié dans l'ordre du document.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le nœud possédant un attribut de type `ID` avec une valeur correspondant à l'objet <xref:System.String> donné.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le nœud frère suivant du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le nœud parent du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le nœud frère précédent du nœud actuel.|  
|<xref:System.Xml.XPath.XPathNavigator.MoveToRoot%2A>|Déplace l'objet <xref:System.Xml.XPath.XPathNavigator> vers le nœud racine du document XML.|  
  
## Commentaires et instructions de traitement de la navigation entre les nœuds  
 Les méthodes suivantes de la classe <xref:System.Xml.XPath.XPathNavigator> sont valide pour le déplacement de commentaires ou d'instructions de traitement d'autres nœuds dans un document XML.  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToNext%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToPrevious%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToFirstChild%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToChild%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToParent%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.MoveToId%2A>  
  
## Voir aussi  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Traitement des données XML à l'aide du modèle de données XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Navigation entre les nœuds d'attribut et d'espace de noms à l'aide de XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)   
 [Extraction de données XML à l'aide de XPathNavigator](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)   
 [Accès à des données XML fortement typées à l'aide de XPathNavigator](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)