<h1 align="center">

<img width="256" alt="Image" src="https://github.com/user-attachments/assets/52df7212-bdff-4bf8-b66b-258c54367fa7" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

Stable Diffusion で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## アーキテクチャ

```mermaid
graph TD

  %% ==== User ====
  User["🧑‍💻 User"]
  User --> CF

  %% ==== Frontend ====
  subgraph "🖥️ Web"
    CF["🌐 Cloudflare (CDN)"]
    Pages["📄 Cloudflare Pages (SSR)"]
    Framework["🧱 Next.js"]
    CF --> Pages
    Pages --> Framework
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

  - Cloudflare Pages(SSR)
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
