---
lab:
  title: Azure Machine Learning ワークスペースを詳しく見る
---

# Azure Machine Learning ワークスペースを詳しく見る

Azure Machine Learning には、機械学習モデルをトレーニングおよび管理するためのデータ サイエンス プラットフォームが用意されています。 このラボでは、Azure Machine Learning ワークスペースを作成し、ワークスペースを操作するさまざまな方法について学びます。 このラボは、Azure Machine Learning のさまざまなコア機能と開発者ツールの入門編として設計されています。 機能について詳しく知りたい場合は、他にも探索するラボがあります。

## 開始する前に

管理レベルのアクセス権を持つ [Azure サブスクリプション](https://azure.microsoft.com/free?azure-portal=true)が必要です。

## Azure Machine Learning ワークスペースをプロビジョニングする

Azure Machine Learning ''ワークスペース'' では、モデルのトレーニングと管理に必要なすべてのリソースと資産を管理するための中心的な場所が提供されます。**** ワークスペースは、Azure portal で対話型インターフェイスを使用して、または Azure CLI と Azure Machine Learning 拡張機能を使用してプロビジョニングすることができます。 ほとんどの運用シナリオでは、CLI を使用してプロビジョニングを自動化し、反復可能な開発と運用 (*DevOps*) プロセスにリソースのデプロイを組み込めるようにすることをお勧めします。 

この演習では、Azure portal を使用して Azure Machine Learning をプロビジョニングし、すべてのオプションを調べていきます。

1. `https://portal.azure.com/` にサインインします。
2. 次の設定を使用して新しい **Azure Machine Learning** リソースを作成します。
    - **[サブスクリプション]**:"*ご自身の Azure サブスクリプション*"
    - **リソース グループ**: `rg-dp100-labs`
    - **ワークスペース名**: `mlw-dp100-labs`
    - **[リージョン]**: "*最も近い地理的リージョンを選択します*"
    - **[ストレージ アカウント]**: "*ワークスペース用に作成される既定の新しいストレージ アカウントに注目します*"
    - **[キー コンテナー]**: *ワークスペース用に作成される既定の新しいキー コンテナーです*
    - **[Application Insights]**: *ワークスペース用に作成される既定の新しい Application Insights リソースです*
    - **[コンテナー レジストリ]**: なし (*コンテナーにモデルを初めてデプロイするときに、自動的に作成されます*)
3. ワークスペースとそれに関連付けられているリソースが作成されるまで待ちます。通常、これには約 5 分かかります。 

> **注**:Azure Machine Learning ワークスペースを作成する場合、いくつかの高度なオプションを使用して、*プライベート エンドポイント*経由のアクセスを制限し、データ暗号化用のカスタム キーを指定できます。 この演習ではこれらのオプションは使用しませんが、注意してください。

## Azure Machine Learning スタジオについて調べる

"Azure Machine Learning スタジオ" は、Azure Machine Learning ワークスペースにアクセスできる Web ベースのポータルです。** Azure Machine Learning スタジオを使用してワークスペース内のすべての資産とリソースを管理できます。 

1. **rg-dp100-labs** という名前のリソース グループに移動します。
1. そのリソース グループに、Azure Machine Learning ワークスペース、Application Insights、キー コンテナー、ストレージ アカウントが含まれていることを確認します。 
1. Azure Machine Learning ワークスペースを選択します。
1. **[概要]** ページから **[スタジオの起動]** を選択します。 ブラウザーで別のタブが開き、Azure Machine Learning スタジオが開きます。
1. スタジオに表示されるすべてのポップアップを閉じます。 
1. スタジオの左側に表示されているさまざまなページに注目してください。 メニューにシンボルのみが表示されている場合は、&#9776; アイコンを選択してメニューを展開し、ページの名前を調べることができます。 
1. **[作成者]** セクションに注目します。ここには、 **[Notebooks]** 、 **[自動 ML]** 、 **[デザイナー]** が含まれています。 これらは Azure Machine Learning スタジオ内で独自の機械学習モデルを作成する 3 つの方法です。
1. **[アセット]** セクションに注目します。ここには、 **[データ]** 、 **[ジョブ]** 、 **[モデル]** などが含まれます。 資産は、モデルをトレーニングまたはスコア付けするときに使用または作成するものです。 資産は、モデルのトレーニング、デプロイ、管理に使用し、履歴を追跡するためにバージョン管理できます。
1. **[管理]** セクションに注目します。ここには、 **[コンピューティング]** 、 **[データストア]** などが含まれます。 これらは、機械学習モデルをトレーニングまたはデプロイするために必要なインフラストラクチャ リソースです。 

## トレーニング パイプラインを作成する

Azure Machine Learning ワークスペースの資産とリソースの使用について調べるために、モデルを試し、トレーニングしてみましょう。 

モデル トレーニング パイプラインを簡単に作成するには、 **[デザイナー]** を使用します。

> [!Note]
> 全体を通して、スタジオを案内するポップアップが表示されることがあります。 すべてのポップアップを閉じて無視し、このラボの手順に集中できます。

1. スタジオの左側にあるメニューから **[デザイナー]** ページを選択します。
1. **[回帰 - 自動車価格の予測 (基本)]** サンプルを選択します。 
    
    新しいパイプラインが表示されます。 パイプラインの上部に、**Automobile price data (raw)** を読み込むコンポーネントが表示されます。 このパイプラインでデータを処理し、各自動車の価格を予測する線形回帰モデルをトレーニングします。
1. ページ上部の **[送信]** を選択します。 コンピューティング先をまだ選択していないため、エラーが表示されます。 パイプラインは、コンピューティング リソースなしでは実行できません。 

コンピューティング先を作成しましょう。

## コンピューティング ターゲットを作成する

Azure Machine Learning ワークスペース内でワークロードを実行するには、コンピューティング リソースが必要です。 Azure Machine Learning の利点の 1 つは、大規模に実験とトレーニング スクリプトを実行できるクラウドベースのコンピューティングを作成できることです。

1. Azure Machine Learning スタジオで、左側のメニューから **[コンピューティング]** ページを選択します。 使用できるコンピューティング リソースは 4 種類あります。
    - **コンピューティング インスタンス**: Azure Machine Learning によって管理される仮想マシン。 データを探索し、機械学習モデルを反復的に実験する場合の開発に最適です。 
    - **コンピューティング クラスター**:実験コードをオンデマンドで処理するための、仮想マシンのスケーラブルなクラスター。 運用コードまたは自動ジョブの実行に最適です。
    - **推論クラスター**: 推論時に使用される Kubernetes クラスター。 大規模なリアルタイムのモデル デプロイに最適です。
    - **アタッチされたコンピューティング**: Virtual Machines や Azure Databricks クラスターなどの既存の Azure コンピューティング リソースをワークスペースにアタッチします。

デザイナーで作成した機械学習モデルをトレーニングするには、コンピューティング インスタンスまたはコンピューティング クラスターを使用できます。

2. **コンピューティング インスタンス** タブで、次の設定を使用して新しいコンピューティング インスタンスを追加します。 
    - **[コンピューティング名]**: "*一意の名前を入力します*"
    - **場所**: "自動的にワークスペースと同じ場所になります"**
    - **仮想マシンの種類**: `CPU`
    - **仮想マシンのサイズ**: `Standard_DS11_v2`
    - **使用可能なクォータ**: 使用できる専用コアが表示されます。
    - **詳細設定の表示**:次の設定に注意しますが、選択しないでください。
        - **SSH アクセスを有効にする**: `Unselected` "(これを使って、SSH クライアントを使用した仮想マシンへの直接アクセスを有効にすることができます)"**
        - **仮想ネットワークの有効化**: `Unselected` "(通常、これをエンタープライズ環境で使用してネットワーク セキュリティを強化します)"**
        - **別のユーザーに割り当てる**: `Unselected` "(これを使用して、コンピューティング インスタンスをデータ サイエンティストに割り当てることができます)"**
        - **セットアップ スクリプトを使用したプロビジョニング**: `Unselected` "(これを使用して、作成時にリモート インスタンスで実行するスクリプトを追加できます)"**

3. **[作成]** を選択し、コンピューティング インスタンスが起動して状態が **[実行中]** に変わるまで待ちます。

> **注**:コンピューティング インスタンスとクラスターは、標準の Azure 仮想マシン イメージに基づいています。 この演習では、コストとパフォーマンスの最適なバランスを実現するために、*Standard_DS11_v2* イメージが推薦されます。 サブスクリプションに、このイメージを含まないクォータが存在する場合は、代替イメージを選択します。ただし、大きなイメージはコストを上昇させる可能性があり、小さなイメージはタスクを完了するには十分でない可能性があることに注意してください。 または、Azure 管理者にクォータを拡張するように依頼します。

## トレーニング パイプラインを実行します。

コンピューティング先を作成したので、デザイナーでサンプル トレーニング パイプラインを実行できるようになりました。

1. **[デザイナー]** ページに移動します。
1. **[従来の事前構築済み]** タブを選択します。
1. **[回帰 - 自動車価格の予測 (基本)]** パイプライン ドラフトを選択します。
1. 右上にある **[設定]** を選択して、 **[設定]** ペインを展開します。
1. **[コンピューティングの種類の選択]** で、 **[コンピューティング インスタンス]** を選択します。
1. **[Azure ML コンピューティング クラスターを選択する]** で、この新しく作成したコンピューティング インスタンスを選択します。 
1. **[送信]** を選択して、トレーニング パイプラインをもう一度実行します。
1. パイプライン ジョブを設定するためのポップアップが表示されます。 次の設定を使用して新しいパイプライン ジョブを構成し、送信します。
    - **実験**: `Create new`
    - **新しい実験名**: `train-regression-designer`
    - その他は既定の設定のままにします。

これで、トレーニング パイプラインがコンピューティング インスタンスに送信されます。 パイプラインが完了するまで 10 分程度かかります。 その間に他のページを調べてみましょう。

## ジョブを使用して履歴を表示する

Azure Machine Learning ワークスペースでスクリプトまたはパイプラインを実行するたびに、それが**ジョブ**として記録されます。 ジョブを使用すると、実行したワークロードを追跡し、それらを相互に比較できます。 ジョブは **[実験]** に属していて、それによりジョブの実行をグループ化できます。

1. Azure Machine Learning スタジオの左側にあるメニューを使用して、 **[ジョブ]** ページに移動します。
1. **train-regression-designer** という実験を選択して、ジョブの実行を表示します。 ここでは、この実験に含まれるすべてのジョブの概要を確認できます。 複数のトレーニング パイプラインを実行した場合、このビューを使用すると、パイプラインを比較し、最適なものを特定できます。
1. **train-regression-designer** の実験で最後のジョブを選択します。
1. トレーニング パイプラインが表示され、どのコンポーネントが正常に実行されたか失敗したかを確認できます。 ジョブがまだ実行中の場合は、現在実行されている内容を特定することもできます。
1. パイプライン ジョブの詳細を表示するには、右上にある **[ジョブの概要]** を選択して **[パイプライン ジョブの概要]** を展開します。 
1. **[概要]** のパラメーターのでは、(特に) ジョブの状態、パイプラインを作成したユーザー、作成日時、パイプライン全体の実行にかかった時間を確認できることに注意してください。

    スクリプトまたはパイプラインをジョブとして実行するときは、任意の入力を定義し、出力を文書化できます。 Azure Machine Learning では、ジョブのプロパティも自動的に追跡されます。 ジョブを使用すると、履歴を簡単に表示して、自分または同僚が既に行ったことを理解できます。 
    
    実験中、ジョブは、比較によって最適なモデルを特定するために、トレーニングするさまざまなモデルを追跡するのに役立ちます。 運用環境では、ジョブを使用して、自動化されたワークロードが想定どおりに実行されたかどうかを確認できます。

1. ジョブが完了したら、出力を含む個々のコンポーネントの実行の詳細を表示することもできます。 パイプラインを自由に調べて、モデルのトレーニング方法を理解してください。

## Azure リソースを削除する

Azure Machine Learning を調べ終わったら、不要な Azure のコストを避けるために作成したリソースを削除する必要があります。

1. [Azure Machine Learning スタジオ] タブを閉じて、Azure portal に戻ります。
1. Azure portal の **[ホーム]** ページで、**[リソース グループ]** を選択します。
1. **rg-dp100-labs** リソース グループを選択します。
1. リソース グループの **[概要]** ページの上部で、**[リソース グループの削除]** を選択します。 
1. リソース グループ名を入力して、削除することを確認し、**[削除]** を選択します。