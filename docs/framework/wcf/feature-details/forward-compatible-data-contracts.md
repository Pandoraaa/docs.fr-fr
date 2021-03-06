---
title: Contrats de données à compatibilité ascendante
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], forward compatibility
ms.assetid: 413c9044-26f8-4ecb-968c-18495ea52cd9
ms.openlocfilehash: 95a72d5d09538bc6f663f2376c7f8f928909cd57
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33492204"
---
# <a name="forward-compatible-data-contracts"></a>Contrats de données à compatibilité ascendante
Une fonctionnalité de la Windows Communication Foundation (WCF) système de contrat de données est les contrats permettre évoluer au fil du temps rupture. Autrement dit, un client avec une version antérieure d'un contrat de données peut communiquer avec un service disposant d'une version plus récente du même contrat de données, ou un client avec une version plus récente d'un contrat de données peut communiquer avec une version antérieure du même contrat de données. Pour plus d’informations, consultez [meilleures pratiques : contrôle de version de contrat de données](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
 Vous pouvez appliquer la plupart des fonctionnalités de suivi des versions dès que besoin lorsque de nouvelles versions d’un contrat de données existant sont créées. Toutefois, une fonctionnalité de contrôle de version, *aller-retour*, doit être construite dans le type de la première version afin de fonctionner correctement.  
  
## <a name="round-tripping"></a>Aller-retour  
 L'aller-retour se produit lorsque des données passent d'une nouvelle version à une version ancienne et reviennent à la nouvelle version d'un contrat de données. L'aller-retour garantit qu'aucunes données ne sont perdues. L'activation de l'aller-retour rend le type compatible en aval avec toutes les modifications futures prises en charge par le modèle du suivi des versions du contrat de données.  
  
 Pour activer l'aller-retour pour un type spécifique, ce dernier doit implémenter l'interface <xref:System.Runtime.Serialization.IExtensibleDataObject>. L'interface contient une propriété, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> (retournant le type <xref:System.Runtime.Serialization.ExtensionDataObject>). La propriété stocke les données des futures versions du contrat de données qui est inconnu de la version actuelle.  
  
### <a name="example"></a>Exemple  
 Le contrat des données suivant n'est pas compatible en aval avec les futures modifications.  
  
 [!code-csharp[C_DataContract#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#7)]
 [!code-vb[C_DataContract#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#7)]  
  
 Pour rendre ce type compatible avec les futures modifications (telles que l'ajout d'un nouveau membre de données nommé « numéroTél »), implémentez l'interface <xref:System.Runtime.Serialization.IExtensibleDataObject>.  
  
 [!code-csharp[C_DataContract#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#8)]
 [!code-vb[C_DataContract#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#8)]  
  
 Lorsque l’infrastructure WCF rencontre des données qui ne fait pas partie du contrat de données d’origine, les données sont stockées dans la propriété et conservées. Elles ne sont pas traitées d'aucune autre façon, sauf pour stockage temporaire. Si l'objet est renvoyé là d'où il est venu, les données d'origine (inconnues) sont également retournées. Par conséquent, les données ont fait aller-retour au point de terminaison d'origine sans perte. Toutefois, notez que si le point de terminaison d'origine exige que les données soient traitées, cette attente n'est pas satisfaite, et le point de terminaison doit détecter d'une façon ou d'une autre la modification et s'en accommoder.  
  
 Le type <xref:System.Runtime.Serialization.ExtensionDataObject> ne contient pas de méthodes ou de propriétés publiques. Il est donc impossible d'accéder directement aux données stockées à l'intérieur de la propriété <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>.  
  
 La fonctionnalité d'aller-retour peut être désactivée, soit en affectant à `ignoreExtensionDataObject` la valeur `true` dans le constructeur <xref:System.Runtime.Serialization.DataContractSerializer>, soit en affectant à la propriété <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> la valeur `true` sur <xref:System.ServiceModel.ServiceBehaviorAttribute>. Lorsque cette fonctionnalité est désactivée, le désérialiseur ne complète pas la propriété <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>, et le sérialiseur n'émet pas le contenu de la propriété.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Runtime.Serialization.IExtensibleDataObject>  
 <xref:System.Runtime.Serialization.ExtensionDataObject>  
 [Gestion de version des contrats de données](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)  
 [Bonnes pratiques : gestion des versions des contrats de données](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)
