<h1 align="center">

<img width="256" alt="Image" src="https://github.com/user-attachments/assets/80bb1996-209c-4821-b376-051986fb9f45" />
<br/>
Let AI Handle Your Look!(外見なんか AI に任せとけ)
</h1>

<br>

Stable Diffusion で作ったストリートスナップを見て楽しむファッションコーディネートサイト

## アーキテクチャ

<img width="500" alt="Image" src="https://github.com/user-attachments/assets/5975d933-8d71-45af-a24d-bb7e9f651aeb" />

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
