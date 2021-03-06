---
title: Introduction au contrôle DataRepeater (Visual Studio)
ms.date: 07/20/2015
helpviewer_keywords:
- repeating data
- DataRepeater, overview
- DataRepeater
ms.assetid: 78a52a1d-65f0-4ecb-97ff-53bc114300c5
ms.openlocfilehash: fc0cf9c358faf3e738eb3b24ec61577b88dbce4a
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2018
ms.locfileid: "43485714"
---
# <a name="introduction-to-the-datarepeater-control-visual-studio"></a>Introduction au contrôle DataRepeater (Visual Studio)
Le contrôle <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> de Visual Basic Power Packs est un conteneur à défilement pour les contrôles qui affichent des données répétées, par exemple des lignes dans une table de base de données. Il peut être utilisé comme alternative au contrôle <xref:System.Windows.Forms.DataGridView> quand vous avez besoin de plus de contrôle sur la disposition des données. Le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> « se » répète un groupe de contrôles connexes en créant plusieurs instances dans une vue de défilement. Cela permet aux utilisateurs d’afficher plusieurs enregistrements en même temps.  
  
## <a name="overview"></a>Vue d'ensemble  
 Au moment du design, le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle se compose de deux sections. La section externe est la *viewport*, où les données de défilement seront affichera au moment de l’exécution. La section interne (supérieur), connu sous le nom du *modèle d’élément*, est l’endroit où vous positionnez des contrôles qui seront répétés au moment de l’exécution, généralement dans un contrôle pour chaque champ dans la source de données. Les propriétés et les contrôles dans le modèle d’élément sont encapsulées dans le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> propriété.  
  
 Au moment de l’exécution, le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> est copié vers une machine virtuelle <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> objet qui est utilisé pour afficher les données lorsque vous faites défiler chaque enregistrement dans la vue. Vous pouvez personnaliser l’affichage des enregistrements individuels dans le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> événement, par exemple, la mise en surbrillance un champ en fonction de la valeur qu’il contient. Pour plus d’informations, consultez [Comment : modifier l’apparence d’un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 L’utilisation la plus courante pour un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle consiste à afficher des données à partir d’une table de base de données ou autre source de données liée. En plus de [!INCLUDE[vstecado](~/includes/vstecado-md.md)] des objets de données, le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle peut être lié à toute classe qui implémente le <xref:System.Collections.IList> interface (y compris les tableaux), toute classe qui implémente le <xref:System.ComponentModel.IListSource> interface, toute classe qui implémente le <xref:System.ComponentModel.IBindingList> interface, ou toute classe qui implémente le <xref:System.ComponentModel.IBindingListView> interface.  
  
### <a name="data-binding"></a>Liaison de données  
 En règle générale, vous effectuer la liaison de données en faisant glisser des champs à partir de la **des Sources de données** fenêtre vers le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle. Pour plus d’informations, consultez [Comment : afficher des données liées dans un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md).  
  
 Lorsque vous travaillez avec grandes quantités de données, vous pouvez définir le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> propriété `True` pour afficher un sous-ensemble des données disponibles. Mode virtuel requiert l’implémentation d’un cache de données à partir de laquelle le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> est remplie, et vous devez contrôler toutes les interactions avec le cache de données en cours d’exécution. Pour plus d’informations, consultez [Mode virtuel dans le contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md).  
  
 Vous pouvez également afficher des contrôles indépendants sur un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle. Par exemple, vous pouvez afficher une image qui est répétée sur chaque élément. Pour plus d’informations, consultez [Comment : afficher les contrôles indépendants dans un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md).  
  
### <a name="events"></a>Événements  
 Les événements les plus importants pour le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle sont le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> événement qui se produit lorsque de nouveaux éléments défilent dans l’affichage, et le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> événement, qui est déclenché lorsqu’un élément est sélectionné. Vous pouvez utiliser le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> événement pour modifier l’apparence de l’élément. Par exemple, vous pouvez mettre en surbrillance les valeurs négatives. Utilisez le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> événement pour accéder aux valeurs des contrôles lorsqu’un élément est sélectionné.  
  
 Le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle expose tous les événements de contrôle standard dans l’éditeur de Code. Toutefois, certains événements ne doivent pas utilisé. Clavier et souris tels que des événements `KeyDown`, `Click`, et `MouseDown` ne sera pas déclenchée au moment de l’exécution, car le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle lui-même n’a jamais le focus.  
  
 Le <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> n’expose pas d’événements au moment du design, car il est créé uniquement au moment de l’exécution. Si vous souhaitez gérer les événements de clavier et de la souris, vous pouvez ajouter un <xref:System.Windows.Forms.Panel> le contrôle à la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> au moment du design, puis gérer les événements pour le <xref:System.Windows.Forms.Panel>. Pour plus d’informations, consultez [résolution des problèmes de contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md).  
  
### <a name="customizations"></a>Personnalisations  
 Il existe plusieurs façons de personnaliser l’apparence et le comportement de la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôler, à la fois au moment de l’exécution et au moment du design. Propriétés peuvent être définies pour modifier les couleurs, masquer ou modifier les en-têtes d’élément, changez l’orientation de vertical à horizontal et bien plus encore. Pour plus d’informations, consultez [Comment : modifier l’apparence d’un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md), [Comment : afficher les en-têtes d’élément dans un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md), et [Comment : modifier la disposition d’un Contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md).  
  
 Notez que certaines propriétés s’appliquent à la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contrôle lui-même, tandis que d’autres s’appliquent uniquement à la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>. Assurez-vous que vous disposez de la section appropriée du contrôle sélectionné avant de définir des propriétés. Pour plus d’informations, consultez [Comment : modifier l’apparence d’un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 D’autres personnalisations permettent de contrôler la capacité d’ajouter ou supprimer des enregistrements, en ajoutant des fonctionnalités de recherche et affichage de données liées dans un format maître et détail. Pour plus d’informations, consultez [Comment : désactiver l’ajout et suppression d’éléments DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md), [Comment : rechercher des données dans un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md), et [Comment : créer un formulaire maître/détail en utilisant deux Contrôles DataRepeater (Visual Studio)](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md).  
  
## <a name="see-also"></a>Voir aussi  
 [DataRepeater, contrôle](../../../visual-basic/developing-apps/windows-forms/datarepeater-control-visual-studio.md)  
 [Procédure pas à pas : affichage de données dans un contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio.md)  
 [Dépannage des problèmes liés au contrôle DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
