---
title: ICorDebugProcess::ReadMemory, méthode
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ReadMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ReadMemory
helpviewer_keywords:
- ReadMemory method [.NET Framework debugging]
- ICorDebugProcess::ReadMemory method [.NET Framework debugging]
ms.assetid: 28e4b2f6-9589-445c-be24-24a3306795e7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a0063e33a6a7861815ebb9d9eb3dabec64dd4b9d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33419651"
---
# <a name="icordebugprocessreadmemory-method"></a>ICorDebugProcess::ReadMemory, méthode
Lit une zone spécifiée de mémoire pour ce processus.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT ReadMemory(  
    [in]  CORDB_ADDRESS address,   
    [in]  DWORD size,  
    [out, size_is(size), length_is(size)] BYTE buffer[],  
    [out] SIZE_T *read);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `address`  
 [in] A `CORDB_ADDRESS` valeur qui spécifie l’adresse de base de la mémoire à lire.  
  
 `size`  
 [in] Le nombre d’octets à lire à partir de la mémoire.  
  
 `buffer`  
 [out] Une mémoire tampon qui reçoit le contenu de la mémoire.  
  
 `read`  
 [out] Un pointeur vers le nombre d’octets transférés vers la mémoire tampon spécifiée.  
  
## <a name="remarks"></a>Notes  
 Le `ReadMemory` méthode est principalement destinée à être utilisée par le débogage d’interopérabilité pour inspecter les régions de mémoire qui sont utilisées par la partie non managée du programme débogué. Cette méthode peut également être utilisée pour lire le code Microsoft intermediate language (MSIL) et le code natif compilé par JIT.  
  
 N’importe quel point d’arrêt managé sera supprimée à partir des données qui sont retournées dans le `buffer` paramètre. Aucun réglage n’est effectué pour les points d’arrêt natifs défini par [ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md).  
  
 Aucune mise en cache de mémoire de processus n’est effectuée.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
