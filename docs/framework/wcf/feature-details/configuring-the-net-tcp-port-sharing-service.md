---
title: Configuration du service de partage de ports Net.TCP
ms.date: 03/30/2017
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
ms.openlocfilehash: 99585bb05364b6b0b3ee093823dc599519c8a12a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33489516"
---
# <a name="configuring-the-nettcp-port-sharing-service"></a>Configuration du service de partage de ports Net.TCP
Les services auto-hébergés qui utilisent le transport Net.TCP peuvent contrôler plusieurs paramètres avancés, tels que `ListenBacklog` et `MaxPendingAccepts`, qui gouvernent le comportement du socket TCP sous-jacent utilisé pour la communication réseau. Toutefois, pour chaque socket, ces paramètres ne s'appliquent qu'au niveau de la liaison si la liaison de transport a désactivé le partage de port, activé par défaut.  
  
 Lorsqu'une liaison net.tcp active le partage de port (en définissant `portSharingEnabled =true` sur l'élément de liaison de transport), elle autorise implicitement un processus externe (à savoir, l'exécutable SMSvcHost.exe, qui héberge le service de partage de ports Net.TCP) à gérer le socket TCP pour son compte. Par exemple, lorsque vous utilisez TCP, spécifiez :  
  
```xml  
    <tcpTransport   
        portSharingEnabled="true"  
/>  
```  
  
 Dans le cas de cette configuration, tous les paramètres de socket spécifiés sur l'élément de liaison de transport du service sont ignorés en faveur des paramètres de socket spécifiés par SMSvcHost.exe.  
  
 Pour configurer SMSvcHost.exe, créez un fichier de configuration XML nommé SmSvcHost.exe.config et placez-le dans le même répertoire physique que l'exécutable SMSvcHost.exe (par exemple, C:\Windows\Microsoft.NET\Framework\v4.5).  
  
 L'exemple suivant montre un exécutable SMSvcHost.exe.config avec les paramètres par défaut pour toutes les valeurs configurables déclarées explicitement.  
  
```xml  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!—16 * # of processors -->  
          maxPendingAccepts="4"<!— 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!—30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
</configuration>  
```  
  
## <a name="when-to-modify-smsvchostexeconfig"></a>Quand modifier SMSvcHost.exe.config  
 En général, il convient de prêter une attention particulière à la modification du contenu du fichier SMSvcHost.exe.config, parce que tout paramètre de configuration spécifié dans ce fichier affecte l'ensemble des services sur un ordinateur utilisant le service de partage de ports Net.TCP. Cela inclut les applications sous [!INCLUDE[wv](../../../../includes/wv-md.md)] qui utilisent les fonctionnalités d'activation TCP du service d'activation de processus de Windows (WAS).  
  
 Toutefois, il est parfois nécessaire de modifier la configuration par défaut du service de partage de ports Net.TCP. Par exemple, la valeur par défaut pour `maxPendingAccepts` est 4 * nombre de processeurs. Les serveurs qui hébergent un grand nombre des services utilisant le partage de port doivent augmenter cette valeur pour atteindre le débit maximal. La valeur par défaut `maxPendingConnections` est 100. Vous devez également envisager d'augmenter cette valeur s'il existe plusieurs clients simultanés appelant le service et le service supprime des connexions clientes.  
  
 SMSvcHost.exe.config contient également des informations concernant les identités de processus qui peuvent utiliser le service de partage de ports. Lorsqu'un processus se connecte au service de partage de ports pour utiliser un port TCP partagé, l'identité de processus de la connexion est vérifiée dans une liste répertoriant les identités autorisées à utiliser le service. Ces identités sont spécifiées en tant qu’identificateurs de sécurité (SID) dans le \<allowAccounts > section du fichier SMSvcHost.exe.config. Par défaut, l'autorisation d'utiliser le service de partage de ports est accordée aux comptes système (LocalService, LocalSystem et NetworkService) ainsi qu'aux membres du groupe Administrateurs. Les applications qui autorisent un processus exécuté en tant qu'autre identité (par exemple, une identité de l'utilisateur) à se connecter au service de partage de ports doivent ajouter explicitement le SID approprié au fichier SMSvcHost.exe.config (ces modifications ne sont appliquées que lorsque le processus SMSvc.exe est redémarré).  
  
> [!NOTE]
>  Sous les systèmes [!INCLUDE[wv](../../../../includes/wv-md.md)] avec contrôle de compte utilisateur (UAC) activé, les utilisateurs locaux requièrent des autorisations élevées même si leur compte est un membre du groupe Administrateurs. Pour autoriser ces utilisateurs d’utiliser le service sans élévation, le SID de l’utilisateur (ou le SID d’un groupe dans lequel l’utilisateur est membre) de partage de ports doit être ajouté explicitement à la \<allowAccounts > section du fichier SMSvcHost.exe.config.  
  
> [!WARNING]
>  Le fichier SMSvcHost.exe.config par défaut spécifie un `etwProviderId` personnalisé pour empêcher le traçage SMSvcHost.exe d'interférer avec les traces de service.  
  
## <a name="see-also"></a>Voir aussi  
 [\<NET.TCP >](../../../../docs/framework/configure-apps/file-schema/wcf/net-tcp.md)
