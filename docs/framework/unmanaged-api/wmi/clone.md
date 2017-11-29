---
title: "複製関数 (アンマネージ API リファレンス)"
description: "複製関数では、現在の 1 つの完全な複製である新しいオブジェクトを返します。"
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: Clone
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: Clone
helpviewer_keywords: Clone function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: df6a089f66ddd6f8f9a2d5677dd8dd6917fcb719
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2017
---
# <a name="clone-function"></a><span data-ttu-id="5e9da-103">複製関数</span><span class="sxs-lookup"><span data-stu-id="5e9da-103">Clone function</span></span>
<span data-ttu-id="5e9da-104">現在のオブジェクトの完全な複製である新しいオブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="5e9da-104">Returns a new object that is a complete clone of the current object.</span></span>   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="5e9da-105">構文</span><span class="sxs-lookup"><span data-stu-id="5e9da-105">Syntax</span></span>  
  
```  
HRESULT Clone (
   [in] int                  vFunc, 
   [in] IWbemClassObject*    ptr, 
   [out] IWbemClassObject**  ppCopy
); 
```  

## <a name="parameters"></a><span data-ttu-id="5e9da-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="5e9da-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="5e9da-107">[in]このパラメーターは使用されません。</span><span class="sxs-lookup"><span data-stu-id="5e9da-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="5e9da-108">[in]ポインター、 [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx)インスタンス。</span><span class="sxs-lookup"><span data-stu-id="5e9da-108">[in] A pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) instance.</span></span>

`ppCopy`  
<span data-ttu-id="5e9da-109">[out]完全なである新しいオブジェクトの唯一`ptr`です。</span><span class="sxs-lookup"><span data-stu-id="5e9da-109">[out] A new object that is a complete lone of `ptr`.</span></span> <span data-ttu-id="5e9da-110">この引数を使用できません`null`場合は、現在のオブジェクトのコピーを受信します。</span><span class="sxs-lookup"><span data-stu-id="5e9da-110">This argument cannot be `null` if it receives the copy of the current object.</span></span>

## <a name="return-value"></a><span data-ttu-id="5e9da-111">戻り値</span><span class="sxs-lookup"><span data-stu-id="5e9da-111">Return value</span></span>

<span data-ttu-id="5e9da-112">この関数によって返される次の値が定義されている、 *WbemCli.h*ヘッダー ファイル、またはすることができますに定義する定数として、コード。</span><span class="sxs-lookup"><span data-stu-id="5e9da-112">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="5e9da-113">定数</span><span class="sxs-lookup"><span data-stu-id="5e9da-113">Constant</span></span>  |<span data-ttu-id="5e9da-114">値</span><span class="sxs-lookup"><span data-stu-id="5e9da-114">Value</span></span>  |<span data-ttu-id="5e9da-115">説明</span><span class="sxs-lookup"><span data-stu-id="5e9da-115">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_FAILED` | <span data-ttu-id="5e9da-116">0x80041001</span><span class="sxs-lookup"><span data-stu-id="5e9da-116">0x80041001</span></span> | <span data-ttu-id="5e9da-117">一般的なエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="5e9da-117">There has been a general failure.</span></span> |
| `WBEM_E_INVALID_PARAMETER` | <span data-ttu-id="5e9da-118">0x80041008</span><span class="sxs-lookup"><span data-stu-id="5e9da-118">0x80041008</span></span> | <span data-ttu-id="5e9da-119">`null`パラメーターとして指定されたこの使用法ではありません。</span><span class="sxs-lookup"><span data-stu-id="5e9da-119">`null` was specified as a parameter, and it is not legal in this usage.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="5e9da-120">0x80041006</span><span class="sxs-lookup"><span data-stu-id="5e9da-120">0x80041006</span></span> | <span data-ttu-id="5e9da-121">十分なメモリが、オブジェクトを複製します。</span><span class="sxs-lookup"><span data-stu-id="5e9da-121">Not enough memory is available to clone the object.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="5e9da-122">0</span><span class="sxs-lookup"><span data-stu-id="5e9da-122">0</span></span> | <span data-ttu-id="5e9da-123">関数呼び出しに成功しました。</span><span class="sxs-lookup"><span data-stu-id="5e9da-123">The function call was successful.</span></span>  |
  
## <a name="remarks"></a><span data-ttu-id="5e9da-124">コメント</span><span class="sxs-lookup"><span data-stu-id="5e9da-124">Remarks</span></span>

<span data-ttu-id="5e9da-125">この関数への呼び出しをラップする、 [IWbemClassObject::Clone](https://msdn.microsoft.com/library/aa391436(v=vs.85).aspx)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="5e9da-125">This function wraps a call to the [IWbemClassObject::Clone](https://msdn.microsoft.com/library/aa391436(v=vs.85).aspx) method.</span></span>

<span data-ttu-id="5e9da-126">複製されたオブジェクトは、1 の参照カウントのある COM オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="5e9da-126">The cloned object is a COM object that has a reference count of 1.</span></span>

## <a name="requirements"></a><span data-ttu-id="5e9da-127">要件</span><span class="sxs-lookup"><span data-stu-id="5e9da-127">Requirements</span></span>  
 <span data-ttu-id="5e9da-128">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="5e9da-128">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5e9da-129">**ヘッダー:** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="5e9da-129">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="5e9da-130">**.NET framework のバージョン:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="5e9da-130">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5e9da-131">関連項目</span><span class="sxs-lookup"><span data-stu-id="5e9da-131">See also</span></span>  
[<span data-ttu-id="5e9da-132">WMI およびパフォーマンス カウンター (アンマネージ API リファレンス)</span><span class="sxs-lookup"><span data-stu-id="5e9da-132">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)