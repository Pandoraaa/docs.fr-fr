---
title: '&lt;securityTokenHandlers&gt;'
ms.date: 03/30/2017
ms.assetid: f11a631d-4094-4e11-bb03-4ede74b30281
author: BrucePerlerMS
ms.openlocfilehash: e63f02add81495e474b59b6c5cc090bd69add3d2
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47206170"
---
# <a name="ltsecuritytokenhandlersgt"></a>&lt;securityTokenHandlers&gt;
Spécifie une collection de gestionnaires de jetons de sécurité qui sont inscrits avec le point de terminaison.  
  
 \<system.identityModel>  
\<identityConfiguration >  
\<securityTokenHandlers>  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|  
|---------------|-----------------|  
|name|Spécifie le nom d’une collection de gestionnaires de jetons. Les seules valeurs reconnues par le framework sont « ActAs » et « OnBehalfOf ». Si les collections de gestionnaires de jetons sont spécifiées avec une de ces noms, la collection sera utilisée lors de traitement ActAs ou OnBehalfOf jetons respectivement.|  
  
### <a name="child-elements"></a>Éléments enfants  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|Ajoute un gestionnaire de jetons de sécurité à la collection de gestionnaires de jetons.|  
|[\<clear>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md)|Efface tous les gestionnaires de jetons de sécurité à partir de la collection de gestionnaires de jetons.|  
|[\<remove>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md)|Supprime un gestionnaire de jetons de sécurité de la collection de gestionnaires de jetons.|  
|[\<securityTokenHandlerConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fournit la configuration de la collection de gestionnaires de jetons.|  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Spécifie les paramètres de l’identité de niveau de service.|  
  
## <a name="remarks"></a>Notes  
 Vous pouvez spécifier une ou plusieurs collections nommées de gestionnaires de jetons de sécurité dans une configuration de service. Vous pouvez spécifier un nom pour une collection en utilisant la `name` attribut. Les seuls noms qui gère l’infrastructure sont « ActAs » et « OnBehalfOf ». Si les gestionnaires existent dans ces collections, elles sont utilisées par un service de jeton de sécurité (STS) au lieu des gestionnaires par défaut lors du traitement `ActAs` et `OnBehalfOf` jetons.  
  
 Par défaut, la collection est remplie avec les types de gestionnaires suivants : <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>, et <xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>. Vous pouvez modifier la collection à l’aide de la `<add>`, `<remove>`, et `<clear>` éléments. Vous devez vous assurer qu’uniquement un seul gestionnaire de n’importe quel type particulier existe dans la collection. Par exemple, si vous dérivez un gestionnaire à partir de la <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> de classe, soit votre gestionnaire ou le <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> peut être configuré dans une collection unique, mais pas les deux.  
  
 Utilisez le `<securityTokenHandlerConfiguration>` élément pour spécifier les paramètres de configuration pour les gestionnaires dans la collection. Paramètres spécifiés par cet élément remplacent celles spécifiées sur le service via le [ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) élément. Certains gestionnaires (y compris les différents types de gestionnaire intégré) peuvent prendre en charge une configuration supplémentaire via un élément enfant de le `<add>` élément. Les paramètres spécifiés sur un gestionnaire remplacent les paramètres équivalents spécifiés sur la collection ou le service.
