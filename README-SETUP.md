# Sistem e-Report KPDN — GitHub + Firebase Hosting

Kod utama berada di `public/index.html`. Repository ini menyediakan deployment automatik ke `https://ereportkpdn.web.app` apabila perubahan dihantar ke branch `main`.

## Sebelum upload ke GitHub

1. Buka `public/index.html`.
2. Cari `PASTE_URL_REALTIME_DATABASE_DI_SINI`.
3. Gantikan dengan URL sebenar Firebase Realtime Database.
4. Pastikan Firebase Authentication → Anonymous telah diaktifkan.

## Cipta repository GitHub

1. Cipta repository Private bernama `sistem-e-report-kpdn`.
2. Buka CMD dalam folder projek ini.
3. Jalankan:

```cmd
git init
git add .
git commit -m "Versi GitHub pertama e-Report KPDN"
git branch -M main
git remote add origin https://github.com/NAMA-ANDA/sistem-e-report-kpdn.git
git push -u origin main
```

## Sambungkan GitHub Actions dengan Firebase

Firebase Hosting Site `ereportkpdn` dan target `ereport` mesti telah diwujudkan:

```cmd
firebase hosting:sites:create ereportkpdn
firebase target:apply hosting ereport ereportkpdn
```

Kemudian jalankan dari folder utama:

```cmd
firebase init hosting:github
```

Jawapan yang disyorkan:

- Repository: `NAMA-ANDA/sistem-e-report-kpdn`
- Build script: `No`
- Automatic live deploy: `Yes`
- Branch live: `main`
- Hosting target/site: `ereport` / `ereportkpdn`

Arahan ini mencipta GitHub Secret bernama lebih kurang `FIREBASE_SERVICE_ACCOUNT_SISTEM_E_REPORT_KPDN`. Workflow yang dibekalkan menggunakan nama secret tersebut. Semak di GitHub → Settings → Secrets and variables → Actions.

Selepas setup, hantar perubahan workflow:

```cmd
git add .
git commit -m "Aktifkan Firebase GitHub Actions"
git push
```

## Proses perubahan selepas ini

### Untuk ujian

```cmd
git checkout -b ujian-interface
```

Ubah `public/index.html`, kemudian:

```cmd
git add .
git commit -m "Ujian interface"
git push -u origin ujian-interface
```

Cipta Pull Request ke `main`. GitHub Actions akan memberikan pautan Firebase Preview. Preview Hosting masih menggunakan Realtime Database sebenar, jadi gunakan data ujian.

### Untuk terbitkan rasmi

Selepas preview disahkan, Merge Pull Request ke `main`. GitHub Actions akan menerbitkan kod ke:

`https://ereportkpdn.web.app`

## Kemas kini mudah tanpa CMD

Gunakan GitHub Desktop:

1. Clone repository.
2. Gantikan `public/index.html`.
3. Commit to branch ujian.
4. Push origin.
5. Cipta Pull Request dan semak pautan preview.
6. Merge selepas lulus.

## Keselamatan

Jangan masukkan App Password, SMTP password, service-account JSON, private key atau token ke GitHub. Repository hendaklah Private. `firebaseConfig` web boleh berada dalam HTML, tetapi Realtime Database tetap mesti dilindungi dengan Authentication dan Security Rules yang sesuai.
