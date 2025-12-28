flowchart TD
    Start((開始)) -->|GET /| Menu[トップメニュー画面]
    
    subgraph CommonSystem [各システム共通フロー]
        direction TB
        Menu -->|システム選択| List[一覧画面 (Index)]

        %% 新規登録の流れ
        List -->|新規登録リンク| NewForm[新規登録画面 (New)]
        NewForm -->|保存ボタン (POST)| CreateProcess[データ追加処理]
        CreateProcess -->|リダイレクト| List

        %% 詳細・編集の流れ
        List -->|ID/名前クリック| Detail[詳細画面 (Show)]
        Detail -->|編集ボタン| EditForm[編集画面 (Edit)]
        EditForm -->|更新ボタン (POST)| UpdateProcess[データ更新処理]
        UpdateProcess -->|リダイレクト| Detail

        %% 削除の流れ
        List -->|削除ボタン (POST)| DeleteProcess[データ削除処理]
        DeleteProcess -->|リダイレクト| List
    end