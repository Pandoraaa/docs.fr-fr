---
title: Fonctionnalités spécifiques à Windows Workflow Foundation
ms.date: 03/30/2017
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
ms.openlocfilehash: 6929150f786f0d6b4a5887eb5c0758ebcfdd411c
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48846004"
---
# <a name="windows-workflow-foundation-feature-specifics"></a>Fonctionnalités spécifiques à Windows Workflow Foundation
[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] ajoute un certain nombre de fonctionnalités à Windows Workflow Foundation. Ce document décrit quelques-unes de ces nouvelles fonctionnalités et donne des détails relatifs à certains scénarios dans lesquels elles peuvent être utiles.  
  
## <a name="messaging-activities"></a>Activités de messagerie  
 Les activités de messagerie (<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.ReceiveReply>) sont utilisés pour envoyer et recevoir des messages WCF à partir de votre flux de travail.  <xref:System.ServiceModel.Activities.Receive> et <xref:System.ServiceModel.Activities.SendReply> activités sont utilisées pour former une opération de service Windows Communication Foundation (WCF) qui est exposée via WSDL comme les services web WCF standards.  <xref:System.ServiceModel.Activities.Send> et <xref:System.ServiceModel.Activities.ReceiveReply> permettent de consommer un service web similaire à un service WCF <xref:System.ServiceModel.ChannelFactory>; une **ajouter une référence de Service** expérience existe également pour Workflow Foundation qui génère des activités préconfigurées.  
  
### <a name="getting-started-with-messaging-activities"></a>Activités de messagerie - Mise en route  
  
-   Dans Visual Studio 2012, créez un projet d’Application de Service de Workflow WCF. Une combinaison <xref:System.ServiceModel.Activities.Receive> et <xref:System.ServiceModel.Activities.SendReply> sera placée sur votre zone de dessin.  
  
-   Avec le bouton droit sur le projet, puis sélectionnez **ajouter une référence de Service**.  Pointer vers un WSDL de service web existant et cliquez sur **OK**.  Générez votre projet pour afficher les activités générées (implémentées à l’aide <xref:System.ServiceModel.Activities.Send> et <xref:System.ServiceModel.Activities.ReceiveReply>) dans votre boîte à outils.
  
-   [Documentation des services de workflow](../wcf/feature-details/workflow-services.md)
  
### <a name="messaging-activities-example-scenario"></a>Exemple de scénario d'activités de messagerie  
 Un `BestPriceFinder` service appelle plusieurs services de compagnies aériennes afin de trouver le tarif d’un itinéraire particulier.  Implémentation de ce scénario vous oblige à utiliser les activités de message pour recevoir la demande de prix, de récupérer les tarifs à partir des services principaux et de répondre à la demande de prix en indiquant le meilleur tarif.  Elle vous oblige également à utiliser d’autres activités out-of-box pour créer la logique métier pour calculer le meilleur tarif.  
  
## <a name="workflowservicehost"></a>WorkflowServiceHost  
 Le <xref:System.ServiceModel.WorkflowServiceHost> est l’hôte de flux de travail out-of-box qui prend en charge plusieurs instances, la configuration et la messagerie WCF (bien que les flux de travail ne sont pas requis pour utiliser la messagerie afin d’être hébergés).  Il permet également la persistance, le suivi et le contrôle de l'instance par un ensemble de comportements de service.  Tout comme de WCF <xref:System.ServiceModel.ServiceHost>, le <xref:System.ServiceModel.WorkflowServiceHost> peut être auto-hébergé dans une application console/WinForms/WPF ou le service de Windows ou hébergé sur le web (comme un fichier .xamlx) dans IIS ou WAS.  
  
### <a name="getting-started-with-workflow-service-host"></a>Mise en route avec l'hôte du service de workflow  
  
-   Dans Visual Studio 2010, créez un projet d’Application de Service de Workflow WCF : ce projet est configuré pour utiliser <xref:System.ServiceModel.WorkflowServiceHost> dans un environnement d’hôte sur le web.  
  
-   Pour héberger un flux de travail sans rapport avec la messagerie, ajoutez un <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> personnalisé qui créera l'instance en fonction d'un message.  
  
-   Il est possible de contrôler des instances de flux de travail (de les suspendre ou de les arrêter, par exemple) en ajoutant un <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> au <xref:System.ServiceModel.WorkflowServiceHost>, puis en utilisant un <xref:System.ServiceModel.Activities.WorkflowControlClient>.  
  
-   Vous trouverez des exemples de <xref:System.ServiceModel.WorkflowServiceHost> dans les sections suivantes :  
  
    -   [Exécution](samples/execution.md)
  
    -   Application : [suspendue de gestion de l’Instance](samples/suspended-instance-management.md)  
  
-   [Vue d’ensemble des services de Workflow d’hébergement](../wcf/feature-details/hosting-workflow-services-overview.md)  
  
### <a name="workflowservicehost-scenario"></a>Scénario WorkflowServiceHost  
 Un service BestPriceFinder appelle plusieurs services de compagnies aériennes afin de trouver le tarif d’un itinéraire particulier.  Implémentation de ce scénario vous oblige à héberger le flux de travail dans <xref:System.ServiceModel.WorkflowServiceHost>.  Il utilise également les activités de message pour recevoir la demande de prix, de récupérer les tarifs à partir des services principaux et de répondre à la demande de prix en indiquant le meilleur tarif.  
  
## <a name="correlation"></a>Corrélation  
 Une corrélation correspond à l'un des deux concepts suivants :  
  
-   manière de regrouper des messages ; autrement dit, la relation entre un message de demande et sa réponse ;  
  
-   manière de mapper des données à une instance de service.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Pour démarrer une corrélation, créez un projet dans Visual Studio. Créez une variable de type <xref:System.ServiceModel.Activities.CorrelationHandle>.  
  
-   À titre d'exemple de corrélation utilisé pour regrouper des messages, citons une corrélation demande-réponse.  
  
    -   Sur un <xref:System.ServiceModel.Activities.Receive> activité, cliquez sur le <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> propriété et ajoutez un <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> à l’aide du CorrelationHandle créé dans la première étape ci-dessus.  
  
    -   Créer un <xref:System.ServiceModel.Activities.SendReply> activité en cliquant sur le <xref:System.ServiceModel.Activities.Receive> et en cliquant sur « Create SendReply ». Collez-la dans votre flux de travail à la suite de l'activité <xref:System.ServiceModel.Activities.Receive>.  
  
-   Une corrélation basée sur le contenu qui mappe des données (un numéro de commande, par exemple) à une instance de flux de travail particulière constitue un exemple de mappage de données à une instance de service.  
  
    -   Dans une activité de messagerie, cliquez sur la propriété `CorrelationInitializers` et ajoutez un <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> à l'aide de la variable <xref:System.ServiceModel.Activities.CorrelationHandle> créée ci-dessus. Double-cliquez sur la propriété de votre choix dans le message (par exemple, OrderID) du menu déroulant. Définissez la propriété `CorrelatesWith` avec la variable <xref:System.ServiceModel.Activities.CorrelationHandle> utilisée précédemment. 
  
-   [Documentation conceptuelle de corrélation](../wcf/feature-details/correlation.md)  
  
### <a name="correlation-scenario"></a>Scénario de corrélation  
 Un flux de travail de traitement des commandes est utilisé pour gérer la création de nouvelles commandes et les commandes figurant dans le processus de mise à jour.  Implémentation de ce scénario vous oblige à héberger le flux de travail dans <xref:System.ServiceModel.WorkflowServiceHost> et utiliser les activités de messagerie.  Cela impliquerait également une corrélation basée sur les `orderId` pour vous assurer que les mises à jour sont effectuées dans le flux de travail correct.  
  
## <a name="simplified-configuration"></a>Configuration simplifiée  
 Le schéma de configuration WCF est complexe et fournit aux utilisateurs plusieurs fonctionnalités difficiles à trouver. Dans [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], nous nous sommes concentrés à aider les utilisateurs WCF configurent leurs services avec les fonctionnalités suivantes :  
  
-   Plus besoin de configuration explicite par service. Si vous ne configurez aucune \<service > éléments de votre service et votre service ne définit pas par programmation à n’importe quel point de terminaison, puis un jeu de points de terminaison est ajouté automatiquement à votre service, un pour chaque adresse de base de service et chaque contrat implémenté par votre service.  
  
-   Permet à l’utilisateur de définir pour les comportements et les liaisons WCF des valeurs par défaut qui seront appliquées aux services sans configuration explicite.  
  
-   Les points de terminaison standard définissent les points de terminaison préconfigurés réutilisables qui ont des valeurs fixes pour une ou plusieurs propriétés de point de terminaison (adresse, liaison ou contrat) et permettent la définition de propriétés personnalisées.  
  
-   Enfin, le <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> vous permet d’effectuer une gestion centralisée de la configuration de client WCF, utile dans les scénarios dans lesquels la configuration est sélectionnée ou modifiée après le temps de chargement du domaine application.  
  
### <a name="getting-started"></a>Prise en main  
  
-   [Guide du développeur pour WCF 4.0](https://go.microsoft.com/fwlink/?LinkId=204940)  
  
-   [Fabrique de canaux de configuration](https://go.microsoft.com/fwlink/?LinkId=204941)  
  
-   [Élément de point de terminaison standard](https://go.microsoft.com/fwlink/?LinkId=204942)  
  
-   [Service des améliorations de configuration dans .net Framework 4](https://go.microsoft.com/fwlink/?LinkId=204943)  
  
-   [Erreur utilisateur courante dans .NET 4 : erreur de frappe le nom de Configuration du Service WF/WCF](https://go.microsoft.com/fwlink/?LinkId=204944)  
  
### <a name="simplified-configuration-scenarios"></a>Scénarios de configuration simplifiée  
  
-   Un développeur ASMX expérimenté souhaite commencer à utiliser WCF. Cependant, WCF semble trop compliqué ! Quelles sont les informations dont j'ai besoin pour écrire dans un fichier de configuration ? Dans .NET 4, vous pouvez même décider de ne pas avoir de fichier de configuration du tout.  
  
-   Il est très difficile de configurer et de gérer un ensemble existant de services WCF. Le fichier de configuration contient des milliers de lignes de code XML qui doivent être manipulées avec la plus grande prudence. De l'aide est nécessaire pour réduire la quantité de code afin que ce dernier soit plus facile à gérer.  
  
## <a name="data-contract-resolver"></a>Programme de résolution de contrat de données  
 Dans .NET 3.5, il existait quelques limitations à la conception de types connus :  
  
-   L'ajout de types connus de manière dynamique pendant la sérialisation ou la désérialisation était impossible.  
  
-   Les sérialiseurs n'étaient pas en mesure de gérer des informations xsi:type inconnues.  
  
-   Il n'était pas possible pour les utilisateurs de spécifier le xsi:type qu'ils souhaitaient voir apparaître sur le câble pour, par exemple, réduire la taille d'une instance de sérialisation sur ce dernier.  
  
 Le [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md) résout ces problèmes dans .NET 4.5.  
  
### <a name="getting-started"></a>Prise en main  
  
-   [Documentation des API de programme de résolution de contrat de données](https://go.microsoft.com/fwlink/?LinkId=204946)  
  
-   [Présentation du programme de résolution de contrat de données](https://go.microsoft.com/fwlink/?LinkId=204947)  
  
-   Exemples :  
  
    -   [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md)  
  
    -   [KnownAssemblyAttribute](../../../docs/framework/wcf/samples/knownassemblyattribute.md)  
  
### <a name="data-contract-resolver-scenarios"></a>Scénarios d'un programme de résolution de contrat de données  
  
-   Éviter d'avoir à déclarer des dizaines d'objets <xref:System.Runtime.Serialization.KnownTypeAttribute> dans un service.  
  
-   Réduire la taille d'un objet BLOB XML.  
  
## <a name="flowchart"></a>Organigramme  
 Un organigramme est un paradigme connu permettant la représentation visuelle de problèmes liés à un domaine. Il s'agit d'un nouveau style de flux de contrôle qui a été introduit dans .NET 4. La principale caractéristique d'un organigramme tient dans le fait qu'une seule activité est exécutée à un moment donné. Les organigrammes peuvent représenter des boucles et des alternatives possibles, mais ne peuvent pas, de manière native, représenter l'exécution simultanée de plusieurs nœuds.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Dans Visual Studio 2012, créez une application console de workflow. Ajoutez un organigramme dans le concepteur de workflow.  
  
-   La fonctionnalité d'organigramme utilise les classes suivantes :  
  
    -   <xref:System.Activities.Statements.Flowchart>  
  
    -   <xref:System.Activities.Statements.FlowNode>  
  
    -   <xref:System.Activities.Statements.FlowDecision>  
  
    -   <xref:System.Activities.Statements.FlowStep>  
  
    -   <xref:System.Activities.Statements.FlowSwitch%601>  
  
-   Exemples :  
  
    -   [Gestion des erreurs dans une activité Flowchart à l’aide de TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md) 
  
    -   [Processus d’embauche](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
-   Documentation relative au concepteur :  
  
    -   [Concepteurs d’activités d’organigramme](/visualstudio/workflow-designer/flowchart-activity-designers)  
  
### <a name="flowchart-scenarios"></a>Scénarios d'organigramme  
 Une activité d'organigramme peut permettre d'implémenter un jeu de devinette. Le jeu de devinette est très simple : l'ordinateur sélectionne un nombre aléatoire et le joueur doit deviner ce nombre. Lorsque le joueur fait une proposition, l’ordinateur lui donne un indice (par exemple, « essayez un nombre inférieur »). Si le joueur devine le nombre en moins de 7 tentatives, il reçoit un message de félicitations spécial de l'ordinateur. Ce jeu peut être implémenté avec une combinaison des activités procédurales suivantes :  
  
-   <xref:System.Activities.Statements.Sequence>  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.Switch%601>  
  
-   <xref:System.Activities.Statements.TryCatch>  
  
-   <xref:System.Activities.Statements.Assign%601>  
  
-   <xref:System.Activities.Statements.If>  
  
## <a name="procedural-activities-sequence-if-foreach-switch-assign-dowhile-while"></a>Activités procédurales (Sequence, If, ForEach, Switch, Assign, DoWhile, While)  
 Les activités procédurales fournissent un mécanisme de modélisation d'un flux de contrôle séquentiel en faisant appel à des concepts que connaissent bien les programmeurs. Ces activités permettent les constructions de langage de programmation structurées de manière traditionnelle et, lorsque cela s'avère nécessaire, une parité de langages avec les langages procéduraux courants, tels que C#/VB.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Dans Visual Studio 2012, créez une application console de workflow. Ajoutez des activités procédurales dans le concepteur de workfow.  
  
-   Exemples :  
  
    -   [Processus d’embauche](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
    -   [Processus d’achat d’entreprise](../../../docs/framework/windows-workflow-foundation/samples/corporate-purchase-process.md)  
  
-   Documentation relative au concepteur :  
  
    -   [Concepteur d’activités Parallel](/visualstudio/workflow-designer/parallel-activity-designer)  
  
    -   [ParallelForEach\<T > Concepteur d’activités](/visualstudio/workflow-designer/parallelforeach-t-activity-designer)  
  
### <a name="procedural-activity-scenarios"></a>Scénarios d'activités procédurales  
  
-   <xref:System.Activities.Statements.Parallel>: Un système de gestion documentaire intranet dispose d’un workflow d’approbation de document. Les documents doivent être approuvés par du personnel travaillant dans plusieurs services différents avant d'être publiés sur le réseau intranet. Il n’est pas un ordre établi pour les approbations ; ils peuvent se produire à tout moment, tandis que le document est en phase de « approbation en attente ». Lorsqu’un utilisateur soumet un document à des fins de revue, ce dernier doit être approuvé par son supérieur hiérarchique direct, par l’administrateur de l’intranet et par le responsable de la communication interne.  
  
-   <xref:System.Activities.Statements.ParallelForEach%601> : une application WF gère les achats au sein d'une grande entreprise. Les règles d'entreprise imposent une évaluation de trois fournisseurs différents avant toute planification d'une opération d'achat. Un employé travaillant dans le service Achat sélectionne trois fournisseurs dans la liste des fournisseurs de la société. Une fois que ces fournisseurs ont été sélectionnés et informés, la société attend de recevoir leur offre. L'ordre de réception des offres n'a pas d'importance. Pour implémenter ce scénario dans WF, nous utilisons un <xref:System.Activities.Statements.ParallelForEach%601> qui permettra une recherche au sein de la liste de fournisseurs et demandera une offre de leur part. Une fois que toutes les offres ont été recueillies, la meilleure est sélectionnée et affichée.  
  
## <a name="invokemethod"></a>InvokeMethod  
 L'activité <xref:System.Activities.Statements.InvokeMethod> permet l'appel de méthodes publiques dans des objets ou des types de l'étendue. Elle prend en charge l'appel de méthodes statiques et d'instances avec ou sans paramètres (y compris les tableaux de paramètres), ainsi que les méthodes génériques. Elle permet également l'exécution de la méthode de façon synchrone et de façon asynchrone.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Dans Visual Studio 2012, créez une application console de workflow. Ajoutez une activité <xref:System.Activities.Statements.InvokeMethod> dans le concepteur de workflow et configurez-y des méthodes d'instances et statiques.  
  
-   Documentation relative au concepteur : [Concepteur d’activités InvokeMethod](/visualstudio/workflow-designer/invokemethod-activity-designer)  
  
### <a name="invokemethod-scenarios"></a>Scénarios InvokeMethod  
  
-   Une méthode doit être appelée dans un objet de l'étendue. Par exemple, une valeur doit être ajoutée à un dictionnaire. La méthode d'ajout de l'instance du dictionnaire est appelée, puis la clé et la valeur sont fournies.  
  
-   Une méthode doit être appelée sur un objet CLR hérité. Au lieu de créer une activité personnalisée pour encapsuler l'appel dans cette classe héritée, s'il se trouve dans l'étendue pendant l'exécution du flux de travail, il est possible d'utiliser <xref:System.Activities.Statements.InvokeMethod>.  
  
## <a name="error-handling-activities"></a>Activités de gestion des erreurs  
 L'activité <xref:System.Activities.Statements.TryCatch> fournit un mécanisme d'interception d'exceptions qui se produisent lors de l'exécution d'un ensemble d'activités contenues (similaire à la construction Try/Catch dans C#/VB). <xref:System.Activities.Statements.TryCatch> permet la gestion des exceptions au niveau du flux de travail. Si une exception non gérée est levée, le flux de travail est abandonné et le bloc Finally n'est pas exécuté. Ce comportement est cohérent avec le langage C#.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Dans Visual Studio 2012, créez une application console de workflow. Ajoutez une activité <xref:System.Activities.Statements.TryCatch> dans le concepteur de workflow.  
  
-   Exemple : [d’erreur de traitement dans une activité Flowchart à l’aide de TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
-   Documentation relative au concepteur : [concepteurs d’activités Gestion des erreurs](/visualstudio/workflow-designer/error-handling-activity-designers)  
  
### <a name="error-handling-scenarios"></a>Scénarios de gestion des erreurs  
 Un ensemble d'activités doit être exécuté et une logique spécifique être exécutée en cas d'erreur. Si, au cours de la logique de gestion des erreurs, il apparaît qu'il n'est pas possible de remédier à l'erreur, l'exception est à nouveau levée et l'activité parente (ou l'hôte) se charge du problème.  
  
## <a name="pick-activity"></a>Activité Pick  
 L'activité <xref:System.Activities.Statements.Pick> fournit une modélisation de flux de contrôle basée sur les événements dans WF. <xref:System.Activities.Statements.Pick> contient de nombreuses branches, où chacune d'entre elles attend qu'un événement particulier se produise avant de s'exécuter. Dans cette configuration, un <xref:System.Activities.Statements.Pick> se comporte de manière similaire à un <xref:System.Activities.Statements.Switch%601> dans lequel l'activité exécutera un seul des jeux d'événements qu'elle écoute. Chaque branche est pilotée par l'événement et celui qui se produit exécute la branche correspondante. Toutes les autres branches annulent et arrêtent l'écoute des événements.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Dans Visual Studio 2012, créez une application console de workflow. Ajoutez une activité <xref:System.Activities.Statements.Pick> dans le concepteur de workflow.  
  
-   Exemple : [à l’aide de l’activité Pick](../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)  
  
-   Documentation relative au concepteur : [Concepteur d’activités Pick](/visualstudio/workflow-designer/pick-activity-designer)  
  
### <a name="pick-scenario"></a>Scénario de l'activité Pick  
 Un utilisateur doit être invité à entrer des informations. Dans des circonstances normales, le développeur utiliserait un appel de méthode similaire à <xref:System.Console.ReadLine%2A> pour inviter un utilisateur à entrer des données. Le problème avec cette configuration est que le programme attend que l'utilisateur entre des données. Dans ce scénario, un délai d'attente est nécessaire pour débloquer une activité bloquante. Dans la plupart des scénarios, une tâche doit être effectuée pendant une durée déterminée. La définition d'un délai d'attente pour une activité bloquante fait partie des cas où Pick apporte une grande valeur ajoutée.  
  
## <a name="wcf-routing-service"></a>Service de routage WCF  
 Le Service de routage est conçu pour être une routeur qui vous permet de contrôler le flux des WCFmessages entre vos clients et les services des logiciels générique.  Le Service de routage vous permet de découpler vos clients à partir de vos services, qui vous donne beaucoup plus de liberté en termes de configurations que vous pouvez prendre en charge et la flexibilité que lorsque vous envisagez d’héberger vos services.  Dans .NET 3.5, les clients et services ont été étroitement couplés ; un client devait connaître sur tous les services, il est nécessaire pour communiquer avec et où ils se trouvaient. Par ailleurs, WCF présentait les limitations suivantes dans .Net Framework 3.5 :  
  
-   La gestion des erreurs était complexe car cette logique devait être codée en dur côté client.  
  
-   Les clients et les services devaient toujours utiliser les mêmes liaisons.  
  
-   Les services étaient rarement conçus de manière appropriée : il est plus facile de faire communiquer le client avec un service qui implémente tout un ensemble, plutôt que de choisir entre plusieurs services.  
  
 La conception du service de routage dans .Net 4 facilite la résolution de ces problèmes. Le nouveau service de routage présente les fonctionnalités suivantes :  
  
1.  Routage basé sur le contenu (les objets <xref:System.ServiceModel.Dispatcher.MessageFilter> examinent un message afin de déterminer sa destination.)  
  
2.  Pontage de protocoles (transport et message)  
  
3.  Gestion des erreurs (le routeur intercepte les exceptions de communication et bascule sur les points de terminaison de sauvegarde)  
  
4.  Mise à jour dynamique (en mémoire) de <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> et configuration du routage.  
  
### <a name="getting-started"></a>Prise en main  
  
1.  Documentation : [routage](../../../docs/framework/wcf/feature-details/routing.md)  
  
2.  Exemples : [Services de routage &#91;exemples WCF&#93;](../../../docs/framework/wcf/samples/routing-services.md)  
  
3.  Blog : [règles de routage !](https://go.microsoft.com/fwlink/?LinkId=204956)  
  
### <a name="routing-scenarios"></a>Scénarios de routage  
 Le service de routage s'avère utile dans les scénarios suivants :  
  
-   Les clients peuvent communiquer avec plusieurs services sans avoir à s'adresser à l'ensemble d'entre eux directement.  
  
-   Les clients peuvent apporter une logique supplémentaire à une demande du client afin de déterminer la destination du routage  
  
-   Décomposez les opérations effectuées par un client en plusieurs implémentations du service sans refactoriser le client.  
  
-   Les clients et les services peuvent présenter différentes liaisons avec différents paramètres de sécurité.  
  
-   Les clients peuvent être configurés de manière à être plus fiables en cas de défaillance ou d'indisponibilité des services.  
  
## <a name="wcf-discovery"></a>Discovery WCF  
 La découverte WCF est une technologie d’infrastructure qui vous permet d’incorporer un mécanisme de découverte pour votre infrastructure d’application. Vous pouvez vous en servir pour rendre votre service détectable et configurer vos clients pour qu'ils recherchent des services. Les clients n'ont plus besoin d'être codés en dur avec un point de terminaison, ce qui rend votre application plus fiable et plus tolérante aux pannes. Discovery est la plateforme parfaite pour intégrer des fonctionnalités d'auto-configuration à votre application.  
  
 Le produit repose sur la norme WS-Discovery. Il est conçu pour être interopérable, extensible et générique. Le produit prend en charge deux modes d'opération :  
  
1.  Managed : lorsqu'une entité sur le réseau est informée des services existants, les clients l'interrogent directement. Ce comportement est similaire à Active Directory.  
  
2.  Ad-hoc : lorsque les clients utilisent des messages de multidiffusion pour localiser des services.  
  
 Par ailleurs, les messages de découverte ne dépendent pas du protocole réseau ; vous pouvez les utiliser avec tout protocole qui prend en charge les besoins de chaque mode. Par exemple, découverte pour les messages de multidiffusion peuvent être envoyés sur le canal UDP ou tout autre réseau qui prend en charge la messagerie multidiffusion.  Ces points de conception, combinés avec la flexibilité des fonctionnalités, vous permettent d’adapter la détection spécifiquement à votre solution.  
  
### <a name="getting-started"></a>Prise en main  
  
-   Documentation : [découverte WCF](../../../docs/framework/wcf/feature-details/wcf-discovery.md)  
  
-   Exemples : [découverte (exemples)](../../../docs/framework/wcf/samples/discovery-samples.md)  
  
### <a name="discovery-scenarios"></a>Scénarios Discovery  
 Un développeur ne souhaite pas coder en dur les points de terminaison car la date de disponibilité de mon service n'est pas encore connue. Il souhaite plutôt choisir un service au moment du runtime. Un plus grand degré de découplage, de fiabilité et de configuration automatique est requis entre les composants de l'application.  
  
## <a name="tracking"></a>Suivi  
 Suivi de workflow fournit un aperçu de l’exécution d’une instance de workflow.  Les événements de suivi sont émis à partir d’un flux de travail au niveau de l’instance de flux de travail et lorsque les activités dans le flux de travail s’exécutent. Un participant au suivi du flux de travail doit être ajouté à l'hôte du flux de travail pour s'abonner aux enregistrements de suivi. Les enregistrements de suivi sont filtrés à l'aide d'un profil de suivi. Le .Net Framework fournit un participant au suivi ETW (Event Tracing for Windows) et un profil de base est installé dans le fichier machine.config.  
  
### <a name="getting-started"></a>Prise en main  
  
1.  Dans Visual Studio 2010, créez un projet d'application de service de flux de travail WCF. Une paire <xref:System.ServiceModel.Activities.Receive> et <xref:System.ServiceModel.Activities.SendReply> sera placée dans votre zone de dessin pour le démarrage.  
  
2.  Ouvrez le fichier web.config et ajoutez un comportement de suivi ETW sans profil.  
  
    1.  Le profil par défaut est utilisé.  
  
    2.  Ouvrez l’Observateur d’événements et activer le canal analytique dans le nœud suivant : **Observateur d’événements**, **journaux des Applications et Services**, **Microsoft**, **Windows** , **Serveur d’applications-Applications**. Avec le bouton droit **analyse** et sélectionnez **activer le journal**.  
  
    3.  Exécutez le service de flux de travail.  
  
    4.  Observez les événements de suivi du flux de travail dans l'observateur d'événements.  
  
3.  Exemples : [de suivi](../../../docs/framework/windows-workflow-foundation/samples/tracking.md)  
  
4.  Documentation conceptuelle : [suivi de Workflow](../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md)  
  
## <a name="sql-workflow-instance-store"></a>Magasin d'instances de workflow SQL  
 Le <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> est une implémentation basée sur SQL d'un magasin d'instances. Un magasin d'instances stocke l'état d'une instance en cours d'exécution avec l'ensemble des données nécessaires au chargement et à la reprise de cette instance. L'hôte du service demande au magasin d'instances d'enregistrer l'état de l'instance si le flux de travail persiste et de charger l'état de l'instance quand un message arrive pour cette instance ou qu'une activité de report arrive à expiration.  
  
### <a name="getting-started"></a>Prise en main  
  
1.  Dans Visual Studio 2012, créez un flux de travail qui contient un implicite ou explicite <xref:System.Activities.Statements.Persist> activité. Ajoutez le comportement <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> à votre hôte de service de workflow. Cela peut se faire dans le code ou dans le fichier de configuration de l'application.  
  
2.  Exemples : [persistance](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)  
  
3.  Documentation conceptuelle : [SQL Workflow Instance Store](../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md).
