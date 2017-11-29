---
title: "IMetaDataAssemblyImport::GetManifestResourceProps メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataAssemblyImport.GetManifestResourceProps
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataAssemblyImport::GetManifestResourceProps
helpviewer_keywords:
- GetManifestResourceProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetManifestResourceProps method [.NET Framework metadata]
ms.assetid: 00be4789-ac63-4397-b2ec-1629a5c5a585
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 29458b0b7afa5a0c0be908915b4fc91c85d28c72
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="imetadataassemblyimportgetmanifestresourceprops-method"></a><span data-ttu-id="18982-102">IMetaDataAssemblyImport::GetManifestResourceProps メソッド</span><span class="sxs-lookup"><span data-stu-id="18982-102">IMetaDataAssemblyImport::GetManifestResourceProps Method</span></span>
<span data-ttu-id="18982-103">指定されたメタデータ署名を持つマニフェスト リソースのプロパティのセットを取得します。</span><span class="sxs-lookup"><span data-stu-id="18982-103">Gets the set of properties of the manifest resource with the specified metadata signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="18982-104">構文</span><span class="sxs-lookup"><span data-stu-id="18982-104">Syntax</span></span>  
  
```  
HRESULT GetManifestResourceProps (  
    [in]  mdManifestResource   mdmr,   
    [out] LPWSTR               szName,   
    [in]  ULONG                cchName,   
    [out] ULONG                *pchName,   
    [out] mdToken              *ptkImplementation,   
    [out] DWORD                *pdwOffset,   
    [out] DWORD                *pdwResourceFlags  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="18982-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="18982-105">Parameters</span></span>  
 `mdmr`  
 <span data-ttu-id="18982-106">[in]`mdManifestResource`プロパティを取得する対象のリソースを表すトークンです。</span><span class="sxs-lookup"><span data-stu-id="18982-106">[in] An `mdManifestResource` token that represents the resource for which to get the properties.</span></span>  
  
 `szName`  
 <span data-ttu-id="18982-107">[out]リソースの名前。</span><span class="sxs-lookup"><span data-stu-id="18982-107">[out] The name of the resource.</span></span>  
  
 `cchName`  
 <span data-ttu-id="18982-108">[in]ワイド文字単位のサイズの`szName`します。</span><span class="sxs-lookup"><span data-stu-id="18982-108">[in] The size, in wide chars, of `szName`.</span></span>  
  
 `pchName`  
 <span data-ttu-id="18982-109">[out]実際に返されるワイド文字数へのポインター`szName`です。</span><span class="sxs-lookup"><span data-stu-id="18982-109">[out] A pointer to the number of wide chars actually returned in `szName`.</span></span>  
  
 `ptkImplementation`  
 <span data-ttu-id="18982-110">[out]ポインター、`mdFile`トークンまたは`mdAssemblyRef`をそれぞれ、ファイルまたはアセンブリを表すトークンをリソースが含まれています。</span><span class="sxs-lookup"><span data-stu-id="18982-110">[out] A pointer to an `mdFile` token or an `mdAssemblyRef` token that represents the file or assembly, respectively, that contains the resource.</span></span>  
  
 `pdwOffset`  
 <span data-ttu-id="18982-111">[out]ファイル内でリソースの先頭までのオフセットを指定する値へのポインター。</span><span class="sxs-lookup"><span data-stu-id="18982-111">[out] A pointer to a value that specifies the offset to the beginning of the resource within the file.</span></span>  
  
 `pdwResourceFlags`  
 <span data-ttu-id="18982-112">[out]リソースに適用されるメタデータを記述するフラグをへのポインター。</span><span class="sxs-lookup"><span data-stu-id="18982-112">[out] A pointer to flags that describe the metadata applied to a resource.</span></span> <span data-ttu-id="18982-113">フラグの値は 1 つまたは複数の組み合わせ[CorManifestResourceFlags](../../../../docs/framework/unmanaged-api/metadata/cormanifestresourceflags-enumeration.md)値。</span><span class="sxs-lookup"><span data-stu-id="18982-113">The flags value is a combination of one or more [CorManifestResourceFlags](../../../../docs/framework/unmanaged-api/metadata/cormanifestresourceflags-enumeration.md) values.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="18982-114">要件</span><span class="sxs-lookup"><span data-stu-id="18982-114">Requirements</span></span>  
 <span data-ttu-id="18982-115">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="18982-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="18982-116">**ヘッダー:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="18982-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="18982-117">**ライブラリ:** MsCorEE.dll にリソースとして使用</span><span class="sxs-lookup"><span data-stu-id="18982-117">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="18982-118">**.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="18982-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="18982-119">関連項目</span><span class="sxs-lookup"><span data-stu-id="18982-119">See Also</span></span>  
 [<span data-ttu-id="18982-120">IMetaDataAssemblyImport インターフェイス</span><span class="sxs-lookup"><span data-stu-id="18982-120">IMetaDataAssemblyImport Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)