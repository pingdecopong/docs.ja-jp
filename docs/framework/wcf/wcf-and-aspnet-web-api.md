---
title: WCF と ASP.NET Web API
ms.date: 03/30/2017
ms.assetid: 08ceded3-fd9a-4467-9715-c4cbd9c7228e
ms.openlocfilehash: c8bc8d3483d2f6c85ff14073f34caaf75d639bdf
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33504108"
---
# <a name="wcf-and-aspnet-web-api"></a>WCF と ASP.NET Web API
WCF は、サービス指向のアプリケーションを構築するための Microsoft の統一プログラミング モデルです。 これを使用して開発者は、プラットフォーム間を統合し、既存のコンポーネントと相互運用する、セキュリティで保護された信頼性の高いトランザクション型のソリューションを構築できます。 [ASP.NET Web API](http://www.asp.net/web-api)フレームワーク クライアント、ブラウザーやモバイル デバイスなどの広範な範囲に到達する HTTP サービスを構築するが容易です。 ASP.NET Web API は、.NET Framework に基づいて RESTful アプリケーションを構築するのに最適なプラットフォームです。 このトピックでは、ニーズに最適なテクノロジを決定するのに役立つガイドラインを示します。  
  
## <a name="choosing-which-technology-to-use"></a>使用するテクノロジの選択  
 各テクノロジの主な機能を次の表に示します。  
  
|WCF|ASP.NET Web API|  
|---------|---------------------|  
|複数のトランスポート プロトコル (HTTP、TCP、UDP、およびカスタム トランスポート) をサポートするサービスを構築し、構築したサービスを切り替えることができます。|HTTP のみ。 HTTP のファースト クラスのプログラミング モデル。 さまざまなブラウザーでは、ワイド到達などを有効にするモバイル デバイスからのアクセスに適しています。|  
|メッセージの種類が同じ複数のエンコーディング (テキスト、MTOM、およびバイナリ) をサポートするサービスを構築し、構築したサービスを切り替えることができます。|XML や JSON などのさまざまなメディアの種類をサポートする Web API を構築できます。|  
|Reliable Messaging、Transactions、Message Security などの WS-* 標準を使用してサービスを構築できます。|基本的なプロトコルを使用して、HTTP、Websocket、SSL、JSON、XML など形式します。 Reliable Messaging や Transactions などの高レベルのプロトコルはサポートされません。|  
|要求/応答、一方向、および双方向の各メッセージ交換パターンをサポートしています。|HTTP 要求/応答は、追加のパターンをサポートできる[SignalR](https://github.com/SignalR/SignalR)と Websocket 統合します。|  
|WCF SOAP サービスは WSDL で記述でき、スキーマが複雑なサービスの場合でも自動化ツールを使用してクライアント プロキシを生成できます。|スニペットを記述する自動生成された HTML ヘルプ ページから OData で統合された API 用に構造化されたメタデータまで、Web API を記述するためのさまざまな方法があります。|  
|.NET Framework に付属しています。|.NET Framework に付属していますが、オープン ソースであるため、個別のダウンロードとして帯域外でも使用できます。|  
  
 WCF を使用すると、さまざまなトランスポートを経由してアクセスできる、信頼性が高くセキュリティで保護された Web サービスを作成できます。 ASP.NET Web API を使用すると、さまざまなクライアントからアクセスできる HTTP ベースのサービスを作成できます。 ASP.NET Web API は、新しい REST スタイルのサービスを作成および設計する場合に使用します。 WCF では REST スタイルのサービスの作成を一部サポートしていますが、ASP.NET Web API の REST のサポートはより詳細で、以降の REST 機能の強化は ASP.NET Web API で行われる予定です。 既存の WCF サービスがあり、追加の REST エンドポイントを公開する場合は、WCF および <xref:System.ServiceModel.WebHttpBinding> を使用してください。  
  
## <a name="see-also"></a>関連項目  
 [Windows Communication Foundation とは](../../../docs/framework/wcf/whats-wcf.md)  
 [Windows Communication Foundation の基本概念](../../../docs/framework/wcf/fundamental-concepts.md)  
