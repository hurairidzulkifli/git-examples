# TUTORIAL AMALI GIT UNTUK PEMULA

### Latihan Bertulis: "Fail Senarai Nama"

**Rujukan Silibus:** Modul 1 (Asas Git), Modul 2 (Pengurusan Branch), Modul 3 (Semakan Perubahan) & Modul 7 (Senario 1)
**Anggaran Masa:** 90 – 120 minit (boleh dipecahkan kepada dua sesi)
**Tahap:** Pemula sepenuhnya (tiada pengalaman Git diperlukan)

---

## KANDUNGAN

**BAHAGIAN 1 — Aliran Kerja Asas** _(Langkah 0 – 9)_
Cipta repositori, rekod perubahan, dan semak apa yang berubah.

**BAHAGIAN 2 — Branch & Konflik** _(Langkah 10 – 23)_
Asingkan kerja menggunakan branch, gabungkan semula, dan selesaikan konflik.

---

# BAHAGIAN 1 — ALIRAN KERJA ASAS

## SEBELUM MULA: Fahami 3 "Tempat" dalam Git

Sebelum menyentuh sebarang arahan, fahami gambaran ini dahulu. Semua arahan Git yang anda pelajari hari ini hanya memindahkan fail antara **tiga tempat**:

| Tempat | Nama Teknikal         | Analogi Mudah                                                                |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| 1      | **Working Directory** | Meja kerja anda. Di sinilah anda menyunting fail.                            |
| 2      | **Staging Area**      | Kotak "sedia untuk dihantar". Anda pilih perubahan mana yang hendak direkod. |
| 3      | **Repository**        | Album kenangan. Rekod kekal yang tidak boleh hilang.                         |

Aliran perjalanan fail:

```
[Meja kerja]  --git add-->  [Kotak]  --git commit-->  [Album]
```

> **Ingat:** Menyunting fail sahaja **tidak** menyimpan apa-apa dalam Git. Anda mesti `add` dan `commit`.

---

## LANGKAH 0: Persediaan (Sekali sahaja seumur hidup)

Buka **Terminal** (Mac/Linux) atau **Git Bash** (Windows), kemudian taip:

```bash
git --version
```

Jika muncul nombor versi (contoh: `git version 2.45.0`), Git sudah dipasang. Jika ralat, maklumkan kepada fasilitator.

Seterusnya, beritahu Git siapa anda. Nama ini akan tercatat pada setiap commit anda:

```bash
git config --global user.name "Nama Penuh Anda"
git config --global user.email "emel@contoh.com"
```

Semak semula:

```bash
git config --global --list
```

---

## LANGKAH 1: Cipta Repositori Latihan

```bash
mkdir latihan-git
cd latihan-git
git init
```

**Output dijangka:**

```
Initialized empty Git repository in /home/anda/latihan-git/.git/
```

**Apa yang berlaku?** Git mencipta folder tersembunyi bernama `.git` di dalam folder anda. Folder itulah "album" yang menyimpan segala sejarah. Jangan sentuh atau padam folder tersebut.

---

## LANGKAH 2: Cipta Fail Teks

Cipta fail bernama `senarai_nama.txt`.

Pilih **satu** cara di bawah:

```bash
# Windows (Git Bash)
notepad senarai_nama.txt

# Mac / Linux
nano senarai_nama.txt

# Jika menggunakan VS Code
code senarai_nama.txt
```

Taip kandungan berikut, kemudian **simpan** fail:

```
SENARAI PESERTA LATIHAN GIT
===========================
Nama peserta:
Jabatan:
```

> Nota: Jika anda menggunakan `nano`, tekan `Ctrl + O` kemudian `Enter` untuk simpan, dan `Ctrl + X` untuk keluar.

---

## LANGKAH 3: `git status` — Arahan Paling Penting

```bash
git status
```

**Output dijangka:**

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        senarai_nama.txt

nothing added to commit but untracked files present
```

**Perhatikan:**

- **Untracked** bermaksud Git nampak fail itu, tetapi belum pernah merekodnya. Git tidak akan menjaga fail ini selagi anda tidak `add`.
- Baris `On branch main` menunjukkan anda berada di branch utama. (Pada sesetengah versi Git, namanya `master` — kedua-duanya betul.)

> **Tabiat baik:** Taip `git status` sebelum dan selepas setiap arahan. Ia percuma, selamat, dan Git akan memberitahu anda apa yang patut dibuat seterusnya.

---

## LANGKAH 4: `git add` — Masukkan ke dalam "Kotak"

```bash
git add senarai_nama.txt
git status
```

**Output dijangka:**

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   senarai_nama.txt
```

**Perhatikan:** Fail kini berada di bawah **"Changes to be committed"**. Ia sudah masuk ke dalam kotak (staging area), tetapi **belum lagi** direkod secara kekal.

---

## LANGKAH 5: `git commit` — Rekod Kekal Pertama

```bash
git commit -m "Tambah fail senarai nama peserta"
```

**Output dijangka:**

```
[main (root-commit) a1b2c3d] Tambah fail senarai nama peserta
 1 file changed, 4 insertions(+)
 create mode 100644 senarai_nama.txt
```

**Perhatikan:**

- `a1b2c3d` ialah **ID commit**. Setiap commit mempunyai ID unik.
- `-m` bermaksud _message_. **Sentiasa** gunakan `-m`. Jika anda terlupa, Git akan membuka editor teks yang mengelirukan bagi pemula.

> **Jika anda tersilap dan skrin pelik terbuka:** tekan `Esc`, taip `:q!`, kemudian tekan `Enter`. Itu cara keluar dari editor `vim`.

Semak semula:

```bash
git status
```

Sepatutnya kini keluar: `nothing to commit, working tree clean` — bermaksud semua kemas dan tersimpan.

---

## LANGKAH 6: Sunting Fail — Masukkan Nama Anda

Buka semula `senarai_nama.txt` dan **ubah** dua baris supaya menjadi seperti ini (guna nama sebenar anda):

```
SENARAI PESERTA LATIHAN GIT
===========================
Nama peserta: Ahmad bin Ismail
Jabatan: Bahagian Pembangunan Sistem
```

Simpan fail, kemudian:

```bash
git status
```

**Output dijangka:**

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   senarai_nama.txt

no changes added to commit
```

**Perhatikan:** Status berubah daripada _untracked_ kepada **modified**. Git tahu fail ini pernah direkod, dan kini ia berbeza daripada rekod terakhir.

---

## LANGKAH 7: `git diff` — Lihat APA yang Berubah

`git status` memberitahu **fail mana** yang berubah. `git diff` memberitahu **baris mana** yang berubah.

```bash
git diff
```

**Output dijangka:**

```diff
diff --git a/senarai_nama.txt b/senarai_nama.txt
index 8f2c1a4..3e9b7d2 100644
--- a/senarai_nama.txt
+++ b/senarai_nama.txt
@@ -1,4 +1,4 @@
 SENARAI PESERTA LATIHAN GIT
 ===========================
-Nama peserta:
-Jabatan:
+Nama peserta: Ahmad bin Ismail
+Jabatan: Bahagian Pembangunan Sistem
```

### Cara membaca output ini:

| Simbol                   | Maksud                                           |
| ------------------------ | ------------------------------------------------ |
| `--- a/fail`             | Versi **lama** (rekod terakhir)                  |
| `+++ b/fail`             | Versi **baharu** (di meja kerja anda)            |
| `@@ -1,4 +1,4 @@`        | Perubahan bermula di baris 1                     |
| Baris dengan `-` (merah) | Baris yang **dibuang**                           |
| Baris dengan `+` (hijau) | Baris yang **ditambah**                          |
| Baris tanpa simbol       | Tidak berubah, dipaparkan sebagai rujukan sahaja |

> **Nota:** Menukar satu baris dipaparkan sebagai satu baris dibuang (`-`) dan satu baris ditambah (`+`). Ini normal.
>
> Jika output panjang dan terperangkap di skrin, tekan **`q`** untuk keluar.

---

## LANGKAH 8: `git diff --staged` — Perbezaan Penting

Sekarang masukkan perubahan ke dalam kotak:

```bash
git add senarai_nama.txt
git diff
```

**Output: kosong!** Ramai pemula panik di sini. Jangan risau — ini betul.

**Sebabnya:** `git diff` hanya membandingkan **meja kerja** dengan **kotak**. Oleh sebab kedua-duanya sudah sama, tiada apa-apa untuk dipaparkan.

Untuk melihat perubahan yang sudah berada di dalam kotak, gunakan:

```bash
git diff --staged
```

Perubahan tadi muncul semula.

### Ringkasan tiga jenis perbandingan

| Arahan              | Membandingkan                                                  |
| ------------------- | -------------------------------------------------------------- |
| `git diff`          | Meja kerja ↔ Kotak (perubahan yang **belum** di-`add`)         |
| `git diff --staged` | Kotak ↔ Album (perubahan yang **sudah** di-`add`)              |
| `git diff HEAD`     | Meja kerja ↔ Album (**semua** perubahan sejak commit terakhir) |

Cuba ketiga-tiganya sekarang dan bandingkan hasilnya:

```bash
git diff
git diff --staged
git diff HEAD
```

---

## LANGKAH 9: Commit Kedua & Lihat Sejarah

```bash
git commit -m "Isi nama dan jabatan peserta"
git log --oneline
```

**Output dijangka:**

```
7d4e2f1 Isi nama dan jabatan peserta
a1b2c3d Tambah fail senarai nama peserta
```

Untuk sejarah penuh berserta tarikh dan nama pengarang:

```bash
git log
```

Tekan **`q`** untuk keluar.

---

## SEMAKAN PERTENGAHAN

Sebelum meneruskan ke Bahagian 2, jawab tanpa merujuk nota:

1. Apakah perbezaan antara _untracked_ dan _modified_?
2. Selepas `git add`, mengapa `git diff` menjadi kosong?
3. Anda menyunting fail tetapi belum commit. Apakah arahan untuk melihat baris mana yang berubah?
4. Bagaimana untuk keluar daripada paparan `git log`?

> **Pastikan repositori anda bersih** (`nothing to commit, working tree clean`) sebelum meneruskan.

---

# BAHAGIAN 2 — BRANCH & KONFLIK

## SEBELUM MULA: Apa Itu Branch dan Konflik?

**Branch** ialah salinan kerja yang berasingan. Ia membolehkan anda mencuba sesuatu tanpa menjejaskan kerja utama. Jika berjaya, anda gabungkan semula. Jika gagal, anda buang sahaja branch itu.

**Konflik** pula **bukan ralat**. Ia **bukan** bermakna Git rosak atau anda buat silap.

Konflik berlaku apabila dua branch mengubah **baris yang sama** dalam **fail yang sama**. Git tidak berani meneka mana satu yang betul, jadi ia berhenti dan bertanya kepada anda.

Analogi mudah:

> Dua orang menyunting satu dokumen yang sama. Seorang menulis "Bahagian Digital" pada baris 4. Seorang lagi menulis "Bahagian Teknologi Maklumat" pada baris 4 yang sama. Apabila kedua-dua salinan digabungkan, Git bertanya: **"Yang mana satu anda mahu?"**

**Kesimpulan penting:** Tugas anda semasa konflik hanyalah _memilih_ atau _menggabungkan_ teks, kemudian beritahu Git anda sudah selesai.

> **Butang keselamatan:** Jika anda keliru atau panik pada bila-bila masa, taip `git merge --abort`. Semuanya akan kembali kepada keadaan sebelum merge. Tiada apa-apa yang hilang.

---

## LANGKAH 10: Cipta Branch Pertama

```bash
git branch
```

**Output:** `* main` — anda hanya ada satu branch buat masa ini. Tanda `*` menunjukkan branch semasa anda.

Cipta dan terus masuk ke branch baharu:

```bash
git switch -c tambah-tarikh
```

**Output dijangka:**

```
Switched to a new branch 'tambah-tarikh'
```

> Arahan lama `git checkout -b tambah-tarikh` juga berfungsi sama. `git switch` ialah kaedah semasa yang disyorkan.

---

## LANGKAH 11: Buat Perubahan di Branch Baharu

Buka `senarai_nama.txt` dan **tambah satu baris di bahagian bawah**:

```
SENARAI PESERTA LATIHAN GIT
===========================
Nama peserta: Ahmad bin Ismail
Jabatan: Bahagian Pembangunan Sistem
Tarikh latihan: 06/09/2026
```

Simpan, kemudian gunakan kemahiran Bahagian 1:

```bash
git status
git diff
git add senarai_nama.txt
git commit -m "Tambah tarikh latihan"
```

---

## LANGKAH 12: Merge Yang Berjaya (Tiada Konflik)

Kembali ke branch utama:

```bash
git switch main
```

Buka `senarai_nama.txt` sekarang. **Baris tarikh sudah hilang!**

Jangan panik — ini normal. Baris itu wujud di branch `tambah-tarikh`, bukan di `main`. Inilah tujuan branch: mengasingkan kerja.

Gabungkan:

```bash
git merge tambah-tarikh
```

**Output dijangka:**

```
Updating a1b2c3d..9f8e7d6
Fast-forward
 senarai_nama.txt | 1 +
 1 file changed, 1 insertion(+)
```

Buka fail semula — baris tarikh sudah kembali.

**Apa itu "Fast-forward"?** Branch `main` tidak berubah langsung sejak branch dicipta, jadi Git hanya perlu "maju ke hadapan" mengikut branch tadi. Tiada apa-apa untuk dipertikaikan, jadi **tiada konflik**.

---

## LANGKAH 13: Buang Branch Yang Sudah Selesai

```bash
git branch -d tambah-tarikh
git branch
```

Branch yang sudah digabungkan tidak lagi diperlukan. Membuangnya ialah amalan kemas.

---

## LANGKAH 14: Cipta Konflik Dengan Sengaja (Bahagian Pertama)

Sekarang kita akan **sengaja** cipta konflik supaya anda tahu rupanya dan cara menanganinya.

```bash
git switch -c tukar-jabatan
```

Buka `senarai_nama.txt` dan ubah **baris 4** sahaja:

```
Jabatan: Bahagian Teknologi Maklumat
```

Simpan, kemudian:

```bash
git add senarai_nama.txt
git commit -m "Tukar jabatan kepada Teknologi Maklumat"
```

---

## LANGKAH 15: Ubah BARIS YANG SAMA di `main`

```bash
git switch main
```

Buka `senarai_nama.txt`. Baris 4 kembali kepada nilai asal. Ubah pula kepada teks yang **berbeza**:

```
Jabatan: Bahagian Digital
```

Simpan, kemudian:

```bash
git add senarai_nama.txt
git commit -m "Tukar jabatan kepada Digital"
```

**Keadaan sekarang:** Dua branch, dua jawapan berbeza, pada baris yang sama. Inilah bahan konflik.

---

## LANGKAH 16: Cuba Gabungkan — Konflik Muncul

```bash
git merge tukar-jabatan
```

**Output dijangka:**

```
Auto-merging senarai_nama.txt
CONFLICT (content): Merge conflict in senarai_nama.txt
Automatic merge failed; fix conflicts and then commit the result.
```

**Tahniah — anda baru sahaja mencipta konflik pertama anda.** Ini yang kita mahukan.

---

## LANGKAH 17: Tanya Git Apa Yang Berlaku

```bash
git status
```

**Output dijangka:**

```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   senarai_nama.txt

no changes added to commit
```

**Perhatikan:** Status baharu — **`both modified`**. Ini penanda khusus konflik.

---

## LANGKAH 18: Baca Penanda Konflik

Buka `senarai_nama.txt`. Git telah menulis penanda khas ke dalam fail anda:

```
SENARAI PESERTA LATIHAN GIT
===========================
Nama peserta: Ahmad bin Ismail
<<<<<<< HEAD
Jabatan: Bahagian Digital
=======
Jabatan: Bahagian Teknologi Maklumat
>>>>>>> tukar-jabatan
Tarikh latihan: 06/09/2026
```

### Cara membaca penanda konflik

| Penanda                 | Maksud                                                            |
| ----------------------- | ----------------------------------------------------------------- |
| `<<<<<<< HEAD`          | Mula bahagian versi **branch semasa anda** (`main`)               |
| Teks selepasnya         | Versi **anda** — "Bahagian Digital"                               |
| `=======`               | Garis pemisah antara dua versi                                    |
| Teks selepasnya         | Versi **branch yang digabungkan** — "Bahagian Teknologi Maklumat" |
| `>>>>>>> tukar-jabatan` | Tamat bahagian, beserta nama branch berkenaan                     |

**Petua mengingat:** Yang **atas** ialah tempat anda berdiri sekarang. Yang **bawah** ialah yang datang masuk.

---

## LANGKAH 19: Sunting Fail Secara Manual

Anda mempunyai tiga pilihan:

**Pilihan 1 — Ambil versi anda:**

```
Jabatan: Bahagian Digital
```

**Pilihan 2 — Ambil versi branch lain:**

```
Jabatan: Bahagian Teknologi Maklumat
```

**Pilihan 3 — Gabungkan kedua-duanya:**

```
Jabatan: Bahagian Digital dan Teknologi Maklumat
```

Untuk latihan ini, pilih **Pilihan 3**. Fail anda sepatutnya menjadi seperti berikut:

```
SENARAI PESERTA LATIHAN GIT
===========================
Nama peserta: Ahmad bin Ismail
Jabatan: Bahagian Digital dan Teknologi Maklumat
Tarikh latihan: 06/09/2026
```

> **SANGAT PENTING:** Buang **semua** baris `<<<<<<<`, `=======` dan `>>>>>>>`. Penanda ini bukan sebahagian daripada kod atau teks anda. Jika tertinggal, ia akan tercommit ke dalam repositori dan menyebabkan masalah kepada seluruh pasukan.

Simpan fail.

---

## LANGKAH 20: Beritahu Git Anda Sudah Selesai

```bash
git add senarai_nama.txt
git status
```

**Output dijangka:**

```
On branch main
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
```

**Perhatikan:** `git add` semasa konflik bermaksud **"saya sudah selesaikan fail ini"**, bukan sekadar memasukkan ke staging area.

---

## LANGKAH 21: Commit Untuk Menamatkan Merge

```bash
git commit -m "Selesaikan konflik pada baris jabatan"
```

**Output dijangka:**

```
[main 5c6d7e8] Selesaikan konflik pada baris jabatan
```

---

## LANGKAH 22: Sahkan Hasilnya

```bash
git status
git log --oneline --graph
```

**Output dijangka:**

```
*   5c6d7e8 Selesaikan konflik pada baris jabatan
|\
| * 3a4b5c6 Tukar jabatan kepada Teknologi Maklumat
* | 9f8e7d6 Tukar jabatan kepada Digital
|/
* a1b2c3d Isi nama dan jabatan peserta
```

Perhatikan bentuk **bercabang dan bertemu semula**. Itulah gambaran visual sebuah merge. Kedua-dua sejarah kekal — tiada kerja siapa pun yang hilang.

Kemas kini akhir:

```bash
git branch -d tukar-jabatan
```

---

## LANGKAH 23: Butang Keselamatan — `git merge --abort`

Ulang Langkah 14 hingga 16 sekali lagi untuk mencipta konflik baharu. Kali ini, sebaik sahaja konflik muncul:

```bash
git merge --abort
git status
```

Semuanya kembali kepada keadaan sebelum merge, seolah-olah anda tidak pernah menaip `git merge`.

**Gunakan arahan ini apabila:**

- Anda tidak pasti perubahan mana yang betul dan perlu bertanya kepada rakan sepasukan;
- Konflik melibatkan terlalu banyak fail dan anda mahu merancang semula; atau
- Anda tersilap menggabungkan branch yang salah.

---

## KESILAPAN LAZIM

| Kesilapan                                         | Kesan                                      | Cara elak                                     |
| ------------------------------------------------- | ------------------------------------------ | --------------------------------------------- |
| Lupa `git add` sebelum `git commit`               | Tiada apa-apa direkod                      | Sentiasa `git status` sebelum commit          |
| Lupa simpan fail dalam editor                     | `git status` kata tiada perubahan          | Simpan dahulu, kemudian semak                 |
| Tertinggal penanda `<<<<<<<` dalam fail           | Kod rosak, semua ahli pasukan terjejas     | Cari `<<<<` dalam fail sebelum `git add`      |
| Terus `git commit` semasa konflik tanpa `git add` | Git menolak dengan amaran `unmerged paths` | `git add` setiap fail yang telah diselesaikan |
| Padam kerja rakan tanpa bertanya                  | Kerja orang lain hilang                    | Berbincang dahulu jika tidak pasti            |
| Panik dan padam folder `.git`                     | Seluruh sejarah repositori musnah          | Gunakan `git merge --abort` sebaliknya        |

---

## LATIHAN BERPASANGAN (Pilihan)

Jika satu repositori kongsi disediakan oleh fasilitator:

1. Dua peserta menyunting **baris yang sama** dalam `senarai_nama.txt` secara serentak.
2. Peserta A: `git add`, `git commit`, `git push` — berjaya.
3. Peserta B: `git push` — **ditolak** oleh Git.
4. Peserta B: `git pull` — konflik muncul.
5. Peserta B menyelesaikan konflik mengikut Langkah 17 – 21, kemudian `git push` semula.
6. Peserta A: `git pull` — melihat hasil gabungan.

> Peraturan emas: **`git pull` dahulu sebelum mula bekerja setiap hari.** Kebanyakan konflik berpunca daripada bekerja atas versi lama.

---

## RINGKASAN ARAHAN PENUH

### Asas (Bahagian 1)

| Arahan                  | Fungsi                                      |
| ----------------------- | ------------------------------------------- |
| `git init`              | Mula jejak folder ini sebagai repositori    |
| `git status`            | Semak keadaan semasa (guna sekerap mungkin) |
| `git add <fail>`        | Masukkan perubahan ke staging area          |
| `git commit -m "mesej"` | Rekod perubahan secara kekal                |
| `git diff`              | Lihat perubahan yang belum di-`add`         |
| `git diff --staged`     | Lihat perubahan yang sudah di-`add`         |
| `git diff HEAD`         | Lihat semua perubahan sejak commit terakhir |
| `git log --oneline`     | Lihat senarai ringkas sejarah commit        |

### Branch & Konflik (Bahagian 2)

| Arahan                      | Fungsi                                            |
| --------------------------- | ------------------------------------------------- |
| `git branch`                | Senaraikan semua branch                           |
| `git switch -c <nama>`      | Cipta branch baharu dan terus masuk               |
| `git switch <nama>`         | Bertukar ke branch sedia ada                      |
| `git merge <nama>`          | Gabungkan branch tersebut ke branch semasa        |
| `git status`                | Lihat fail mana yang berkonflik (`both modified`) |
| `git add <fail>`            | Tandakan konflik fail tersebut sebagai selesai    |
| `git commit`                | Tamatkan proses merge                             |
| `git merge --abort`         | Batalkan merge, kembali kepada keadaan asal       |
| `git log --oneline --graph` | Lihat gambaran cabang sejarah repositori          |
| `git branch -d <nama>`      | Buang branch yang sudah digabungkan               |

---

## SEMAKAN KEFAHAMAN AKHIR

Jawab tanpa merujuk nota:

1. Apakah perbezaan antara _untracked_, _modified_ dan _both modified_?
2. Selepas `git add`, mengapa `git diff` menjadi kosong?
3. Apakah fungsi `-m` dalam `git commit -m "..."`?
4. Mengapakah merge di Langkah 12 tidak menghasilkan konflik, tetapi merge di Langkah 16 menghasilkannya?
5. Dalam penanda konflik, bahagian mana yang mewakili branch semasa anda?
6. Apakah maksud `git add` semasa proses menyelesaikan konflik?
7. Apakah yang berlaku jika anda commit tanpa membuang penanda `=======`?
8. Apakah arahan untuk membatalkan merge dan kembali kepada keadaan asal?

---
