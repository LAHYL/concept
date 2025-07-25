<h1 align="center">

<img width="256" alt="Image" src="https://github.com/user-attachments/assets/80bb1996-209c-4821-b376-051986fb9f45" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

Stable Diffusion で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## アーキテクチャ

```mermaid
graph TD

  %% ==== User ====
  User["🧑‍💻 ユーザー"]
  User -->|アクセス| CF

  %% ==== Frontend ====
  subgraph フロントエンド
    CF["🌐 Cloudflare (CDN)"]
    Pages["📄 Cloudflare Pages (SSR)"]
    Framework["🧱 Next.js / Nuxt"]
    CF --> Pages
    Pages --> Framework
  end

  %% ==== Backend ====
  subgraph バックエンド
    CloudRun["☁️ Cloud Run"]
    CSharp["💻 C# (API)"]
    Framework -->|API Request| CloudRun
    CloudRun --> CSharp
    CSharp -->|"Search / Prompt"| ESNode
  end

  %% ==== Elasticsearch on VPS ====
  ESNode["🖥️ Conoha VPS (Elasticsearch)"]

  %% ==== Storage ====
  subgraph ストレージ
    R2["🗂️ Cloudflare R2"]
  end

  %% ==== AI ====
  subgraph AI
    ConohaAI["🧠 Conoha VPS (AI)"]
    SD["🎨 Stable Diffusion"]
    Python["🐍 Python"]
    ESNode -->|Prompt| Python
    ConohaAI --> SD
    SD --> Python
    Python -->|Upload| R2
  end

  %% CDN - R2 Cache
  CF -->|CDN Cache| R2
```

- フロントエンド

  - Cloudflare Pages(SSR)
  - Next.js or Nuxt

- バックエンド

  - Cloud Run
  - C#

- DB

  - Elasticsearch
  - Conoha VPS

- ストレージ

  - Cloudflare R2

- CDN

  - Cloudflare

- AI
  - Stable Diffusion(Realistic_Vision_V5)
  - Conoha VPS
  - Python
