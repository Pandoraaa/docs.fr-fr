---
title: 'Comment : positionner une info-bulle'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], positioning
- positioning ToolTip controls [WPF]
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
ms.openlocfilehash: e51be52301197a66ef49339245e60404d823b36c
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43512291"
---
# <a name="how-to-position-a-tooltip"></a>Comment : positionner une info-bulle
Cet exemple montre comment spécifier la position d’une info-bulle sur l’écran.  
  
## <a name="example"></a>Exemple  
 Vous pouvez positionner une info-bulle à l’aide d’un ensemble de cinq propriétés sont définies dans les deux le <xref:System.Windows.Controls.ToolTip> et <xref:System.Windows.Controls.ToolTipService> classes. Le tableau suivant illustre ces deux ensembles de cinq propriétés et fournit des liens vers leur documentation de référence en fonction de la classe.  
  
### <a name="corresponding-tooltip-properties-according-to-class"></a>Propriétés d’info-bulle correspondant en fonction de classe  
  
|<xref:System.Windows.Controls.ToolTip?displayProperty=nameWithType> propriétés de la classe|<xref:System.Windows.Controls.ToolTipService?displayProperty=nameWithType> propriétés de la classe|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=nameWithType>|  
  
 Si vous définissez le contenu d’une info-bulle à l’aide un <xref:System.Windows.Controls.ToolTip> de l’objet, vous pouvez utiliser les propriétés de classe ; Toutefois, le <xref:System.Windows.Controls.ToolTipService> propriétés sont prioritaires. Utilisez le <xref:System.Windows.Controls.ToolTipService> propriétés pour les info-bulles qui ne sont pas définies comme <xref:System.Windows.Controls.ToolTip> objets.  
  
 Les illustrations suivantes montrent comment positionner une info-bulle à l’aide de ces propriétés. Bien que, le [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] exemples dans ces illustrations montrent comment définir les propriétés qui sont définies par le <xref:System.Windows.Controls.ToolTip> classe, les propriétés correspondantes de la <xref:System.Windows.Controls.ToolTipService> classe suivent les mêmes règles de mise en page. Pour plus d’informations sur les valeurs possibles pour la propriété de positionnement, consultez [comportement de positionnement de Popup](../../../../docs/framework/wpf/controls/popup-placement-behavior.md).  
  
 ![Positionnement de ToolTip](../../../../docs/framework/wpf/controls/media/tooltipplacement.png "ToolTipPlacement")  
Positionnement de ToolTip à l’aide de la propriété de positionnement  
  
 ![Placer une info-bulle à l’aide d’un rectangle de sélection élective](../../../../docs/framework/wpf/controls/media/tooltipplacementrectangle.png "ToolTipPlacementRectangle")  
Positionnement de ToolTip à l’aide des propriétés Placement et PlacementRectangle  
  
 ![Diagramme de positionnement de ToolTip](../../../../docs/framework/wpf/controls/media/tooltipplacementprhv.png "ToolTipPlacementPRHV")  
Positionnement de ToolTip à l’aide des propriétés Placement, PlacementRectangle et Offset  
  
 L’exemple suivant montre comment utiliser le <xref:System.Windows.Controls.ToolTip> propriétés pour spécifier la position d’une info-bulle dont le contenu est un <xref:System.Windows.Controls.ToolTip> objet.  
  
 [!code-xaml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 L’exemple suivant montre comment utiliser le <xref:System.Windows.Controls.ToolTipService> propriétés pour spécifier la position d’une info-bulle dont le contenu n’est pas un <xref:System.Windows.Controls.ToolTip> objet.  
  
 [!code-xaml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Controls.ToolTip>  
 <xref:System.Windows.Controls.ToolTipService>  
 [Rubriques de guide pratique](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)  
 [Vue d’ensemble de l’info-bulle](../../../../docs/framework/wpf/controls/tooltip-overview.md)  
 [Utiliser les ContextMenuService ToolTipService](https://msdn.microsoft.com/library/809b0e9c-d612-4cda-b8af-1a698c68f4d1)
