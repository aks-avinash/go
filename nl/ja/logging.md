---

copyright:
  years: 2018
lastupdated: "2018-10-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Go でのロギング
{: #logging_golang}

ログ・メッセージは、ログ・エントリーが作成された時点のマイクロサービスの状態およびアクティビティーに関するコンテキスト情報を含むストリングです。ログは、サービスでの障害がなぜどのように起こったのかを診断するために必要なもので、アプリケーション正常性のモニタリングにおいて[メトリック](appmetrics.html)の補助的な役割を果たします。

クラウド環境でのプロセスの一過性の性質を考慮すると、ログは収集されて、分析のために他の場所 (通常は一元管理の場所) に送信される必要があります。 クラウド環境でロギングを行う最も一貫性のある方法は、ログ・エントリーを標準出力とエラー・ストリームに送信する方法です (こうするとインフラストラクチャーが残りを処理します)。

## Go アプリへの Logrus サポートの追加
{: #add_logrus}

[Logrus](https://github.com/sirupsen/logrus) は、Go 用の一般的なロギング・フレームワークであり、以下のような多くの固有の利点があります。 
 * `stdout` または `stderr` へのログの書き込み
 * 各種の付加オプション
 * 構成可能なログ・メッセージ・レイアウトおよびパターン
 * さまざまなログ・カテゴリー用のログ・レベルの使用

1. Logrus を使用するには、アプリケーションのルート・ディレクトリーで次のコマンドを実行します。これにより、パッケージがインストールされ、`Gopkg.toml` ファイルに追加されます。
  ```bash
  dep ensure -add https://github.com/sirupsen/logrus
  ```
  {: codeblock}

2. これをアプリケーションで使用するために、以下のコード行を追加します。
  ```go
  import log "github.com/sirupsen/logrus"
  log.SetFormatter(&log.JSONFormatter{})
  log.SetOutput(os.Stdout)
  log.Info("My message")
  ```
  {: codeblock}

  **STDOUT 出力**:
  ```
  {"level":"info","msg":"My message","time":"2018-08-03T11:05:02-05:00"}
  ```
  {: screen}

アペンダー、ログ・レベル、および構成詳細でのログ・メッセージのカスタマイズについて詳しくは、公式の [Logrus 資料](https://godoc.org/gopkg.in/Sirupsen/logrus.v0)を参照してください。

## 次のステップ
{: #next_steps}

各デプロイメント環境でのログの表示について詳しくは、次の各ページを参照してください。
* [Kubernetes のログ](https://kubernetes.io/docs/concepts/cluster-administration/logging/)
* [Cloud Foundry のログ](https://console.bluemix.net/docs/cli/reference/bluemix_cli/bx_cli.html#ibmcloud_app_logs)
* [{{site.data.keyword.openwhisk}} のログおよびモニタリング](https://console.bluemix.net/docs/openwhisk/openwhisk_logs.html#openwhisk_logs)

ログ統合機能の使用について詳しくは、以下を参照してください。
* [{{site.data.keyword.cloud_notm}} Log Analysis](https://console.bluemix.net/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov)
* [{{site.data.keyword.cloud_notm}} Private ELK スタック](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_2.1.0.2/manage_metrics/logging_elk.html)