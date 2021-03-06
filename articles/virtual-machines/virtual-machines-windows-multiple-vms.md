---
title: "複数の仮想マシンの作成 | Microsoft Docs"
description: "Windows で複数の仮想マシンを作成するためのオプション"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.translationtype: Human Translation
ms.sourcegitcommit: 51de0e9aa1d29d0b3f3ffc4f126b8ca688be3504
ms.openlocfilehash: 5e96805f8880a30a5fc8779d8f07addb6d068c09
ms.contentlocale: ja-jp
ms.lasthandoff: 07/06/2017


---
# <a name="create-multiple-azure-virtual-machines"></a>複数の Azure 仮想マシンを作成する
似通った仮想マシンを大量に作成する必要があるシナリオは数多く見られます。 例として、ハイパフォーマンス コンピューティング (HPC)、大規模なデータ分析、スケーラブルでステートレスであることが多い中間層またはバックエンド サーバー (Web サーバーなど)、分散データベースなどがあります。

この記事では、Azure で複数の VM を作成するために使用できるオプションについて説明します。 これらのオプションは、一連の VM を手動で作成する単純な事例ではありません。 多数の VM を作成する必要がある場合、通常使用するプロセスでは、スケールをうまく調整できません。

似通った多数の VM を作成する方法の 1 つは、 *リソース ループ*の Azure Resource Manager コンストラクトを使用することです。

## <a name="resource-loops"></a>リソース ループ
リソース ループは、Azure Resource Manager テンプレート内の構文の簡略記法です。 リソース ループは、似通った構成のリソースをループで作成できます。 リソース ループを使用して、複数のストレージ アカウント、ネットワーク インターフェイス、または仮想マシンを作成できます。 リソース グループの詳細については、「 [リソース ループを使用して可用性セット内に VM を作成する](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)」を参照してください。

## <a name="challenges-of-scale"></a>スケールの課題
リソース ループは、規模に応じたクラウド インフラストラクチャのより簡単な構築とより簡潔なテンプレートの作成を実現しますが、いくつかの課題もあります。 たとえば、リソース グループを使用して 100 台の仮想マシンを作成する場合は、ネットワーク インターフェイス コントローラー (NIC) を対応する VM とストレージ アカウントに関連付ける必要があります。 VM とストレージ アカウントの数は一致しない可能性があるため、リソース ループの複数のサイズも処理する必要があります。 これらは解決可能な問題であるとはいえ、規模に応じて複雑さが大幅に増します。

スケールが弾性的に変化するインフラストラクチャが必要な場合は、別の課題が発生します。 たとえば、ワークロードに応じて VM の数を自動的に増減させる自動スケール インフラストラクチャが必要な場合です。 VM には、さまざまな数 (スケールアウトやスケールイン) に対応する統合されたメカニズムが用意されていません。 VM を削除してスケールインする場合、VM を複数の更新ドメインや障害ドメインに分散させて高可用性を保証することは容易ではありません。

さらに、リソース ループを使用すると、リソースを作成するための複数の呼び出しが基礎となるファブリックに対して行われます。 複数の呼び出しで似通ったリソースを作成するとき、Azure には、この設計を改良してデプロイの信頼性とパフォーマンスを最適化するための潜在的なチャンスがあります。 ここで、 *仮想マシン スケール セット* が登場します。

## <a name="virtual-machine-scale-sets"></a>仮想マシン スケール セット
仮想マシン スケール セットは、同一の VM のセットをデプロイおよび管理するための Azure コンピューティング リソースです。 すべての VM を同一に構成することで、VM スケール セットは、スケールインとスケールアウトを簡単に実行できます。 実行するのは、セット内の VM の数を変更するだけです。 ワークロードの需要に基づいて VM スケール セットを自動スケールするように構成することもできます。

コンピューティング リソースをスケールアウトしたりスケールインしたりする必要のあるアプリケーションでは、複数の障害ドメインと更新ドメインに対してスケール操作が暗黙的にバランシングされます。

複数のリソース (NIC、VM など) を関連付ける代わりに、VM スケール セットには一元的に構成できるネットワーク、ストレージ、仮想マシン、および拡張プロパティがあります。

VM スケールセットの概要については、 [仮想マシン スケール セットの作成に関するページ](https://azure.microsoft.com/services/virtual-machine-scale-sets/)を参照してください。 詳細な情報については、 [仮想マシン スケール セットのドキュメント](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)を参照してください。


