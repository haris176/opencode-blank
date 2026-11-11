# Tim Multi-Agent OpenCode untuk Pengembangan Aplikasi

Semua agent memakai `model: opencode/bigpickle` (gratis untuk waktu terbatas via OpenCode Zen). Ganti baris `model:` di file manapun kalau mau kembali ke provider lain — lihat catatan di `agent/security.md` khususnya.

## 1. Cara instalasi

Salin folder `agent/` ke:

- **Per-project** (direkomendasikan): `<root-proyek>/.opencode/agent/`
- **Global**: `~/.config/opencode/agent/`

Salin juga `opencode.json`, `AGENTS.md`, dan `PROGRESS.md` ke root proyek.

Struktur akhir:
```
project/
├── .opencode/
│   └── agent/
│       ├── orchestrator.md
│       ├── architect.md
│       ├── database.md
│       ├── backend.md
│       ├── frontend.md
│       ├── security.md
│       ├── qa.md
│       ├── devops.md
│       └── docs.md
├── opencode.json
├── AGENTS.md      ← isi sesuai project asli (masih kerangka)
└── PROGRESS.md     ← log kerja berjalan, diupdate tiap sesi
```

## 2. Setup awal

```bash
opencode auth login      # sambungkan provider (Zen/dll)
opencode init             # generate/update AGENTS.md dari scan repo (untuk project existing)
```

## 3. Cara pakai

```bash
opencode
```

`default_agent` sudah di-set ke `orchestrator`. Contoh:
```
Saya mau bangun aplikasi absensi dosen berbasis web, ada QR code check-in,
dashboard admin, dan laporan bulanan. Stack: Next.js + PostgreSQL.
```

Panggil subagent manual kapan saja: `@security review kode login di ...`

## 4. Kontinuitas kerja antar sesi/agent

Karena session baru di opencode dimulai kosong (kecuali resume session yang sama via `opencode --continue`/`--session <id>`), dan subagent tidak otomatis mewarisi seluruh riwayat percakapan, paket ini menambahkan `PROGRESS.md` sebagai log kerja berjalan yang WAJIB dibaca & diupdate tiap agent — aturan ini sudah ditulis di `AGENTS.md`. Commit `PROGRESS.md` ke Git di akhir tiap sesi.

## 5. Urutan kerja yang direkomendasikan (proyek baru)

1. `@architect` → 2. `@database` → 3. `@backend` + `@frontend` (paralel) → 4. `@qa` → 5. `@security` (wajib untuk auth/payment/data sensitif) → 6. `@devops` → 7. `@docs`

## 6. Template frontend standar

Semua project dashboard/admin dimulai dari **https://github.com/haris176/coneng-schadn-admin-studio** (Next.js 16 + TS + Tailwind v4 + shadcn), bukan scaffold dari nol. Konvensinya (colocation, React Compiler, Biome, semantic token) sudah tertulis di `agent/frontend.md` dan `agent/architect.md`. Saat clone template, salin juga `AGENTS.md` bawaan repo tersebut ke root proyek sebagai pelengkap `AGENTS.md` di paket ini.

## 7. Catatan soal model `opencode/bigpickle`

- Gratis untuk waktu terbatas, bukan gratis permanen — bisa berubah/hilang sewaktu-waktu.
- Stealth model (provider asli tidak dipublikasikan) — hindari untuk kode yang menyentuh data sensitif/kredensial institusi.
- Untuk `@security` dan `@architect` (keputusan berdampak besar), pertimbangkan tetap pakai model dengan provider jelas seperti `anthropic/claude-sonnet-4-6`.
- Alternatif gratis-selamanya + lebih aman untuk data sensitif: model lokal via Ollama self-hosted (lihat pembahasan sebelumnya).
