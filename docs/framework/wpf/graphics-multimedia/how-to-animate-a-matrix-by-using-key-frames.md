---
title: "Comment : animer une matrice à l'aide d'images clés"
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], Matrix properties with key frames
- Matrix properties [WPF], animating with key frames
- key frames [WPF], animating Matrix properties with
ms.assetid: b851a4c7-ecb1-420e-9203-83e7afd037fd
ms.openlocfilehash: 8f58b43a870f2c85ae4349965f586a33e2f75a2a
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2018
ms.locfileid: "43485848"
---
# <a name="how-to-animate-a-matrix-by-using-key-frames"></a>Comment : animer une matrice à l'aide d'images clés
Cet exemple montre comment animer la <xref:System.Windows.Media.MatrixTransform.Matrix%2A> propriété d’un <xref:System.Windows.Media.MatrixTransform> à l’aide d’images clés.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant utilise le <xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames> classe pour animer la <xref:System.Windows.Media.MatrixTransform.Matrix%2A> propriété d’un <xref:System.Windows.Media.MatrixTransform>. L’exemple utilise le <xref:System.Windows.Media.MatrixTransform> objet à transformer l’apparence et la position d’un <xref:System.Windows.Controls.Button>.  
  
 Cette animation utilise la <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> classe pour créer deux images clés et effectue les opérations suivantes avec eux :  
  
1.  Anime la première <xref:System.Windows.Media.Matrix> pendant les premières secondes de 0,2. L’exemple modifie la <xref:System.Windows.Media.Matrix.M11%2A> et <xref:System.Windows.Media.Matrix.M12%2A> propriétés de la <xref:System.Windows.Media.Matrix>. Cette modification entraîne le bouton pour étirer et être faussées. L’exemple modifie également le <xref:System.Windows.Media.Matrix.OffsetX%2A> et <xref:System.Windows.Media.Matrix.OffsetY%2A> propriétés afin que le bouton change de position.  
  
2.  Anime la deuxième <xref:System.Windows.Media.Matrix> à 1 seconde. Le bouton se déplace vers un autre alors que le bouton n’est plus incliné ni étiré.  
  
3.  Répète l’animation indéfiniment.  
  
> [!NOTE]
>  Images clés qui dérivent de la <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> objet créent des changements soudains entre les valeurs, autrement dit, le déplacement de l’animation est saccadé.  
  
 [!code-xaml[keyframes_snip#MatrixAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/MatrixAnimationUsingKeyFramesExample.xaml#matrixanimationusingkeyframeswholepage)]  
  
 Pour l’exemple complet, consultez la page [Animation d’image clé, exemple](https://go.microsoft.com/fwlink/?LinkID=160012).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Media.MatrixTransform.Matrix%2A>  
 <xref:System.Windows.Media.MatrixTransform>  
 [Vue d'ensemble des animations d'image clé](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)  
 [Guides pratiques relatifs aux images clés](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)
