---
title: Documents et données XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5f286d0f64478bfc46ca207086e4a6b918ee47b5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33576088"
---
# <a name="xml-documents-and-data"></a>Documents et données XML
Le .NET Framework fournit un jeu de classes complet et intégré qui vous permet de créer facilement des applications capables de traiter du code XML. Les classes dans les espaces de noms suivants prennent en charge l’analyse et l’écriture de code XML, l’édition de donnés XML en mémoire, la validation de données et la transformation XSLT.  
  
-   <xref:System.Xml>  
  
-   <xref:System.Xml.XPath>  
  
-   <xref:System.Xml.Xsl>  
  
-   <xref:System.Xml.Schema>  
  
-   <xref:System.Xml.Linq>  
  
 Pour obtenir une liste complète, consultez la page web [Espaces de noms System.Xml](https://msdn.microsoft.com/library/gg145036.aspx).  
  
 Les classes dans ces espaces de noms prennent en charge les recommandations World Wide Web Consortium (W3C). Exemple :  
  
-   La classe <xref:System.Xml.XmlDocument?displayProperty=nameWithType> implémente les recommandations du [W3C relatives aux modèles objet de documents (DOM) de niveau 1](https://www.w3.org/TR/REC-DOM-Level-1/) et [2 (standard)](https://www.w3.org/TR/DOM-Level-2-Core/).  
  
-   Les classes <xref:System.Xml.XmlReader?displayProperty=nameWithType> et <xref:System.Xml.XmlWriter?displayProperty=nameWithType> sont conformes aux recommandations du [W3C relatives à XML 1.0](https://www.w3.org/TR/2006/REC-xml-20060816/) et aux [espaces de noms dans XML](https://www.w3.org/TR/REC-xml-names/).  
  
-   Les schémas de la classe <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=nameWithType> sont conformes aux recommandations du [W3C relatives aux structures (Part 1)](https://www.w3.org/TR/xmlschema-1/) et aux [types de données (Part 2) du schéma XML](https://www.w3.org/TR/xmlschema-2/).  
  
-   Les classes de l’espace de noms <xref:System.Xml.Xsl?displayProperty=nameWithType> prennent en charge les transformations XSLT qui sont conformes à la recommandation [W3C XSLT 1.0](http://www.w3.org/TR/xslt).  
  
 Les classes XML du .NET Framework offrent les avantages suivants :  
  
-   **Productivité** : [LINQ to XML](https://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13) facilite la programmation avec XML et offre une expérience de requête similaire à SQL.  
  
-   **Extensibilité** : Les classes XML du .NET Framework sont extensibles grâce à l'utilisation de classes de base abstraites et de méthodes virtuelles. Par exemple, vous pouvez créer une classe dérivée de la classe <xref:System.Xml.XmlUrlResolver> qui stocke le flux mis en cache sur le disque local.  
  
-   **Architecture enfichable** : Le .NET Framework propose une architecture dans laquelle les composants peuvent s'utiliser réciproquement et où les données peuvent être transmises en continu entre les composants. Par exemple, un magasin de données, tel qu'un objet <xref:System.Xml.XPath.XPathDocument> ou <xref:System.Xml.XmlDocument>, peut être transformé à l'aide de la classe <xref:System.Xml.Xsl.XslCompiledTransform>, et la sortie peut ensuite être soit transmise sous la forme de flux à un autre magasin, soit retournée sous la forme d'un flux à partir d'un service web.  
  
-   **Performances** Pour améliorer les performances des applications, certaines des classes XML du .NET Framework prennent en charge un modèle basé sur les flux de données ayant les caractéristiques suivantes :  
  
    -   Mise en cache minimale pour une analyse avant uniquement et de type pull (<xref:System.Xml.XmlReader>).  
  
    -   Validation avant uniquement (<xref:System.Xml.XmlReader>).  
  
    -   Navigation par curseur qui minimise la création de nœuds à un seul nœud virtuel, tout en permettant l'accès aléatoire au document (<xref:System.Xml.XPath.XPathNavigator>).  
  
     Pour de meilleures performances chaque fois que le traitement XSLT est nécessaire, vous pouvez utiliser la classe <xref:System.Xml.XPath.XPathDocument> qui est un magasin optimisé en lecture seule pour les requêtes XPath, conçu pour fonctionner de manière efficace avec la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   **Intégration à ADO.NET** : les classes XML et [ADO.NET](../../../../docs/framework/data/adonet/index.md) sont étroitement intégrés afin de rassembler les données relationnelles et XML. La classe <xref:System.Data.DataSet> est un cache en mémoire de données extraites d'une base de données. La classe <xref:System.Data.DataSet> a la capacité de lire et d'écrire du XML à l'aide des classes <xref:System.Xml.XmlReader> et <xref:System.Xml.XmlWriter>, de rendre persistante sa structure de schéma relationnel interne sous la forme de schémas XML (XSD) et de déduire la structure de schéma d'un document XML.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Options de traitement XML](../../../../docs/standard/data/xml/xml-processing-options.md)  
 Présente les options de traitement des données XML.  
  
 [Traitement de données XML en mémoire](../../../../docs/standard/data/xml/processing-xml-data-in-memory.md)  
 Présente les trois modèles de traitement des données XML en mémoire. [LINQ to XML](https://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13), la classe <xref:System.Xml.XmlDocument> (basée sur le DOM (Document Object Model) W3C) et la classe <xref:System.Xml.XPath.XPathDocument> (basée sur le modèle de données XPath).  
  
 [Transformations XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)  
 Décrit comment utiliser le processeur XSLT.  
  
 [Modèle Objet du schéma (SOM) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)  
 Décrit les classes utilisées pour créer et manipuler des schémas XML (XSD) en fournissant une classe <xref:System.Xml.Schema.XmlSchema> pour le chargement et la modification d'un schéma.  
  
 [Intégration de XML aux données relationnelles et à ADO.NET](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)  
 Décrit comment le .NET Framework permet un accès synchrone en temps réel aux représentations relationnelles et hiérarchiques des données via l'objet <xref:System.Data.DataSet> et l'objet <xref:System.Xml.XmlDataDocument>.  
  
 [Gestion d’espaces de noms dans un document XML](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)  
 Décrit comment la classe <xref:System.Xml.XmlNamespaceManager> est utilisée pour stocker et gérer des informations d'espace de noms.  
  
 [Prise en charge du type dans les classes System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)  
 Décrit comment les types de données XML sont mappés aux types CLR, comment convertir des types de données XML, ainsi que d'autres fonctionnalités de prise en charge des types dans les classes <xref:System.Xml>.  
  
## <a name="related-sections"></a>Rubriques connexes  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 Présente des informations sur la manière d'accéder à des données à l'aide d'ADO.NET.  
  
 [Sécurité](../../../../docs/standard/security/index.md)  
 Offre une vue d'ensemble du système de sécurité .NET Framework.  
  