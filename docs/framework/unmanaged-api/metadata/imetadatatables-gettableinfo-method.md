---
title: IMetaDataTables::GetTableInfo, méthode
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetTableInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetTableInfo
helpviewer_keywords:
- IMetaDataTables::GetTableInfo method [.NET Framework metadata]
- GetTableInfo method [.NET Framework metadata]
ms.assetid: 50cbe557-2322-41aa-8e0d-f967602eaa0f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ea617668a72413f3387a35fe009b37fa15d03354
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
---
# <a name="imetadatatablesgettableinfo-method"></a>IMetaDataTables::GetTableInfo, méthode
Obtient le nom, la taille de ligne, le nombre de lignes, le nombre de colonnes et les index de colonne clé de la table spécifiée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT GetTableInfo (  
    [in]  ULONG       ixTbl,  
    [out] ULONG       *pcbRow,  
    [out] ULONG       *pcRows,  
    [out] ULONG       *pcCols,  
    [out] ULONG       *piKey,  
    [out] const char  **ppName  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `ixTbl`  
 [in] L’identificateur de la table dont les propriétés à retourner.  
  
 `pcbRow`  
 [out] Pointeur vers la taille, en octets, d’une ligne de table.  
  
 `pcRows`  
 [out] Pointeur vers le nombre de lignes dans la table.  
  
 `pcCols`  
 [out] Pointeur vers le nombre de colonnes dans la table.  
  
 `piKey`  
 [out] Pointeur vers l’index de la colonne clée, ou -1 si la table ne comporte aucune colonne clé.  
  
 `ppName`  
 [out] Pointeur vers un pointeur vers le nom de table.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** Cor.h  
  
 **Bibliothèque :** utilisé en tant que ressource dans MsCorEE.dll  
  
 **Versions du .NET framework :** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [IMetaDataTables, interface](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)  
 [IMetaDataTables2, interface](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)
