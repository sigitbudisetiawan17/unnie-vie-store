# Dokumentasi Unnie Vie Store

**Proyek:** Unnie Vie Store — Integrated E-Commerce, Store Management, and CRM System  
**Baseline:** Project Constitution v0.1 dan Project Overview v0.1  
**Tanggal paket:** 14 November 2026

## Struktur

| Dokumen | Isi |
|---|---|
| `01-project-foundation/project-constitution.md` | Pedoman dasar dan keputusan proyek yang disetujui |
| `01-project-foundation/project-overview.md` | Gambaran umum proyek |
| `02-business-analysis/business-requirements.md` | Kebutuhan bisnis dan sistem |
| `02-business-analysis/business-rules.md` | Aturan operasional yang harus dipatuhi sistem |
| `03-system-design/system-architecture.md` | Arsitektur aplikasi dan integrasi |
| `03-system-design/database-specification.md` | Rancangan entitas dan aturan data |
| `03-system-design/erd.md` | ERD konseptual awal |
| `04-feature-specifications/feature-specifications.md` | Ruang lingkup fitur dan acceptance criteria |
| `05-development-planning/task-breakdown.md` | Milestone dan urutan implementasi |

## Status dan tata kelola dokumen

- Project Constitution dan Project Overview disalin dari dokumen sumber tanpa perubahan.
- Dokumen spesifikasi lain merupakan kompilasi kerja berdasarkan keputusan proyek yang telah dibahas. Tinjau kembali sebelum implementasi.
- Jika ada konflik, Project Constitution yang telah disetujui menjadi acuan prinsip; Business Rules dan Feature Specifications menjabarkan perilaku operasional.
- Perubahan terhadap dokumen baseline harus dibahas dan disetujui. Jangan mengubahnya diam-diam.
- Database Specification dan ERD ini adalah rancangan konseptual. Belum menjadi izin untuk membuat migration sebelum M-01 dan pemeriksaan teknis selesai.

## Alur pengembangan

Specification → Planning → Task Breakdown → Implementation → Verification.

Setiap fitur harus memiliki validasi backend, otorisasi backend, transaksi database yang aman, pencatatan aktivitas yang relevan, dan pengujian.
