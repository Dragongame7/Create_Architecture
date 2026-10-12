# GitHubへアップロードするもの

## このフォルダに含めたファイル

|ファイル|用途|
|---|---|
|ArchitectureGenerator.exe|Windows x64の単一exe。進捗バーの修正版|
|inventory.xlsx|編集元の7シート台帳。元ファイルと同じ内容|
|architecture.html|同梱Excelと設定から最新exeで再生成した構成図|
|report.html|今回の生成結果とエラー・警告|
|generation_manifest.json|生成日時、入力のハッシュ、レコード件数|
|validation.json|生成時のエラー・警告の詳細|
|view_settings.json|同梱図の生成に使った表示設定|
|LOCAL_AI_EXCEL_EDIT_PROMPT.md|ローカルLLMのExcel更新用共通プロンプト|
|LOCAL_AI_HANDOFF_GUIDE.md|プロンプトとExcelの渡し方、追加・変更・削除の例|
|README.md|ダウンロード後の使い方とGitHub配置の案内|
|UPLOAD_CONTENTS.md|この整理表|
|THIRD_PARTY_LICENSES.txt / ELK-LICENSE.md|同梱ライブラリ等のライセンス|
|package_manifest.json|各配布ファイルのサイズとSHA-256|
|.gitignore|作業・生成履歴・一時ファイルのGit登録を抑制|

すべて同じフォルダ直下に置いています。図・レポート内の入力名はinventory.xlsxに統一し、作成者のローカル絶対パスは配布資料から除いています。台帳データや警告はそのまま保持しています。

## 今回のアップロードに含めないもの

|対象|理由|
|---|---|
|.build/、packaging-env/、PyInstaller作業フォルダ|生成に不要な開発・ビルド環境|
|旧exe、_internal/、distribution-backup-*|旧版または単一exe内部と重複する依存ファイル|
|outputs/の過去履歴と検証用HTML|配布する最新の図で足りるため|
|source.xlsxの複製、CSVの複製|編集元Excelと重複し、必要なときにexeで再生成できるため|
|work/内の更新候補、失敗した台帳、technical_error.txt|作業途中のデータや端末固有のログ|
|画面検証PNG・NDJSON、__pycache__/|利用者の更新・変換に不要|
|開発用の設計検討書とテストスクリプト|今回の利用者向け配布には不要|

ソースコードも管理したい場合は、開発用としてapp/とIMPLEMENTATION.mdを別途追加します。その場合も.build/と仮想環境は追加しません。現在のフォルダはExcel更新・図の閲覧・再生成を行う利用者向けです。

## 配布の更新

現在のフォルダは配布用のコピーです。開発側の元ファイルはdetail_architecture/distribution/にあります。元ファイルやexeを更新した後は、app/prepare_github_upload.pyをビルド用Pythonで実行すると、台帳から図を再生成し、このフォルダと隣のZIPを更新します。変更した配布用ファイルがある場合は、元ファイルにも反映してから再作成してください。

公開先：[Dragongame7/Create_Architecture](https://github.com/Dragongame7/Create_Architecture)。
