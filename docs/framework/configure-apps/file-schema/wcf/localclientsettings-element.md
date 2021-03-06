---
title: '&lt;localClientSettings&gt;, élément'
ms.date: 03/30/2017
ms.assetid: 4680ace5-f4e1-4fcb-b9d8-a4a4af5cd7ae
ms.openlocfilehash: a960a18c472bed64609947220dffedf9ec90945c
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32750945"
---
# <a name="ltlocalclientsettingsgt-element"></a>&lt;localClientSettings&gt;, élément
Spécifie les paramètres de sécurité d’un client local pour cette liaison.  
  
 \<system.serviceModel>  
\<liaisons >  
\<customBinding >  
\<liaison >  
\<sécurité >  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<security>  
   <localClientSettings cacheCookies="Boolean"  
      cookieRenewalThresholdPercentage="Integer"  
      detectReplays="Boolean"  
      maxClockSkew="TimeSpan"  
      maxCookieCachingTime="TimeSpan"  
      reconnectTransportOnFailure="Boolean"  
      replayCacheSize="Integer"  
      replayWindow="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      timestampValidityDuration="TimeSpan" />  
</security>  
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|  
|---------------|-----------------|  
|`cacheCookies`|Valeur booléenne qui spécifie si la mise en cache de cookie est activée. La valeur par défaut est `false`.|  
|`cookieRenewalThresholdPercentage`|Entier qui spécifie le pourcentage maximal des cookies qui peuvent être renouvelés. Cette valeur doit être comprise entre 0 et 100. La valeur par défaut est 90.|  
|`detectReplays`|Valeur booléenne qui spécifie si les attaques par relecture contre le canal sont détectées et traitées automatiquement. La valeur par défaut est `false`.|  
|`maxClockSkew`|<xref:System.TimeSpan> qui spécifie la différence de temps maximale entre les horloges système des deux parties communicantes. La valeur par défaut est « 00:05:00 ».<br /><br /> Lorsque la valeur par défaut est définie, le récepteur accepte des messages dont l'horodatage d'envoi diffère au maximum de 5 minutes de son horodatage de réception. Les messages qui échouent au test de l'heure d'envoi sont rejetés. Ce paramètre est utilisé conjointement à l'attribut `replayWindow`.|  
|`maxCookieCachingTime`|<xref:System.TimeSpan> qui spécifie la durée de vie maximale des cookies. La valeur par défaut est « 10675199.02:48:05.4775807 ».|  
|`reconnectTransportOnFailure`|Valeur booléenne qui spécifie si des connexions utilisant la messagerie WS-Reliable tentent une reconnexion après des incidents de transport. La valeur par défaut est `true`, ce qui signifie que le nombre de tentatives de reconnexion est infini. Le cycle s'arrête si le délai d'attente expire suite à une inactivité prolongée, après laquelle le canal lève une exception lorsqu'il ne peut pas être reconnecté.|  
|`replayCacheSize`|Entier positif qui spécifie le nombre de pointeurs en cache utilisés pour la détection de relecture. Si cette limite est dépassée, le pointeur le plus ancien est supprimé et un pointeur est créé pour le nouveau message. La valeur par défaut est 500000.|  
|`replayWindow`|<xref:System.TimeSpan> qui spécifie la durée de validité des pointeurs de messages individuels.<br /><br /> Une fois cette durée écoulée, un message envoyé avec le même pointeur que celui envoyé précédemment ne sera pas accepté. Cet attribut est utilisé conjointement à l'attribut `maxClockSkew` pour empêcher des attaques par relecture. Un intrus pourrait relire un message une fois que sa fenêtre de relecture a expiré. Toutefois, ce message échouerait au test `maxClockSkew` qui rejette les messages portant un horodatage d'envoi qui diffère au maximum d'une heure par rapport à l'horodatage de réception du message.|  
|`sessionKeyRenewalInterval`|<xref:System.TimeSpan> qui spécifie le délai d'attente au terme duquel l'initiateur renouvellera la clé de la session de sécurité. La valeur par défaut est « 10:00:00 ».|  
|`sessionKeyRolloverInterval`|<xref:System.TimeSpan> qui spécifie la période de validité d'une clé de session précédente sur les messages entrants pendant un renouvellement de clé. La valeur par défaut est « 00:05:00 ».<br /><br /> Pendant un renouvellement de clé, le client et le serveur doivent toujours envoyer des messages à l'aide de la clé disponible la plus récente. Les deux correspondants doivent accepter des messages entrants sécurisés avec la clé de session précédente jusqu'à l'expiration de l'heure de substitution.|  
|`timestampValidityDuration`|<xref:System.TimeSpan> positif qui spécifie la durée de validité d'un horodatage. La valeur par défaut est « 00:15:00 ».|  
  
### <a name="child-elements"></a>Éléments enfants  
 Aucun  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<sécurité >](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|Spécifie les options de sécurité d’une liaison personnalisée.|  
|[\<secureConversationBootstrap >](../../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)|Spécifie les valeurs par défaut utilisées pour initialiser un service de conversation sécurisé.|  
  
## <a name="remarks"></a>Notes  
 Les paramètres sont locaux dans le sens où ils ne dérivent pas de la stratégie de sécurité du service.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement>  
 <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalClientSettings%2A>  
 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A>  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 [Liaisons](../../../../../docs/framework/wcf/bindings.md)  
 [Extension de liaisons](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [Liaisons personnalisées](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)  
 [Guide pratique pour créer une liaison personnalisée à l’aide de SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 [Sécurité de liaison personnalisée](../../../../../docs/framework/wcf/samples/custom-binding-security.md)
