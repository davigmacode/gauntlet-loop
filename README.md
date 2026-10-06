# Panduan Gauntlet Loop di Google Antigravity

Skill **Gauntlet Loop** dirancang untuk mendorong kualitas hasil kerja AI hingga mengalahkan standar referensi nyata (*The Bar*) melalui mekanisme perulangan terstruktur dan peran sub-agent terisolasi.

---

## 4 Variasi Workflow

| Workflow | Fokus Tugas | Peran Subagents | Kriteria Berhenti |
| :--- | :--- | :--- | :--- |
| **1. Classic Gauntlet** | UI/UX, Landing Page, Copywriting, Artikel Teknis | `Builder` vs `Harsh Critic` (Model `pro`, blind A/B) | Critic memilih hasil buatan sendiri secara blind |
| **2. Tournament Arena** | Eksplorasi Ide, Variasi Algoritma, Konsep Desain | Multi-`Builder` (branch terpisah) vs 1 `Judge` | Satu variasi terbaik memenangkan kompetisi |
| **3. Adversarial Red-Team** | Security API, Smart Contract, Parser, Logic Kritis | `Builder` vs `Breaker / Attacker` | Breaker gagal menemukan celah/crash baru |
| **4. Benchmark Driven** | Optimasi Kecepatan, Latensi, Memory, Bundle Size | `Optimizer` vs `Benchmark Runner` | Metrik numerik melampaui angka acuan |

---

## Cara Penggunaan Sehari-hari

Anda bisa menggunakan gauntlet loop dengan dua cara:

### Cara 1: Menggunakan Perintah Cepat (Triggers)
Ketik salah satu perintah berikut di awal prompt Anda:
* `/gauntlet-loop [tujuan Anda]`
* `gauntlet this: [tujuan Anda]`
* `make a gauntlet prompt untuk [tujuan Anda]`

**Contoh:**
> `/gauntlet-loop buat landing page fintech dengan referensi Stripe Checkout menggunakan mode Classic Gauntlet`

### Cara 2: Meminta Eksekusi Otonom Langsung
Anda bisa langsung meminta Antigravity menjalankannya sebagai lead orchestrator:
> *"Jalankan gauntlet loop secara langsung untuk memvalidasi algoritma kompresi data ini melawan implementasi zstd menggunakan workflow Benchmark Driven."*

---

## Di Mana Menemukan Skill Ini Kembali?

Jika sewaktu-waktu Anda lupa sintaks atau ingin membaca dokumentasinya:

1. **File Instruksi Utama**:
   [`~/.gemini/config/plugins/gauntlet-loop/skills/gauntlet-loop/SKILL.md`](file:///C:/Users/davigmacode/.gemini/config/plugins/gauntlet-loop/skills/gauntlet-loop/SKILL.md)
2. **Cheat Sheet Ringkas**:
   [`~/.gemini/config/plugins/gauntlet-loop/README.md`](file:///C:/Users/davigmacode/.gemini/config/plugins/gauntlet-loop/README.md)
3. **Cukup Tanyakan ke Antigravity**:
   Ketik *"bagaimana cara pakai gauntlet loop?"* atau *"tampilkan mode gauntlet loop"*, Antigravity akan otomatis membaca skill ini kembali.
