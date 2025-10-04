<h1 align="center">

<img width="256" alt="Image" src="https://github.com/user-attachments/assets/52df7212-bdff-4bf8-b66b-258c54367fa7" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

Stable Diffusion で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## 特徴

- **運用要らず 😴** 毎日自動で 40 種類以上※のコーディネイトが追加される
- **探したいものがすぐ見つかる 🔍** 画像生成に使用したプロンプトの内容を日本語でそのまま検索できる
  _（例：夏ファッション / T シャツ / ハーフパンツ など）_
- **検索が爆速 ⚡️** 高速検索エンジン Elasticsearch を使用しており、ストレスフリーな体験
- **安心・安全な画像利用 🔓** 生成された画像は 商用利用可 / 著作権問題なし

※ 最弱マシンの場合

## アーキテクチャ

```mermaid
graph TD
    U[👤 ユーザー]

    subgraph Frontend["🌐 Frontend"]
        FE[⚛️ Next.js（Cloudflare Workers）]
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

    %% Connections
    U --> FE
    FE --> BE
    BE --> DB
    ST --> FE
    BE --> PY
    PY --> ST
```

- **Frontend**: Next.js（Cloudflare Workers）
- **Backend**: Hono（Cloudflare Workers）
- **Database**: Elasticsearch（ConoHa VPS）
- **AI Server**: Python + Juggernaut-XL（Kaggle Notebooks）
- **Storage**: Cloudflare R2

ユーザー → Frontend → Backend を経由して、DB・AI・ストレージと連携し、生成画像は R2 に保存・配信されます。
