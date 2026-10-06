---
name: gauntlet-loop
description: Turns any goal into a high-standard iterative gauntlet loop prompt or directly orchestrates multi-agent iterations. Sets a concrete quality bar, splits work into verifiable pieces, runs builder and harsh critic/judge subagents with fresh context, compares blind or benchmarks against the bar, and loops until victory. Supports 4 specialized workflows: Classic A/B, Tournament Arena, Adversarial Red-Team, and Benchmark Driven. Triggers on "/gauntlet-loop", "gauntlet loop", "gauntlet this", "make a gauntlet prompt", "loop until it beats X".
---

# Gauntlet Loop for Antigravity

Menghasilkan prompt siap pakai atau mengorkestrasi eksekusi multi-agent secara otonom hingga hasil pekerjaan mengalahkan standar referensi nyata (*The Bar*).

---

## 4 Variasi Workflow Gauntlet Loop

Pilih workflow yang paling sesuai dengan jenis tugas:

### 1. Classic Gauntlet (1-on-1 Blind A/B)
* **Cocok untuk**: UI/UX design, landing page, copywriting, technical writing, diagram visual.
* **Arsitektur Subagents**:
  * `Builder` (Model: `flash` atau `inherit`, write tools aktif).
  * `Harsh Critic` (Model: `pro`, context bersih, tanpa bias terhadap usaha builder).
* **Mekanisme**: Critic membandingkan output vs referensi asli secara blind (label nama disamarkan), memilih yang terbaik, dan menyebutkan 1 kelemahan paling krusial untuk diperbaiki builder.

### 2. Tournament Arena (Multi-Builder vs 1 Judge)
* **Cocok untuk**: Eksplorasi konsep kreatif, variasi desain frontend, pemilihan arsitektur/algoritma.
* **Arsitektur Subagents**:
  * 2–3 `Builder` independen dengan strategi berbeda (gunakan `Workspace: 'branch'` agar tidak bentrok direktori).
  * 1 `Judge / Referee` (Model: `pro`).
* **Mekanisme**: Seluruh variasi diadu satu sama lain dan dibandingkan dengan The Bar. Pemenang dipilih untuk iterasi babak berikutnya.

### 3. Adversarial Red-Team (Builder vs Breaker)
* **Cocok untuk**: Backend security, autentikasi, parser data, smart contract, business logic kritis.
* **Arsitektur Subagents**:
  * `Builder`: Mengimplementasikan fitur dan unit test standar.
  * `Breaker / Red Team`: Mengirim input malformed, race conditions, edge-cases, dan payload untuk merusak kode.
* **Mekanisme**: Loop berhenti hanya jika Breaker kehabisan skenario eksploitasi/kerusakan (zero unhandled exceptions & pass 100% boundary tests).

### 4. Benchmark Driven (Measurable Performance)
* **Cocok untuk**: Optimasi latensi/kecepatan, bundle size web, efisiensi memori, query database.
* **Arsitektur Subagents**:
  * `Optimizer`: Melakukan refactoring dan tuning kode.
  * `Benchmark Runner`: Menjalankan profiling di sandbox Antigravity dan mengukur metrik objektif (ms, KB, FPS, pass rate).
* **Mekanisme**: Loop otomatis selesai hanya ketika metrik target berhasil melampaui metrik kompetitor/referensi.

---

## Alur Kerja Agen (Execution Flow)

1. **Identifikasi Goal & Pilih Workflow**: Tentukan goal utama dan workflow mana yang paling relevan dari 4 mode di atas.
2. **Tetapkan The Bar (Standar Acuan)**:
   * **Named**: Nama spesifik produk/repo/artikel (misal: "Stripe Checkout", "Ripgrep CLI benchmark").
   * **Fetchable**: Dapat diambil/diinspeksi langsung (URL, file lokal, repo, screenshot).
   * **Comparable**: Dapat diuji secara A/B atau diukur dengan angka pasti.
   *(Jika user belum menyertakan referensi, tawarkan 2–3 pilihan standar acuan terlebih dahulu)*.
3. **Pilihan Eksekusi**:
   * **Opsi A (Hasilkan Prompt)**: Berikan satu blok prompt siap tempel yang ringkas (120–180 kata).
   * **Opsi B (Eksekusi Langsung via Subagents)**: Agen langsung menjalankan `define_subagent` dan `invoke_subagent` untuk mengorkestrasi perulangan secara otomatis.
4. **Pelaporan Kemajuan**: Catat progress perbandingan dan skor tiap putaran ke dalam berkas **Artifact Antigravity** agar user dapat memantau evolusi hasil secara langsung.

---

## Template Prompt Siap Pakai (Antigravity Native)

Gunakan template ini saat menghasilkan prompt untuk user:

```text
Build [GOAL].

The bar is [BAR]. Dapatkan referensi aslinya terlebih dahulu dan bandingkan secara langsung, bukan hanya membaca deskripsinya.
Workflow: [Pilih: Classic A/B / Tournament Arena / Adversarial Red-Team / Benchmark Driven].

Pecah tugas ini menjadi komponen-komponen terkecil yang bisa dinilai secara mandiri.
Untuk setiap komponen, jalankan subagent Builder (model: inherit/flash) dan Harsh Critic (model: pro) dengan context bersih melalui invoke_subagent.
Critic harus menilai secara objektif/blind tanpa memuji, menaruh hasil kita berdampingan dengan referensi asli, dan menyebutkan 1 gap terbesar yang tersisa.

Gunakan mode /goal dan terus lakukan iterasi sampai Critic memilih hasil buatan kita secara blind.
Catat riwayat dan perkembangan iterasi ke dalam Artifacts Antigravity agar prosesnya terpantau.
```

---

## Aturan Penting

* **Jangan biarkan Builder menilai karyanya sendiri**: Penilai harus selalu memiliki konteks terpisah (sub-agent mandiri).
* **Hindari batasan iterasi statis (N rounds)**: Kriteria keluar dari loop adalah menang melawan *The Bar*, bukan jumlah putaran tertentu.
* **Kritik harus tajam (*Harsh Critic*)**: Nilai biner atau A/B langsung lebih efektif daripada skor angka yang cenderung bias melunak di tiap putaran.
