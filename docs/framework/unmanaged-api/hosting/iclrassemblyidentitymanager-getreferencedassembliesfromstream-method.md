---
title: ICLRAssemblyIdentityManager::GetReferencedAssembliesFromStream, méthode
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetReferencedAssembliesFromStream
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetReferencedAssembliesFromStream
helpviewer_keywords:
- ICLRAssemblyIdentityManager::GetReferencedAssembliesFromStream method [.NET Framework hosting]
- GetReferencedAssembliesFromStream method [.NET Framework hosting]
ms.assetid: fe9849c1-c3fc-477b-a31f-e8619f5516f5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7a5020b387abcdcdc0047de90eb588157eaec08c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33435308"
---
# <a name="iclrassemblyidentitymanagergetreferencedassembliesfromstream-method"></a>ICLRAssemblyIdentityManager::GetReferencedAssembliesFromStream, méthode
Obtient un pointeur vers un [ICLRReferenceAssemblyEnum](../../../../docs/framework/unmanaged-api/hosting/iclrreferenceassemblyenum-interface.md) objet qui contient les données d’identité pour les assemblys référencés par l’assembly dans le flux spécifié.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT GetReferencedAssembliesFromStream (  
    [in]  IStream *pStream,  
    [in]  DWORD    dwFlags,  
    [in]  ICLRAssemblyReferenceList  *pExcludeAssembliesList,  
    [out] ICLRReferenceAssemblyEnum **ppReferenceEnum  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `pStream`  
 [in] Pointeur d’interface vers un `IStream` contenant l’assembly à évaluer.  
  
 `dwFlags`  
 [in] Fourni pour une extensibilité future. CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT est la seule valeur de la version actuelle du common language runtime (CLR) prend en charge.  
  
 `pExcludeAssembliesList`  
 [in] Un pointeur vers un [ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md) objet qui contient les données d’identité pour les assemblys à exclure de `ppReferenceEnum`.  
  
 `ppReferenceEnum`  
 [out] Un pointeur vers l’adresse d’un `ICLRReferenceAssemblyEnum` objet qui contient les données d’identité pour les assemblys référencés par l’assembly dans `pStream`, à l’exclusion des assemblys dans `pExcludeAssembliesList`.  
  
## <a name="return-value"></a>Valeur de retour  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|La méthode a été retourné avec succès.|  
|HOST_E_CLRNOTAVAILABLE|Le CLR n’a pas été chargé dans un processus ou le CLR est dans un état dans lequel il ne peut pas exécuter du code managé ou traiter l’appel avec succès.|  
|HOST_E_TIMEOUT|L’appel a expiré.|  
|HOST_E_NOT_OWNER|L’appelant ne possède pas le verrou.|  
|HOST_E_ABANDONED|Un événement a été annulé alors qu’un thread bloqué ou une fibre l’attendait.|  
|E_FAIL|Une défaillance grave et inconnue s’est produite. Si une méthode retourne E_FAIL, le CLR n’est plus utilisable dans le processus. Les appels suivants aux méthodes d’hébergement retournent HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Notes  
 L’appelant peut choisir d’exclure un ensemble de références d’assembly connues de la liste retournée. Ce jeu est défini par `pExcludeAssembliesList`.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** MSCorEE.h  
  
 **Bibliothèque :** inclus en tant que ressource dans MSCorEE.dll  
  
 **Versions du .NET framework :** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [ICLRAssemblyIdentityManager, interface](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-interface.md)  
 [ICLRAssemblyReferenceList, interface](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)  
 [ICLRReferenceAssemblyEnum, interface](../../../../docs/framework/unmanaged-api/hosting/iclrreferenceassemblyenum-interface.md)
