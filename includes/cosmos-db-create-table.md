これで、データ エクスプローラーを使用してテーブルを作成し、データベースにデータを追加できるようになりました。 

1. Azure Portal のナビゲーション メニューで、**[データ エクスプローラー (プレビュー)]** をクリックします。 
2. [データ エクスプローラー] ブレードで **[新しいテーブル]** をクリックし、以下の情報を使用してページに必要事項を入力します。

    ![Azure Portal のデータ エクスプローラー](./media/cosmos-db-create-table/azure-cosmosdb-data-explorer.png)

    設定|推奨値|Description
    ---|---|---
    テーブル ID|sample-table|新しいテーブルの ID。 テーブル名の文字要件はデータベース ID と同じです。 データベース名は、1 - 255 文字である必要があります。また、`/ \ # ?` は使えず、末尾にスペースを入れることもできません。
    ストレージの容量| 10 GB|既定値をそのまま使用します。 これは、データベースの記憶域容量です。
    スループット|400 RU|既定値をそのまま使用します。 待ち時間を短縮する場合、後で[スループット](../articles/cosmos-db/request-units.md)をスケールアップできます。
    RU/m|オフ|既定値を使用します。 ワークロードのスパイクに対処する必要がある場合は、後で [RU/m](../articles/cosmos-db/request-units-per-minute.md) 機能を有効にすることができます。

3. フォームに入力したら、**[OK]** をクリックします。