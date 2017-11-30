---
title: "ICorDebugHeapValue2::CreateHandle メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugHeapValue2.CreateHandle
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7feef9af174a63976729f91b5a0b4967fea55b23
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugheapvalue2createhandle-method"></a><span data-ttu-id="8afbc-102">ICorDebugHeapValue2::CreateHandle メソッド</span><span class="sxs-lookup"><span data-stu-id="8afbc-102">ICorDebugHeapValue2::CreateHandle Method</span></span>
<span data-ttu-id="8afbc-103">ICorDebugHeapValue2 オブジェクトによって表されるヒープ値の指定した型のハンドルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8afbc-103">Creates a handle of the specified type for the heap value represented by this ICorDebugHeapValue2 object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8afbc-104">構文</span><span class="sxs-lookup"><span data-stu-id="8afbc-104">Syntax</span></span>  
  
```  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,   
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="8afbc-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="8afbc-105">Parameters</span></span>  
 `type`  
 <span data-ttu-id="8afbc-106">[in]作成されるハンドルの種類を指定する CorDebugHandleType 列挙型の値です。</span><span class="sxs-lookup"><span data-stu-id="8afbc-106">[in] A value of the CorDebugHandleType enumeration that specifies the type of handle to be created.</span></span>  
  
 `ppHandle`  
 <span data-ttu-id="8afbc-107">[out]このヒープ値に対して新しいハンドルを表す ICorDebugHandleValue オブジェクトのアドレスへのポインター。</span><span class="sxs-lookup"><span data-stu-id="8afbc-107">[out] A pointer to the address of an ICorDebugHandleValue object that represents the new handle for this heap value.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8afbc-108">コメント</span><span class="sxs-lookup"><span data-stu-id="8afbc-108">Remarks</span></span>  
 <span data-ttu-id="8afbc-109">ハンドルは、ヒープの値に関連付けられているアプリケーション ドメインでが作成され、アプリケーション ドメインがアンロードされると無効になります。</span><span class="sxs-lookup"><span data-stu-id="8afbc-109">The handle will be created in the application domain that is associated with the heap value, and will become invalid if the application domain gets unloaded.</span></span>  
  
 <span data-ttu-id="8afbc-110">この関数はヒープの値が同じ複数の呼び出しでは、複数のハンドルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8afbc-110">Multiple calls to this function for the same heap value will create multiple handles.</span></span> <span data-ttu-id="8afbc-111">ハンドルは、ガベージ コレクターのパフォーマンスに影響するために一度にアクティブになっているハンドル (約 256) の数を比較的小さなデバッガーに制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8afbc-111">Because handles affect the performance of the garbage collector, the debugger should limit itself to a relatively small number of handles (about 256) that are active at a time.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8afbc-112">要件</span><span class="sxs-lookup"><span data-stu-id="8afbc-112">Requirements</span></span>  
 <span data-ttu-id="8afbc-113">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="8afbc-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8afbc-114">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="8afbc-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="8afbc-115">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="8afbc-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8afbc-116">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8afbc-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>