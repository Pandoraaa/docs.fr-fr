---
title: ICLRDataTarget::SetTLSValue, méthode
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.SetTLSValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::SetTLSValue
helpviewer_keywords:
- ICLRDataTarget::SetTLSValue method [.NET Framework debugging]
- SetTLSValue method [.NET Framework debugging]
ms.assetid: 4a2d6a24-749a-47ad-9f01-4517203d3f35
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 18733c2d643a75f9bb11159ba4acdbc8ab064c55
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33404102"
---
# <a name="iclrdatatargetsettlsvalue-method"></a>ICLRDataTarget::SetTLSValue, méthode
Définit une valeur dans le stockage local des threads (TLS) du thread spécifié dans le processus cible. Cette méthode est appelée par les services d’accès données common language runtime (CLR).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT SetTLSValue (  
    [in] ULONG32            threadID,  
    [in] ULONG32            index,  
    [in] CLRDATA_ADDRESS    value  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `threadID`  
 [in] L’identificateur de système d’exploitation d’un thread dans le processus cible.  
  
 `index`  
 [in] Index de l’emplacement. Cette valeur doit être un index valide dans le magasin local du thread spécifié.  
  
 `value`  
 [in] A `CLRDATA_ADDRESS` valeur qui spécifie la valeur à placer dans l’emplacement de TLS donné.  
  
## <a name="remarks"></a>Notes  
 Cette méthode est implémentée par le writer de l'application de débogage.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** ClrData.idl, ClrData.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [ICLRDataTarget, interface](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
