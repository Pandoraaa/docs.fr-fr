---
title: '&lt;resolver&gt;'
ms.date: 03/30/2017
ms.assetid: 0c00200c-f135-4e5c-a024-76b72bcbc021
ms.openlocfilehash: 48b6b6ca315f7ab63a8f7a64b97167fa04fe1e4e
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44180798"
---
# <a name="ltresolvergt"></a>&lt;resolver&gt;
Spécifie un programme de résolution d'homologue utilisé pour résoudre un ID de maille d'homologues en un jeu d'adresses de nœuds d'homologues représentant plusieurs nœuds faisant partie de la maille.  
  
 \<system.ServiceModel>  
\<liaisons >  
\<netPeerBinding>  
\<liaison >  
\<resolver>  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<resolver mode="Auto/Custom/Pnrp"  
   referralPolicy="DoNotShare/Service/Share">  
</resolver>  
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|  
|---------------|-----------------|  
|`mode`|Chaîne qui spécifie si l'instance du programme de résolution d'homologue associée à ce service est spécifique au PNRP, à un programme de résolution personnalisé ou si elle est déterminée automatiquement. Cet attribut est de type <xref:System.ServiceModel.PeerResolvers.PeerResolverMode>.|  
|`referralPolicy`|Chaîne qui spécifie la manière dont les références sont partagées parmi des homologues. Cet attribut est de type <xref:System.ServiceModel.PeerResolvers.PeerReferralPolicy>.|  
  
### <a name="child-elements"></a>Éléments enfants  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<en-têtes >](../../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)|Spécifie les paramètres pour un service de programme de résolution d'homologue personnalisé.|  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<liaison >](../../../../../docs/framework/misc/binding.md)|Définit toutes les fonctions de liaison de la [ \<netPeerTcpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md).|  
  
## <a name="remarks"></a>Notes  
 Un programme de résolution de nom d'homologue est un service de découverte utilisé par les canaux homologues afin de rechercher des nœuds d'homologues faisant partie d'une maille d'homologues. Il est également utilisé pour « inscrire » un nœud avec un maillage d'homologue, le mécanisme par lequel le nœud homologue est connu et disponible à partir du maillage d'homologue. Pour plus d’informations sur les programmes de résolution homologues, consultez [programmes de résolution homologues](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.PeerResolver>  
 <xref:System.ServiceModel.PeerResolvers.PeerResolverSettings>  
 <xref:System.ServiceModel.NetPeerTcpBinding.Resolver%2A>  
 <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Resolver%2A>  
 <xref:System.ServiceModel.Configuration.PeerResolverElement>  
 [Programmes de résolution d’homologue](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md)  
 [Ajout d’un programme de résolution personnalisé à une Application PeerChannel](https://msdn.microsoft.com/library/12aa3787-2962-439c-ad27-46523c8b0419)
