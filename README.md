# Create_Architecture

Excel台帳からHTML構成図を生成するツール。

Windows x64向けの生成exe、編集元Excel、現在の構成図、ローカルLLM向けのExcel更新ルールを一つにまとめた配布フォルダです。台帳は架空の表示検証用データです。

[全ファイルをまとめてダウンロード（ZIP）](https://github.com/Dragongame7/Create_Architecture/archive/refs/heads/main.zip)。ダウンロード後に展開し、ArchitectureGenerator.exeを実行してください。

## 図を見る

[architecture.html](architecture.html)をダウンロードし、EdgeやChromeなどのブラウザで開いてください。HTML単体で閲覧でき、ネット接続は不要です。GitHubのファイル画面では構成図として実行されません。

図では製品の全体図・構成要素の詳細、通信・基盤・ネットワーク、拠点や製品の絞り込み、検索、詳細情報、拡大縮小、全画面表示を利用できます。今回の入力と結果は[generation_manifest.json](generation_manifest.json)、警告の内容は[report.html](report.html)にあります。

## Excelから図を作り直す

1. [inventory.xlsx](inventory.xlsx)を編集し、保存する。
2. [ArchitectureGenerator.exe](ArchitectureGenerator.exe)を起動する。
3. 保存した.xlsxを画面へドラッグ＆ドロップするか、「Excelファイルを選ぶ」で指定する。
4. 生成された図がブラウザで開く。エラーがある場合は修正箇所を示すレポートが開く。

exeはPython・画面用ライブラリ・HTML生成用ファイルを同梱した単一ファイルです。Java・Python・Node.jsの事前インストール、_internalフォルダ、管理者権限、ネット接続は不要です。変換にはExcel本体も不要で、保存済みの.xlsxを読みます。図を開くブラウザは必要です。

対象は指定の7シート形式の.xlsx台帳です。任意のExcelを推測して構成図にする機能ではありません。.xls・.xlsm・暗号化ファイル・Excelの一時ファイル（~$で始まる名前）は対象外です。数式セルはエラーになります。台帳名は変更できます。

画面からの変換結果は入力Excelの隣のoutputs/日時/へ保存します。「保存先を変更」から変更でき、「再変換」で同じ台帳を処理できます。進捗バーは変換中だけ表示します。過去の正常な結果は保持します。このフォルダ直下のarchitecture.htmlは配布時点の図であり、通常の変換では自動更新されません。

[view_settings.json](view_settings.json)はタイトルや拠点順などの表示設定です。exeの隣にある場合はこれを使い、ない場合は同梱の既定設定を使います。設定を変えた後は再生成します。

## ローカルLLMへExcel更新を依頼する

共通ルールは[LOCAL_AI_EXCEL_EDIT_PROMPT.md](LOCAL_AI_EXCEL_EDIT_PROMPT.md)、追加・変更・削除の依頼例と手順は[LOCAL_AI_HANDOFF_GUIDE.md](LOCAL_AI_HANDOFF_GUIDE.md)です。プロンプトと入力Excelを渡し、今回の変更内容を指定してください。

入力inventory.xlsxを保持し、更新候補はwork/inventory_updated.xlsxなどの別名で保存します。ローカルLLMにはExcelの読込・編集・保存機能が必要です。さらにexeを実行できる環境では、保存した候補を次のように検証できます。

```powershell
.\ArchitectureGenerator.exe --workbook ".\work\inventory_updated.xlsx" --output-root ".\work\validation" --no-open
```

LLMは終了コードと、結果フォルダ内のmanifest.json・validation.json・report.htmlを確認します。現在の架空台帳には未確認の通信情報等による警告があります。警告を消すために未確認の情報を確認済みに変更しないでください。

## GitHubへアップロードする

このフォルダの内容をアップロードすれば、利用者向け配布物が揃います。[UPLOAD_CONTENTS.md](UPLOAD_CONTENTS.md)に採用ファイルと除外ファイルを記載しています。必要なファイルを通常のリポジトリに配置する形を想定しています。

GitHubからは冒頭のZIPリンクで全ファイルをまとめて取得できます。ローカルでの配布準備時には、隣にgithub-upload.zipも作成されます。ZIPをリポジトリ内の同じファイルと重複して管理する必要はありません。

GitHubのブラウザアップロードは1ファイル25 MiBまで、同時100ファイルまでです。この配布物のexeは約12.5 MiBで、その範囲内です。[GitHub公式説明](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)

次回の配布内容を更新するときは、検証済みのExcelと、それに対応する構成図・レポートを一緒に更新してください。生成の履歴、作業候補、ビルド環境は.gitignoreで通常のGit登録対象から除外しています。GitHubのブラウザアップロードは.gitignoreを適用しないため、手動アップロードではこれらを選択しないでください。

## ライセンスと配布記録

同梱ランタイムとライブラリのライセンスは[THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt)と[ELK-LICENSE.md](ELK-LICENSE.md)にあります。配布ファイルのサイズ・SHA-256は[package_manifest.json](package_manifest.json)で確認できます。これらは第三者ライブラリのライセンスであり、このプロジェクト自体に新しい利用許諾を設定したものではありません。

ソースコード・ビルド環境はこの利用者向けフォルダに含めていません。開発用リポジトリとして公開する場合はapp/のソースとビルド手順を追加できます。
