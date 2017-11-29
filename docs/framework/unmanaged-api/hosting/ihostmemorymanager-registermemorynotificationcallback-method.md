---
title: "IHostMemoryManager::RegisterMemoryNotificationCallback メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostMemoryManager.RegisterMemoryNotificationCallback
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostMemoryManager::RegisterMemoryNotificationCallback
helpviewer_keywords:
- IHostMemoryManager::RegisterMemoryNotificationCallback method [.NET Framework hosting]
- RegisterMemoryNotificationCallback method [.NET Framework hosting]
ms.assetid: 65d301f6-4dbb-4b5f-8eff-82540e2b6465
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 142fd6edba9a517f0d43db9d070a47ebeba8d313
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="ihostmemorymanagerregistermemorynotificationcallback-method"></a><span data-ttu-id="8e2b5-102">IHostMemoryManager::RegisterMemoryNotificationCallback メソッド</span><span class="sxs-lookup"><span data-stu-id="8e2b5-102">IHostMemoryManager::RegisterMemoryNotificationCallback Method</span></span>
<span data-ttu-id="8e2b5-103">コンピューターのメモリ負荷が現在のホストが共通言語ランタイム (CLR) に通知するために呼び出すコールバック関数へのポインターを登録します。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-103">Registers a pointer to a callback function that the host invokes to notify the common language runtime (CLR) of the current memory load on the computer.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8e2b5-104">構文</span><span class="sxs-lookup"><span data-stu-id="8e2b5-104">Syntax</span></span>  
  
```  
HRESULT RegisterMemoryNotificationCallback (  
    [in] ICLRMemoryNotificationCallback* pCallback  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="8e2b5-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="8e2b5-105">Parameters</span></span>  
 `pCallback`  
 <span data-ttu-id="8e2b5-106">[in]インターフェイス ポインター、 [ICLRMemoryNotificationCallback](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-interface.md) CLR で実装されているインスタンス。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-106">[in] An interface pointer to an [ICLRMemoryNotificationCallback](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-interface.md) instance that is implemented by the CLR.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8e2b5-107">戻り値</span><span class="sxs-lookup"><span data-stu-id="8e2b5-107">Return Value</span></span>  
  
|<span data-ttu-id="8e2b5-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="8e2b5-108">HRESULT</span></span>|<span data-ttu-id="8e2b5-109">説明</span><span class="sxs-lookup"><span data-stu-id="8e2b5-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="8e2b5-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="8e2b5-110">S_OK</span></span>|<span data-ttu-id="8e2b5-111">`RegisterMemoryNotificationCallback`正常に返されます。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-111">`RegisterMemoryNotificationCallback` returned successfully.</span></span>|  
|<span data-ttu-id="8e2b5-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="8e2b5-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="8e2b5-113">CLR が、プロセスに読み込まれていませんまたは CLR は、状態をマネージ コードを実行またはできないの呼び出しは正常に処理します。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-113">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="8e2b5-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="8e2b5-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="8e2b5-115">呼び出しがタイムアウトしました。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-115">The call timed out.</span></span>|  
|<span data-ttu-id="8e2b5-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="8e2b5-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="8e2b5-117">呼び出し元は、ロックを所有していません。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="8e2b5-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="8e2b5-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="8e2b5-119">イベントがキャンセルされましたブロックされたスレッドまたはファイバーが待機しています。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="8e2b5-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="8e2b5-120">E_FAIL</span></span>|<span data-ttu-id="8e2b5-121">不明な致命的なエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="8e2b5-122">メソッドには、E_FAIL が返される、ときに、CLR は、プロセス内で使用可能ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="8e2b5-123">メソッドのホストに以降の呼び出しでは、HOST_E_CLRNOTAVAILABLE を返します。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8e2b5-124">コメント</span><span class="sxs-lookup"><span data-stu-id="8e2b5-124">Remarks</span></span>  
 <span data-ttu-id="8e2b5-125">`ICLRMemoryNotificationCallback`インターフェイスが 1 つのメソッドを定義 ([iclrmemorynotificationcallback::onmemorynotification](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-onmemorynotification-method.md))、およびため`pCallback`へのポインター、 `ICLRMemoryNotificationCallback` CLR によって指定されたインスタンスは、登録は、コールバック関数自体は効果的です。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-125">Because the `ICLRMemoryNotificationCallback` interface defines only one method ([ICLRMemoryNotificationCallback::OnMemoryNotification](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-onmemorynotification-method.md)), and because `pCallback` is a pointer to an `ICLRMemoryNotificationCallback` instance provided by the CLR, the registration is effectively for the callback function itself.</span></span> <span data-ttu-id="8e2b5-126">ホストが呼び出す`OnMemoryNotification`標準の Win32 を使用するのではなく、メモリ不足の状態を報告する、`CreateMemoryResourceNotification`関数。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-126">The host invokes `OnMemoryNotification` to report memory pressure conditions, rather than using the standard Win32 `CreateMemoryResourceNotification` function.</span></span> <span data-ttu-id="8e2b5-127">詳細については、Windows プラットフォームのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-127">For more information, see the Windows Platform documentation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8e2b5-128">呼び出す`OnMemoryNotification`ブロックことはありません。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-128">Calls to `OnMemoryNotification` never block.</span></span> <span data-ttu-id="8e2b5-129">常に返すすぐにします。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-129">They always return immediately.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8e2b5-130">要件</span><span class="sxs-lookup"><span data-stu-id="8e2b5-130">Requirements</span></span>  
 <span data-ttu-id="8e2b5-131">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-131">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8e2b5-132">**ヘッダー:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="8e2b5-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="8e2b5-133">**ライブラリ:** MSCorEE.dll にリソースとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="8e2b5-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="8e2b5-134">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8e2b5-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8e2b5-135">関連項目</span><span class="sxs-lookup"><span data-stu-id="8e2b5-135">See Also</span></span>  
 [<span data-ttu-id="8e2b5-136">ICLRMemoryNotificationCallback インターフェイス</span><span class="sxs-lookup"><span data-stu-id="8e2b5-136">ICLRMemoryNotificationCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-interface.md)  
 [<span data-ttu-id="8e2b5-137">IHostMemoryManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="8e2b5-137">IHostMemoryManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)