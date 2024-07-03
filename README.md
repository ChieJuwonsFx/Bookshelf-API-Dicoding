# Bookshelf-API

## Kriteria 1 : API dapat menyimpan buku <br><hr>
Projek ini adalah submission dari Dicoding untuk kelas Belajar Membuat Aplikasi Back-End untuk Pemulayang harus diselesaikan untuk mendapatkan sertifikat. <br>

API yang Anda buat harus dapat menyimpan buku melalui route:

Method : POST <br>
URL : /books <br>
Body Request:

```json
{
    "name": string,
    "year": number,
    "author": string,
    "summary": string,
    "publisher": string,
    "pageCount": number,
    "readPage": number,
    "reading": boolean
}
```

Objek buku yang disimpan pada server harus memiliki struktur seperti contoh di bawah ini:

```json
{
    "id": "Qbax5Oy7L8WKf74l",
    "name": "Buku A",
    "year": 2010,
    "author": "John Doe",
    "summary": "Lorem ipsum dolor sit amet",
    "publisher": "Dicoding Indonesia",
    "pageCount": 100,
    "readPage": 25,
    "finished": false,
    "reading": false,
    "insertedAt": "2021-03-04T09:11:44.598Z",
    "updatedAt": "2021-03-04T09:11:44.598Z"
}
```
Properti yang ditebalkan diolah dan didapatkan di sisi server. Berikut penjelasannya:

- id : nilai id haruslah unik. Untuk membuat nilai unik, Anda bisa memanfaatkan nanoid. <br>
- finished : merupakan properti boolean yang menjelaskan apakah buku telah selesai dibaca atau belum. Nilai finished didapatkan dari observasi pageCount === readPage.<br>
- insertedAt : merupakan properti yang menampung tanggal dimasukkannya buku. Anda bisa gunakan new Date().toISOString() untuk menghasilkan nilainya.<br>
- updatedAt : merupakan properti yang menampung tanggal diperbarui buku. Ketika buku baru dimasukkan, berikan nilai properti ini sama dengan insertedAt.<br>

Server harus merespons gagal bila:

- Client tidak melampirkan properti name pada request body. Bila hal ini terjadi, maka server akan merespons dengan: <br>
Status Code : 400 <br>
Response Body:

```json
{
    "status": "fail",
    "message": "Gagal menambahkan buku. Mohon isi nama buku"
}
```

- Client melampirkan nilai properti readPage yang lebih besar dari nilai properti pageCount. Bila hal ini terjadi, maka server akan merespons dengan: <br>
Status Code : 400 <br>
Response Body:

```json
{
    "status": "fail",
    "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
}
```
- Server gagal memasukkan buku karena alasan umum (generic error). Bila hal ini terjadi, maka server akan merespons dengan: <br>
Status Code : 500 <br>
Response Body:

```json
{
    "status": "error",
    "message": "Buku gagal ditambahkan"
}
```
- Bila buku berhasil dimasukkan, server harus mengembalikan respons dengan: <br>
Status Code : 201 <br>
Response Body:

```json
{
    "status": "success",
    "message": "Buku berhasil ditambahkan",
    "data": {
        "bookId": "1L7ZtDUFeGs7VlEt"
    }
}
```

## Kriteria 2 : API dapat menampilkan seluruh buku <br><hr>
API yang Anda buat harus dapat menampilkan seluruh buku yang disimpan melalui route:<br>
Method : GET<br>
URL: /books

- Server harus mengembalikan respons dengan:<br>
Status Code : 200<br>
Response Body:

```json
{
    "status": "success",
    "data": {
        "books": [
            {
                "id": "Qbax5Oy7L8WKf74l",
                "name": "Buku A",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "1L7ZtDUFeGs7VlEt",
                "name": "Buku B",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "K8DZbfI-t3LrY7lD",
                "name": "Buku C",
                "publisher": "Dicoding Indonesia"
            }
        ]
    }
}
```
- Jika belum terdapat buku yang dimasukkan, server bisa merespons dengan array books kosong.

```json
{
    "status": "success",
    "data": {
        "books": []
    }
}
```


## Kriteria 3 : API dapat menampilkan detail buku <br><hr>
API yang Anda buat harus dapat menampilkan seluruh buku yang disimpan melalui route: <br>
Method : GET<br>
URL: /books/{bookId}

- Bila buku dengan id yang dilampirkan oleh client tidak ditemukan, maka server harus mengembalikan respons dengan:<br>
Status Code : 404<br>
Response Body:

```json
{
    "status": "fail",
    "message": "Buku tidak ditemukan"
}
```
- Bila buku dengan id yang dilampirkan ditemukan, maka server harus mengembalikan respons dengan: <br>
Status Code : 200 <br>
Response Body:

```json
{
    "status": "success",
    "data": {
        "book": {
            "id": "aWZBUW3JN_VBE-9I",
            "name": "Buku A Revisi",
            "year": 2011,
            "author": "Jane Doe",
            "summary": "Lorem Dolor sit Amet",
            "publisher": "Dicoding",
            "pageCount": 200,
            "readPage": 26,
            "finished": false,
            "reading": false,
            "insertedAt": "2021-03-05T06:14:28.930Z",
            "updatedAt": "2021-03-05T06:14:30.718Z"
        }
    }
}
```

## Kriteria 4 : API dapat mengubah data buku <br><hr>
API yang Anda buat harus dapat mengubah data buku berdasarkan id melalui route: <br>
Method : PUT<br>
URL : /books/{bookId}<br>
Body Request:

```json
{
    "name": string,
    "year": number,
    "author": string,
    "summary": string,
    "publisher": string,
    "pageCount": number,
    "readPage": number,
    "reading": boolean
}
```
Server harus merespons gagal bila:

- Client tidak melampirkan properti name pada request body. Bila hal ini terjadi, maka server akan merespons dengan:<br>
Status Code : 400<br>
Response Body:<br>

```json
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Mohon isi nama buku"
}
```
- Client melampirkan nilai properti readPage yang lebih besar dari nilai properti pageCount. Bila hal ini terjadi, maka server akan merespons dengan:<br>
Status Code : 400<br>
Response Body:

```json
{
    "status": "fail",
    "message": "Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount"
}
```
- Id yang dilampirkan oleh client tidak ditemukkan oleh server. Bila hal ini terjadi, maka server akan merespons dengan:<br>
Status Code : 404<br>
Response Body:

```json
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Id tidak ditemukan"
}
```
- Bila buku berhasil diperbarui, server harus mengembalikan respons dengan:<br>
Status Code : 200<br>
Response Body:

```json
{
    "status": "success",
    "message": "Buku berhasil diperbarui"
}
```

## Kriteria 5 : API dapat menghapus buku<br><hr>
API yang Anda buat harus dapat menghapus buku berdasarkan id melalui route berikut:<br>
Method : DELETE<br>
URL: /books/{bookId}<br>

- Bila id yang dilampirkan tidak dimiliki oleh buku manapun, maka server harus mengembalikan respons berikut:<br>
Status Code : 404<br>
Response Body:

```json
{
    "status": "fail",
    "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```
- Bila id dimiliki oleh salah satu buku, maka buku tersebut harus dihapus dan server mengembalikan respons berikut: <br>
Status Code : 200 <br>
Response Body:
```json
{
    "status": "success",
    "message": "Buku berhasil dihapus"
}
```

Ketika membangun Bookshelf API, tentu Anda perlu menguji untuk memastikan API berjalan sesuai dengan kriteria yang ada. Kami sudah menyediakan berkas Postman Collection dan Environment yang dapat Anda gunakan untuk pengujian. <br>

- Berkas submission yang dikirim merupakan folder proyek dari Bookshelf API dalam bentuk ZIP. <br>
- Pastikan di dalam folder proyek yang Anda kirim terdapat berkas package.json. <br>
- Pastikan Anda hapus dulu berkas node_modules pada folder proyek sebelum mengkompresi dalam bentuk ZIP. <br>