# Panduan Lengkap Metode Array pada JavaScript

Berikut adalah catatan lengkap mengenai metode-metode (functions) bawaan yang dapat digunakan pada tipe data Array di JavaScript beserta kegunaannya. Metode-metode ini dibagi ke dalam beberapa kategori untuk memudahkan pemahaman.

---

## 1. Menambah dan Menghapus Elemen (Mutating)
Metode ini **mengubah** array aslinya secara langsung.

*   **`push(...items)`**: Menambahkan satu atau lebih elemen ke **akhir** array. Mengembalikan panjang array yang baru.
*   **`pop()`**: Menghapus elemen **terakhir** dari array. Mengembalikan elemen yang dihapus.
*   **`unshift(...items)`**: Menambahkan satu atau lebih elemen ke **awal** array. Mengembalikan panjang array yang baru.
*   **`shift()`**: Menghapus elemen **pertama** dari array. Mengembalikan elemen yang dihapus.
*   **`splice(start, deleteCount, ...items)`**: Menambah, menghapus, atau mengganti elemen array mulai dari indeks `start`. Mengembalikan array berisi elemen yang dihapus.

## 2. Menggabungkan dan Memotong Array (Non-Mutating)
Metode ini **tidak mengubah** array aslinya, melainkan menghasilkan array baru.

*   **`concat(...arrays)`**: Menggabungkan dua atau lebih array (atau nilai lain) menjadi satu array baru.
*   **`slice(start, end)`**: Menyalin sebagian elemen array (dari indeks `start` sampai sebelum `end`) dan mengembalikannya sebagai array baru.

## 3. Pencarian dan Pengecekan (Searching & Checking)

*   **`indexOf(searchElement, fromIndex)`**: Mencari elemen tertentu dan mengembalikan indeks **pertama** elemen tersebut ditemukan. Jika tidak ada, mengembalikan `-1`.
*   **`lastIndexOf(searchElement, fromIndex)`**: Mencari elemen dari belakang dan mengembalikan indeks **terakhir** elemen tersebut ditemukan.
*   **`includes(searchElement, fromIndex)`**: Mengecek apakah array memiliki elemen tertentu. Mengembalikan `true` atau `false`.
*   **`find(callbackFn)`**: Mengembalikan **nilai elemen pertama** yang memenuhi kondisi di dalam fungsi callback. Jika tidak ada, mengembalikan `undefined`.
*   **`findIndex(callbackFn)`**: Mengembalikan **indeks dari elemen pertama** yang memenuhi kondisi di dalam fungsi callback. Jika tidak ada, mengembalikan `-1`.
*   **`findLast(callbackFn)`**: Sama seperti `find()`, tetapi mencari dari elemen terakhir ke elemen pertama.
*   **`findLastIndex(callbackFn)`**: Sama seperti `findIndex()`, tetapi mencari dari elemen terakhir ke elemen pertama.

## 4. Iterasi dan Transformasi (Looping)

*   **`forEach(callbackFn)`**: Menjalankan fungsi callback untuk setiap elemen di dalam array. Tidak mengembalikan nilai baru (`undefined`).
*   **`map(callbackFn)`**: Membuat **array baru** yang berisi hasil dari pemanggilan fungsi callback pada setiap elemen array.
*   **`filter(callbackFn)`**: Membuat **array baru** yang berisi elemen-elemen yang lulus pengujian/kondisi dari fungsi callback.
*   **`reduce(callbackFn, initialValue)`**: Mengeksekusi fungsi reducer pada setiap elemen array untuk menghasilkan satu nilai akumulasi (dari kiri ke kanan).
*   **`reduceRight(callbackFn, initialValue)`**: Sama seperti `reduce()`, namun iterasi dilakukan dari kanan ke kiri (dari akhir ke awal).
*   **`some(callbackFn)`**: Mengecek apakah **setidaknya satu** elemen dalam array memenuhi kondisi pada callback. Mengembalikan boolean (`true/false`).
*   **`every(callbackFn)`**: Mengecek apakah **semua** elemen dalam array memenuhi kondisi pada callback. Mengembalikan boolean (`true/false`).

## 5. Pengurutan (Sorting)

*   **`sort(compareFn)`**: Mengurutkan elemen array secara *in-place* (mengubah array asli) dan mengembalikan array yang sudah diurutkan. Secara default diurutkan berdasarkan string abjad.
*   **`reverse()`**: Membalikkan urutan elemen dalam array secara *in-place* (mengubah array asli).
*   **`toSorted(compareFn)`**: (*Modern*) Mengembalikan array baru yang diurutkan tanpa mengubah array aslinya.
*   **`toReversed()`**: (*Modern*) Mengembalikan array baru yang dibalik urutannya tanpa mengubah array aslinya.

## 6. Manipulasi Lainnya

*   **`join(separator)`**: Menggabungkan seluruh elemen array menjadi sebuah string, yang dipisahkan oleh karakter `separator` (default koma `,`).
*   **`fill(value, start, end)`**: Mengisi (me-replace) elemen array dengan nilai `value` statis dari indeks `start` sampai sebelum `end`. Mengubah array aslinya.
*   **`copyWithin(target, start, end)`**: Menyalin sebagian elemen array ke lokasi lain di dalam array yang sama, tanpa mengubah panjang aslinya. Mengubah array aslinya.
*   **`flat(depth)`**: Meratakan array multidimensi (array di dalam array) ke dalam satu dimensi array baru. `depth` menentukan kedalaman array yang akan diratakan.
*   **`flatMap(callbackFn)`**: Gabungan dari `map()` kemudian diikuti oleh `flat()` dengan kedalaman 1.
*   **`with(index, value)`**: (*Modern*) Mengembalikan array baru di mana elemen pada `index` tertentu diganti dengan `value`. Ini adalah versi non-mutating dari `array[index] = value`.
