---
title: -optioninfer
ms.date: 07/20/2015
f1_keywords:
- -optioninfer
helpviewer_keywords:
- -optioninfer compiler option [Visual Basic]
- /optioninfer compiler option [Visual Basic]
- optioninfer compiler option [Visual Basic]
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
ms.openlocfilehash: e7dbc4d5f06096978c4d93ea20677dcb60bc3fcb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33655923"
---
# <a name="-optioninfer"></a>-optioninfer
Permet l'utilisation de l'inférence de type de variable locale dans les déclarations de variable.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
-optioninfer[+ | -]  
```  
  
## <a name="arguments"></a>Arguments  
  
|Terme|Définition|  
|---|---|  
|`+` &#124; `-`|Facultatif. Spécifiez `-optioninfer+` pour activer l'inférence de type de variable locale ou `-optioninfer-` pour la bloquer. L'option `-optioninfer`, sans aucune valeur spécifiée, est identique à `-optioninfer+`. La valeur par défaut en l'absence du commutateur `-optioninfer` est aussi `-optioninfer+`. La valeur par défaut est définie dans le fichier réponse Vbc.rsp.|  
  
> [!NOTE]
>  Vous pouvez utiliser l'option `-noconfig` pour conserver les valeurs par défaut internes du compilateur au lieu de celles spécifiées dans le fichier vbc.rsp. Pour cette option, la valeur par défaut du compilateur est `-optioninfer-`.  
  
## <a name="remarks"></a>Notes  
 Si le fichier de code source contient un [Option Infer, instruction](../../../visual-basic/language-reference/statements/option-infer-statement.md), l’instruction substitue le `-optioninfer` paramètre du compilateur de ligne de commande.  
  
### <a name="to-set--optioninfer-in-the-visual-studio-ide"></a>Pour définir /optioninfer - dans l’IDE de Visual Studio  
  
1.  Sélectionnez un projet dans **l’Explorateur de solutions**. Dans le menu **Projet**, cliquez sur **Propriétés**.  
  
2.  Sur le **compiler** onglet, modifiez la valeur dans la **Option infer** boîte.  
  
## <a name="example"></a>Exemple  
 Le code suivant compile `test.vb` avec l'inférence de type de variable locale activée.  
  
```console
vbc -optioninfer+ test.vb  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Compilateur de ligne de commande de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)  
 [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)  
 [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)  
 [Exemples de lignes de commande de compilation](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Option Infer (instruction)](../../../visual-basic/language-reference/statements/option-infer-statement.md)  
 [Inférence de type local](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)  
 [Valeurs par défaut Visual Basic, Projets, boîte de dialogue Options](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)  
 [Page Compiler, Concepteur de projet (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)  
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)  
 [Génération à partir de la ligne de commande](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)
