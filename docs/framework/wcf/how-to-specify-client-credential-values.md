---
title: "Comment : spécifier des valeurs d'informations d'identification du client"
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 82293d7f-471a-4549-8f19-0be890e7b074
ms.openlocfilehash: 9625400b855492ead12a5a2f1fa74f10164f6cdd
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33806642"
---
# <a name="how-to-specify-client-credential-values"></a>Comment : spécifier des valeurs d'informations d'identification du client
À l’aide de Windows Communication Foundation (WCF), le service peut spécifier la manière dont un client est authentifié auprès du service. Par exemple, un service peut stipuler que le client soit authentifié avec un certificat.  
  
### <a name="to-determine-the-client-credential-type"></a>Pour déterminer le type d'informations d'identification du client  
  
1.  Récupérez les métadonnées à partir du point de terminaison des métadonnées du service. Les métadonnées se composent généralement de deux fichiers : le code client dans le langage de programmation de votre choix (la valeur par défaut est Visual C#) et un fichier de configuration XML. L'une des manières permettant de récupérer des métadonnées consiste à utiliser l'outil Svcutil.exe pour retourner le code client et la configuration cliente. Pour plus d’informations, consultez [récupérer des métadonnées](../../../docs/framework/wcf/feature-details/retrieving-metadata.md) et [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
2.  Ouvrez le fichier de configuration XML. Si vous utilisez l'outil Svcutil.exe, le nom par défaut du fichier est Output.config.  
  
3.  Rechercher les  **\<sécurité >** élément avec la **mode** attribut (**< mode de sécurité =** `MessageOrTransport` **>** où `MessageOrTransport` est défini sur l’un des modes de sécurité.  
  
4.  Recherchez l'élément enfant qui correspond à la valeur de mode. Par exemple, si le mode est défini sur **Message**, recherchez le  **\<message >** élément contenu dans le  **\<sécurité >** élément.  
  
5.  Notez la valeur affectée à la **clientCredentialType** attribut. La valeur réelle dépend du mode utilisé, du transport ou du message.  
  
 Le code XML suivant montre la configuration pour un client utilisant la sécurité du message et nécessitant un certificat pour authentifier le client.  
  
```xml  
<security mode="Message">  
    <transport clientCredentialType="Windows" proxyCredentialType="None"  
        realm="" />  
     <message clientCredentialType="Certificate" negotiateServiceCredential="true"  
    algorithmSuite="Default" establishSecurityContext="true" />  
</security>  
```  
  
## <a name="example-tcp-transport-mode-with-certificate-as-client-credential"></a>Exemple : mode de transport TCP avec certificat comme informations d'identification du client  
 Cet exemple définit le mode de sécurité sur le mode Transport et définit la valeur d'informations d'identification du client sur un certificat X.509. Les procédures suivantes montrent comment définir la valeur d'information d'identification du client sur le client dans le code et dans la configuration. Cela suppose que vous avez utilisé le [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) pour retourner les métadonnées (code et configuration) à partir du service. Pour plus d’informations, consultez [Comment : créer un Client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
#### <a name="to-specify-the-client-credential-value-on-the-client-in-code"></a>Pour spécifier la valeur d'information d'identification du client sur le client dans le code  
  
1.  Utilisez le [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) pour générer le code et la configuration du service.  
  
2.  Créez une instance du client WCF à l’aide du code généré.  
  
3.  Sur la classe de client, affectez à la propriété <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> de la classe <xref:System.ServiceModel.ClientBase%601> une valeur appropriée. Cet exemple affecte à la propriété un certificat X.509 à l'aide de la méthode <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> de la classe <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>.  
  
     [!code-csharp[c_TcpService#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_tcpservice/cs/source.cs#4)]
     [!code-vb[c_TcpService#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_tcpservice/vb/source.vb#4)]  
  
     Vous pouvez utiliser n'importe lesquelles des énumérations de la classe <xref:System.Security.Cryptography.X509Certificates.X509FindType>. Le nom du sujet est utilisé ici au cas où le certificat serait modifié (en raison d'une date d'expiration). L'utilisation du nom du sujet permet à l'infrastructure de retrouver le certificat.  
  
#### <a name="to-specify-the-client-credential-value-on-the-client-in-configuration"></a>Pour spécifier la valeur d'information d'identification du client sur le client dans la configuration  
  
1.  Ajouter un [ \<comportement >](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) élément à la [ \<comportements >](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) élément.  
  
2.  Ajouter un [ \<clientCredentials >](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) élément à la [ \<comportements >](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) élément. Assurez-vous d'affecter à l'attribut `name` requis une valeur appropriée.  
  
3.  Ajouter un [ \<clientCertificate >](../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-servicecredentials.md) élément à la [ \<clientCredentials >](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) élément.  
  
4.  Affectez aux attributs suivants des valeurs appropriées : `storeLocation`, `storeName`, `x509FindType` et `findValue`, comme illustré dans le code suivant. Pour plus d’informations sur les certificats, consultez [Utilisation de certificats](../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
    ```xml  
    <behaviors>  
       <endpointBehaviors>  
          <behavior name="endpointCredentialBehavior">  
            <clientCredentials>  
              <clientCertificate findValue="Contoso.com"   
                                 storeLocation="LocalMachine"  
                                 storeName="TrustedPeople"  
                                 x509FindType="FindBySubjectName" />  
            </clientCredentials>  
          </behavior>  
       </endpointBehaviors>  
    </behaviors>  
    ```  
  
5.  Lorsque vous configurez le client, spécifiez le comportement en définissant l'attribut `behaviorConfiguration` de l'élément `<endpoint>`, comme illustré dans le code suivant. L’élément de point de terminaison est un enfant de la [ \<client >](../../../docs/framework/configure-apps/file-schema/wcf/client.md) élément. Spécifiez également le nom de la configuration de liaison en affectant à l'attribut `bindingConfiguration` la liaison pour le client. Si vous utilisez un fichier de configuration généré, le nom de la liaison est généré automatiquement. Dans cet exemple, le nom est `"tcpBindingWithCredential"`.  
  
    ```xml  
    <client>  
      <endpoint name =""  
                address="net.tcp://contoso.com:8036/aloha"  
                binding="netTcpBinding"  
                bindingConfiguration="tcpBindingWithCredential"  
                behaviorConfiguration="endpointCredentialBehavior" />  
    </client>  
    ```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.NetTcpBinding>  
 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>  
 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>  
 <xref:System.ServiceModel.ClientBase%601>  
 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>  
 [Programmation de la sécurité dans WCF](../../../docs/framework/wcf/feature-details/programming-wcf-security.md)  
 [Sélection d’un type d’informations d’identification](../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)  
 [Outil ServiceModel Metadata Utility (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)  
 [Utilisation des certificats](../../../docs/framework/wcf/feature-details/working-with-certificates.md)  
 [Guide pratique pour créer un client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)  
 [\<netTcpBinding>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)  
 [\<sécurité >](../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)  
 [\<message>](../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-nettcpbinding.md)  
 [\<behavior>](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)  
 [\<comportements >](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
 [\<clientCertificate >](../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-servicecredentials.md)  
 [\<clientCredentials>](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)
