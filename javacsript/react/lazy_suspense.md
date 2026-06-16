# React `lazy` dan `Suspense`

Salah satu teknik optimasi performa terbaik pada React adalah **Code-Splitting**. Secara default, seluruh aplikasi React Anda dibundel menjadi satu file JavaScript yang besar. Jika aplikasi semakin besar, file bundle ini juga membesar dan membuat waktu *loading* awal (Initial Load) menjadi lambat.

`React.lazy` dan `React.Suspense` digunakan bersamaan untuk melakukan *code-splitting* di level komponen secara mudah.

---

## 1. `React.lazy`

`React.lazy` memungkinkan Anda untuk me-render komponen yang di-import secara dinamis (*dynamic import*) seolah-olah komponen tersebut di-import secara biasa. 

Dengan menggunakan `lazy()`, browser hanya akan mengunduh file komponen tersebut saat komponen itu benar-benar dibutuhkan (misalnya saat pengguna mengklik tombol atau pindah ke rute tertentu).

### Cara Menggunakan `lazy`

**Sebelum:** Import statis (File komponen langsung dimasukkan ke bundle utama)
```jsx
import MyBigComponent from './MyBigComponent';
```

**Sesudah:** Import dinamis (File komponen dipisah dan di-load belakangan)
```jsx
import { lazy } from 'react';

const MyBigComponent = lazy(() => import('./MyBigComponent'));
```

> **Catatan:** Komponen yang di-import menggunakan `React.lazy` harus diekspor secara default (`export default`).

---

## 2. `React.Suspense`

Ketika Anda menggunakan `lazy()`, dibutuhkan sedikit waktu bagi browser untuk mengunduh kode komponen melalui jaringan. Selama proses pengunduhan ini terjadi, React membutuhkan tempat untuk menampilkan indikator *loading* sementara.

Di sinilah peran `Suspense`. Komponen `Suspense` memungkinkan kita menentukan UI *fallback* (seperti animasi spinner, teks "Loading", atau skeleton) yang akan ditampilkan kepada pengguna saat komponen sedang dimuat.

### Contoh Implementasi Lengkap

```jsx
import React, { lazy, Suspense } from 'react';

// 1. Definisikan komponen lazy
const Dashboard = lazy(() => import('./Dashboard'));

function App() {
  return (
    <div>
      <h1>Aplikasi Saya</h1>
      
      {/* 2. Bungkus komponen lazy dengan Suspense */}
      <Suspense fallback={<div>Memuat Dashboard... </div>}>
        <Dashboard />
      </Suspense>
      
    </div>
  );
}

export default App;
```

### Suspense dapat membungkus banyak komponen
Anda tidak perlu membuat satu `Suspense` untuk setiap komponen `lazy`. Anda bisa membungkus beberapa komponen *lazy* sekaligus dengan satu buah `Suspense`.

```jsx
<Suspense fallback={<h2>Sedang Memuat...</h2>}>
  <Navbar /> {/* lazy component */}
  <MainContent /> {/* lazy component */}
  <Footer /> {/* lazy component */}
</Suspense>
```

---

## Kapan Sebaiknya Menggunakan `lazy` & `Suspense`?

1.  **Route-Based Code Splitting:** Menggunakan `lazy` dan `Suspense` pada tingkat Router (misalnya dengan React Router) adalah praktik yang sangat direkomendasikan. Unduh komponen halaman hanya saat pengguna menavigasi ke URL tersebut.
2.  **Komponen yang Berat:** Jika ada komponen yang ukurannya sangat besar (seperti text editor, chart library 3D, peta) yang tidak selalu langsung dilihat pengguna.
3.  **UI Tersembunyi:** Modals, Dialogs, atau *Tabs* yang baru muncul setelah ada interaksi (klik).
