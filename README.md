<h1 align="center">

<img width="256" alt="Image" src="https://private-user-images.githubusercontent.com/48668579/552489824-94d6749f-eccc-46f3-b425-2cc84ac6f288.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzE1NTk2MTEsIm5iZiI6MTc3MTU1OTMxMSwicGF0aCI6Ii80ODY2ODU3OS81NTI0ODk4MjQtOTRkNjc0OWYtZWNjYy00NmYzLWI0MjUtMmNjODRhYzZmMjg4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNjAyMjAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjYwMjIwVDAzNDgzMVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTRhNzRhZWZmZjc4YjY2MjQ0ODcxNmM3ZDI3YjE3MmZkODkxYmM3YzUxZTBmOTM5NGIyNWE3NDRhZDdkZDZhMGQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.WSewP43hwiHinidwWXY4hgeW-PP0h_jRgi_ht2wWV9c" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

生成AI で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## 特徴

- **運用最小限 😴** 毎日自動で 40 種類以上※のコーディネイトが追加される
- **探したいものがすぐ見つかる 🔍** 画像生成に使用したプロンプトの内容を日本語でそのまま検索できる
  _（例：夏ファッション / T シャツ / ハーフパンツ など）_
- **検索が爆速 ⚡️** 高速検索エンジン Elasticsearch を使用しており、ストレスフリーな体験
- **安心・安全な画像利用 🔓** 生成された画像は 商用利用可 / 著作権問題なし
- **エラーハンドリング 🛠️** Sentry で例外を監視・通知

## アーキテクチャ

```mermaid
graph TD
    U[👤 ユーザー]
    DEV[🧑‍💻 開発者]

    subgraph Frontend["🌐 Frontend"]
        FE[⚛️ Next.js 16（Cloudflare Workers）]
    end

    subgraph Edge["🛡️ Edge"]
        CW[🛡️ CDN/WAF（Cloudflare）]
    end

    subgraph Backend["🖥️ Backend"]
        BE[🚀 Hono（Cloudflare Workers）]
    end

    subgraph Database["💾 Database"]
        DB[(🔍 Elasticsearch（ConoHa VPS）)]
    end

    subgraph AI["🤖 画像生成AIサーバー"]
        PY[🐍 Python（Kaggle Notebooks）]
    end


    subgraph Storage["🗄️ Storage"]
        ST[☁️ Cloudflare R2]
    end

    subgraph Observability["📈 Observability"]
        SE[🐞 Sentry]
        SL[💬 Slack]
    end

    subgraph Analytics["📊 Analytics"]
        GA[📈 Google Analytics]
    end

    subgraph Forms["📝 Forms"]
        GF[📝 Google Forms]
    end

    subgraph ExternalAPI["🔌 External API"]
        RA[🛍️ 楽天API]
    end

    %% Connections
    U --> CW
    CW --> FE
    FE --> BE
    BE --> DB
    ST --> FE
    FE --> SE
    BE --> SE
    FE --> GA
    FE --> GF
    FE --> RA
    SE --> SL
    SL --> DEV
    DEV --> PY
    PY --> ST
```

- **Frontend**: Next.js 16（Cloudflare Workers）
- **CDN/WAF**: Cloudflare
- **Backend**: Hono（Cloudflare Workers）
- **Database**: Elasticsearch（ConoHa VPS）
- **AI Server**: Python + FLUX（Kaggle Notebooks）
- **Storage**: Cloudflare R2
- **Observability**: Sentry → Slack
- **Analytics/Forms**: Google Analytics / Google Forms
- **External API**: 楽天API

ユーザーは Cloudflare の CDN/WAF 経由で Frontend にアクセスし、Frontend から Backend・各種外部サービス（Analytics/Forms/楽天API）へ接続します。Backend は DB と Sentry に連携し、Sentry の通知は Slack 経由で開発者に届きます。画像生成は開発者が AI サーバーを実行して行い、生成結果は R2 に保存され Frontend から配信されます。
