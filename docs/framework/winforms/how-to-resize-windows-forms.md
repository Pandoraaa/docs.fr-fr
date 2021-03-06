---
title: 'Comment : redimensionner des Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- resizing Windows Forms
- Windows Forms, resizing
ms.assetid: 5d9dd47e-e68c-48c9-a0a3-a9ff34ba009d
ms.openlocfilehash: 40a2ff3dcde9d0fbbc9a7e6c67430eb8313614e4
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43521184"
---
# <a name="how-to-resize-windows-forms"></a>Comment : redimensionner des Windows Forms
Vous pouvez spécifier la taille de votre Windows Form de plusieurs façons. Vous pouvez modifier à la fois la hauteur et la largeur du formulaire par programmation en affectant une nouvelle valeur à la propriété <xref:System.Windows.Forms.Form.Size%2A>, ou ajuster les propriétés <xref:System.Windows.Forms.Control.Height%2A> et <xref:System.Windows.Forms.Control.Width%2A> individuellement. Si vous utilisez Visual Studio, vous pouvez modifier la taille à l’aide du Concepteur de formulaires Windows. Consultez également [Comment : redimensionner des Windows Forms en utilisant le concepteur](https://msdn.microsoft.com/library/37k2zkwx\(v=vs.110\)).  
  
### <a name="to-resize-a-form-programmatically"></a>Pour redimensionner un formulaire par programmation  
  
-   Définissez la taille d'un formulaire au moment de l'exécution en définissant la propriété <xref:System.Windows.Forms.Form.Size%2A> du formulaire.  
  
     L'exemple de code suivant montre la taille de formulaire définie sur 100 × 100 pixels.  
  
    ```vb  
    Form1.Size = New System.Drawing.Size(100, 100)  
    ```  
  
    ```csharp  
    Form1.Size = new System.Drawing.Size(100, 100);  
    ```  
  
    ```cpp  
    Form1->Size = System::Drawing::Size(100, 100);  
    ```  
  
### <a name="to-change-form-width-and-height-programmatically"></a>Pour modifier la hauteur et la largeur du formulaire par programmation  
  
-   Une fois le <xref:System.Windows.Forms.Form.Size%2A> défini, modifiez la hauteur ou la largeur du formulaire à l'aide de la propriété <xref:System.Windows.Forms.Control.Width%2A> ou <xref:System.Windows.Forms.Control.Height%2A>.  
  
     L'exemple de code suivant montre la largeur du formulaire définie sur 300 pixels à partir du bord gauche du formulaire, alors que la hauteur reste constante.  
  
    ```vb  
    Form1.Width = 300  
    ```  
  
    ```csharp  
    Form1.Width = 300;  
    ```  
  
    ```cpp  
    Form1->Width = 300;  
    ```  
  
     ou  
  
     Modifiez <xref:System.Drawing.Size.Width%2A> ou <xref:System.Drawing.Size.Height%2A> en définissant la propriété <xref:System.Windows.Forms.Form.Size%2A>.  
  
     Toutefois, comme le montre l'exemple de code suivant, cette approche est plus laborieuse que la simple définition de la propriété <xref:System.Windows.Forms.Control.Width%2A> ou <xref:System.Windows.Forms.Control.Height%2A>.  
  
    ```vb  
    Form1.Size = New Size(300, Form1.Size.Height)  
    ```  
  
    ```csharp  
    Form1.Size = new Size(300, Form1.Size.Height);  
    ```  
  
    ```cpp  
    Form1->Size = System::Drawing::Size(300, Form1->Size.Height);  
    ```  
  
### <a name="to-change-form-size-by-increments-programmatically"></a>Pour modifier la taille de formulaire par incréments par programmation  
  
-   Pour incrémenter la taille du formulaire, définissez les propriétés <xref:System.Drawing.Size.Width%2A> et <xref:System.Drawing.Size.Height%2A>.  
  
     L'exemple de code suivant montre la largeur du formulaire définie sur 200 pixels de plus que la valeur actuelle.  
  
    ```vb  
    Form1.Width += 200  
    ```  
  
    ```csharp  
    Form1.Width += 200;  
    ```  
  
    ```cpp  
    Form1->Width += 200;  
    ```  
  
    > [!CAUTION]
    >  Utilisez toujours la propriété <xref:System.Drawing.Size.Height%2A> ou <xref:System.Drawing.Size.Width%2A> pour modifier une dimension d'un formulaire, sauf si vous définissez les dimensions de hauteur et de largeur en même temps en affectant une nouvelle structure <xref:System.Drawing.Size> à la propriété <xref:System.Windows.Forms.Form.Size%2A>. La propriété <xref:System.Windows.Forms.Form.Size%2A> retourne une structure <xref:System.Drawing.Size>, qui est un type valeur. Vous ne pouvez pas attribuer une nouvelle valeur à la propriété d'un type valeur. Le code suivant, par exemple, ne sera pas compilé :  
  
    ```vb  
    ' NOTE: CODE WILL NOT COMPILE  
    Dim f As New Form()  
    f.Size.Width += 100  
    ```  
  
    ```csharp  
    // NOTE: CODE WILL NOT COMPILE  
    Form f = new Form();  
    f.Size.Width += 100;  
    ```  
  
    ```cpp  
    // NOTE: CODE WILL NOT COMPILE  
    Form^ f = gcnew Form();  
    f->Size->X += 100;  
    ```  
  
## <a name="see-also"></a>Voir aussi  
 [Bien démarrer avec Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)  
 [Amélioration des applications Windows Forms](../../../docs/framework/winforms/advanced/index.md)
