# Psikotes Arcelio — berkas web

| Berkas | Untuk siapa |
|---|---|
| `index.html` | Pelamar — Psikotes Karakter dan Tes Jenjang SPV/Manager |
| `kognitif.html` | Pelamar — Tes Kemampuan Kognitif |
| `hrd.html` | HRD — pembuatan token, hasil tes, peringkat |
| `manifest.json`, `icon-*.png` | Ikon dan pemasangan sebagai aplikasi |

Ketiga berkas HTML harus berada di **satu folder yang sama**, karena `hrd.html`
membuat tautan relatif ke `index.html` dan `kognitif.html`, dan `index.html`
mengalihkan token kognitif ke `kognitif.html`.

## Urutan migrasi database

Jalankan berurutan di Supabase → SQL Editor:

1. `migrasi_001_modul_kognitif_REVISI.sql`
2. `migrasi_003_status_kerja.sql`
3. `migrasi_004_tingkat_puncak.sql`
4. `migrasi_005_progres_dan_penilaian.sql`
5. `seed_figural.sql`
6. `seed_spasial.sql`
7. `seed_spasial_puncak.sql`
8. `seed_numerik.sql`
9. `seed_verbal.sql`

(`migrasi_002` sudah dijalankan sebelumnya.)

## Sebelum dipakai untuk pelamar sungguhan

Seluruh soal kognitif berstatus `pilot` dan **belum akan tampil**. Aktifkan hanya
setelah piloting ke karyawan dan analisis item:

```sql
update cognitive_items set status = 'aktif'
 where status = 'pilot' and tingkat <> 'puncak';
```

Item tingkat `puncak` sengaja dibiarkan tidak aktif — dipakai nanti untuk tahap
dua posisi manajerial.
