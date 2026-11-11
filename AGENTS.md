# AGENTS.md

> Instruksi standing yang dibaca oleh semua agent di workspace ini.
> Sesuaikan isi ini dengan project kamu, lalu commit ke Git.

## Project Overview

<!-- Contoh: "Aplikasi absensi dosen berbasis web dengan QR check-in, dashboard admin, dan laporan bulanan." -->

## Tech Stack

- **Frontend (dashboard/admin)**: template standar https://github.com/haris176/coneng-schadn-admin-studio — Next.js 16 (App Router), React 19, TypeScript strict, Tailwind v4, shadcn (`radix-nova`), Zod, React Hook Form, Zustand, TanStack Table, Biome. Lihat `agent/frontend.md` untuk detail konvensi lengkap.
- **Backend/database**: <!-- isi sesuai project, mis. PostgreSQL + Prisma / Laravel -->

> Catatan: `AGENTS.md` bawaan repo template di atas berisi konvensi teknis sangat spesifik (colocation, React Compiler, aturan Biome). Kalau proyek ini di-clone dari template tersebut, salin `AGENTS.md` bawaannya ke root proyek sebagai pelengkap file ini — jangan tulis ulang manual, supaya tidak ada dua sumber kebenaran yang beda.

## Command Penting

```bash
# install
# dev
# build
# test
# lint
```

## Konvensi Kode

- <!-- mis. pakai TypeScript strict mode, nama file kebab-case, dsb -->

## Aturan Keras (berlaku untuk semua agent)

- Jangan pernah commit file `.env` atau credential apa pun.
- Jangan jalankan perintah destruktif (`rm -rf`, `DROP TABLE`, `git push --force`) tanpa konfirmasi eksplisit dari pengguna.
- Jalankan test & lint sebelum menyatakan sebuah task selesai.
- Untuk perubahan pada skema database atau endpoint auth/payment, wajib delegasikan review ke agent `security` sebelum selesai.

## Protokol Kontinuitas Kerja (WAJIB)

- Setiap agent WAJIB membaca `PROGRESS.md` di awal sesi/task sebelum mulai bekerja.
- Sebelum mengakhiri sesi kerja atau menyerahkan tugas ke agent lain, WAJIB update `PROGRESS.md` dengan: apa yang sudah selesai, keputusan penting yang diambil, apa yang belum selesai, blocker, dan langkah berikutnya.
- Orchestrator WAJIB menyertakan ringkasan konteks relevan dari `PROGRESS.md` saat mendelegasikan task ke subagent — subagent tidak otomatis melihat seluruh riwayat percakapan.
- Commit `PROGRESS.md` ke Git di akhir setiap sesi kerja.

## Catatan Operasional

<!-- mis. "Server staging ada di CloudPanel, deploy manual via git pull + pm2 restart" -->
