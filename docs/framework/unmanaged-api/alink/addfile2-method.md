---
title: AddFile2, méthode
ms.date: 03/30/2017
api_name:
- AddFile2
- IALink2.AddFile2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddFile2
helpviewer_keywords:
- AddFile2 method
ms.assetid: 03bc49bf-a89b-4fb6-a88d-97482e061195
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f4735103f277d710dd23adfa19c475c425feaa36
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33403329"
---
# <a name="addfile2-method"></a>AddFile2, méthode
Ajoute des fichiers à l’assembly. Peut également être utilisé pour créer des modules indépendants.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT AddFile2(  
    mdAssembly AssemblyID,  
    LPCWSTR pszFilename,  
    DWORD dwFlags,  
    IMetaDataEmit2* pEmitter,  
    mdFile* pFileToken  
) PURE;  
```  
  
#### <a name="parameters"></a>Paramètres  
 `AssemblyID`  
 ID de l’assembly auquel le fichier est ajouté.  
  
 `pszFilename`  
 Nom du fichier à ajouter.  
  
 `dwFlags`  
 COM + `FileDef` indicateurs tels que `ffContainsNoMetaData` et `ffWriteable`. `dwFlags` est passé à [DefineFile, méthode](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-definefile-method.md).  
  
 `pEmitter`  
 Interface [IMetaDataEmit2 (Interface)](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md) interface.  
  
 `pFileToken`  
 Reçoit l’ID du fichier à ajouter.  
  
## <a name="return-value"></a>Valeur de retour  
 Retourne S_OK si la méthode réussit.  
  
## <a name="requirements"></a>Spécifications  
 Requiert alink.h.  
  
## <a name="see-also"></a>Voir aussi  
 [IALink2, interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)  
 [IALink, interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)  
 [API ALink](../../../../docs/framework/unmanaged-api/alink/index.md)
