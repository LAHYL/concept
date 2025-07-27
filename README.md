<h1 align="center">

<img width="256" alt="Image" src="https://github.com/user-attachments/assets/52df7212-bdff-4bf8-b66b-258c54367fa7" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

Stable Diffusion で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## 特徴

- **運用要らず 😴** 毎日自動で 20〜30 種類※のコーディネイトが追加される
- **探したいものがすぐ見つかる 🔍** 画像生成に使用したプロンプトの内容を日本語でそのまま検索できる
  _（例：夏ファッション / T シャツ / ハーフパンツ など）_
- **検索が爆速 ⚡️** 高速検索エンジン Elasticsearch を使用しており、ストレスフリーな体験
- **安心・安全な画像利用 🔓** 生成された画像は 商用利用可 / 著作権問題なし

※ 最弱マシンの場合

## アーキテクチャ

```mermaid
graph TD

  %% ==== User ====
  User["🧑‍💻 User"]
  User --> CF

  %% ==== Frontend ====
  subgraph "🖥️ Web"
    CF["🌐 Cloudflare (CDN)"]
    Workers["📄 Cloudflare Workers (SSR)"]
    Framework["🧱 Next.js"]
    CF --> Workers
    Workers --> Framework
  end

  %% ==== Backend ====
  subgraph "🔧 Api"
    Workers["⚙️ Cloudflare Workers"]
    Hono["🛠️ Hono (API)"]
    Framework -->|API Request| Workers
    Workers --> Hono
  end

  %% ==== DB ====
  subgraph "🗄️ Database"
    ESNode["🖥️ Conoha VPS (Elasticsearch)"]
  end

  Hono -->|"Search"| ESNode

  %% ==== Storage ====
  subgraph "💾 Storage"
    R2["🗂️ Cloudflare R2"]
  end

  %% ==== AI ====
  subgraph "🧠 AI Server"
    SD["🎨 Stable Diffusion"]
    Python["🐍 Python"]
    SD --> Python
  end

  ESNode -->|Prompt| Python
  Python -->|Upload| R2

  %% CDN - R2 Cache
  CF -->|CDN Cache| R2
```

- フロントエンド

  - Cloudflare Workers(SSR)
  - Next.js

- バックエンド

  - Cloudflare Workers
  - Hono

- DB

  - Elasticsearch
  - Conoha VPS

- ストレージ

  - Cloudflare R2

- CDN

  - Cloudflare

- AI
  - Stable Diffusion(Realistic_Vision_V5)
  - Python
