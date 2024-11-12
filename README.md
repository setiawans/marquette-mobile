# Marquette (mobile version)

Marquette-mobile merupakan proyek Flutter untuk tugas mata kuliah Pemrograman Berbasis Platform Ganjil 2024/2025 oleh Steven Setiawan dengan NPM 2306152260.

## Daftar Isi
- [README.md Tugas 7](#tugas-7)
  - [Implementasi Checklist Tugas 7](#implementasi-checklist-tugas-7)
  - [Apa itu _stateless widget_ dan _stateful widget_?](#jelaskan-apa-yang-dimaksud-dengan-stateless-widget-dan-stateful-widget-dan-jelaskan-perbedaan-dari-keduanya)
  - [Apa saja _widget_ yang digunakan pada proyek ini?](#sebutkan-widget-apa-saja-yang-kamu-gunakan-pada-proyek-ini-dan-jelaskan-fungsinya)
  - [Apa fungsi dari setState()?](#apa-fungsi-dari-setstate-jelaskan-variabel-apa-saja-yang-dapat-terdampak-dengan-fungsi-tersebut)
  - [Apa perbedaan antara const dan final](#jelaskan-perbedaan-antara-const-dengan-final)
- [README.md Tugas 8](#tugas-8)
  - [Apa kegunaan const di Flutter?](#apa-kegunaan-const-di-flutter-jelaskan-apa-keuntungan-ketika-menggunakan-const-pada-kode-flutter-kapan-sebaiknya-kita-menggunakan-const-dan-kapan-sebaiknya-tidak-digunakan)
  - [Jelaskan penggunaan _Column_ dan _Row_ pada Flutter.](#jelaskan-dan-bandingkan-penggunaan-column-dan-row-pada-flutter-berikan-contoh-implementasi-dari-masing-masing-layout-widget-ini)
  - [Sebutkan apa saja elemen input yang digunakan pada halaman _form_.](#sebutkan-apa-saja-elemen-input-yang-kamu-gunakan-pada-halaman-form-yang-kamu-buat-pada-tugas-kali-ini-apakah-terdapat-elemen-input-flutter-lain-yang-tidak-kamu-gunakan-pada-tugas-ini-jelaskan)
  - [Bagaimana cara kamu mengatur tema dalam aplikasi Flutter agar konsisten?](#bagaimana-cara-kamu-mengatur-tema-theme-dalam-aplikasi-flutter-agar-aplikasi-yang-dibuat-konsisten-apakah-kamu-mengimplementasikan-tema-pada-aplikasi-yang-kamu-buat)
  - [Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?](#bagaimana-cara-kamu-menangani-navigasi-dalam-aplikasi-dengan-banyak-halaman-pada-flutter)

## Tugas 7

## Implementasi Checklist Tugas 7

<details>
<summary>Membuat sebuah program Flutter baru</summary>

Untuk membuat sebuah program Flutter baru, saya menjalankan perintah berikut:
```
flutter create marquette_mobile
```

Setelah itu, saya menambahkan berkas baru bernama `menu.dart` untuk menampilkan menu-menu pada halaman utama dan memanfaatkan `main.dart` sebagai layout utama.
Untuk mengecek apakah aplikasi dapat berjalan, saya menjalankan perintah berikut:

```
flutter run -d chrome
```

Hal ini akan membuka sebuah tab Chrome yang berisi aplikasi flutter kita. Namun, sebelum itu jangan lupa menjalankan perintah berikut:

```
flutter config --enable-web
```
</details>

<details>
<summary>Membuat tiga tombol sederhana dengan ikon dan teks</summary>
Untuk membuat tiga tombol sederhana, kita dapat membuat widget ItemHomepage dan ItemCard yang akan berperan menjadi tombol. Berikut adalah potongan kode saya yang mengimplementasikan hal tersebut:

```flutter
class MyHomePage extends StatelessWidget {
  final String npm = '2306152260';
  final String name = 'Steven Setiawan';
  final String className = 'PBP D';

  final List<ItemHomepage> items = [
    ItemHomepage("Lihat Daftar Produk", Icons.shopping_cart, Colors.blue),
    ItemHomepage("Tambah Produk", Icons.add, Colors.green),
    ItemHomepage("Logout", Icons.logout, Colors.red),
  ];
  ...
}

class ItemHomepage {
  final String name;
  final IconData icon;
  final Color color;

  ItemHomepage(this.name, this.icon, this.color);
}

class ItemCard extends StatelessWidget {
  final ItemHomepage item;

  const ItemCard(this.item, {super.key});

  @override
  Widget build(BuildContext context) {
    return Material(
      ...
    )
  }
}
```

Kemudian, pemanggilan komponen ItemHomepage akan dilakukan pada potongan kode berikut:
```flutter
GridView.count(
  primary: true,
  padding: const EdgeInsets.all(20),
  crossAxisSpacing: 10,
  mainAxisSpacing: 10,
  crossAxisCount: 3,
  shrinkWrap: true,

  children: items.map((ItemHomepage item) {
    return ItemCard(item);
  }).toList(),
),
```
</details>

<details>
<summary>Mengimplementasikan warna-warna yang berbeda untuk setiap tombol</summary>

Untuk mengimplementasikan warna yang berbeda pada setiap tombol, ada beberapa potongan kode yang harus kita modifikasi.

```flutter
final List<ItemHomepage> items = [
  ItemHomepage("Lihat Daftar Produk", Icons.shopping_cart, Colors.blue),
  ItemHomepage("Tambah Produk", Icons.add, Colors.green),
  ItemHomepage("Logout", Icons.logout, Colors.red),
];
```

Pada bagian tersebut, kita tambahkan parameter Colors yang nantinya akan dihandle pada bagian berikut:

```flutter
class ItemHomepage {
  final String name;
  final IconData icon;
  final Color color;

  ItemHomepage(this.name, this.icon, this.color);
}
```
</details>

<details>
<summary>Memunculkan Snackbar</summary>
Untuk memunculkan Snackbar ketika tombol ditekan, kita cukup menambahkan kode berikut:

```flutter
class ItemCard extends StatelessWidget {
  final ItemHomepage item;

  const ItemCard(this.item, {super.key});

  @override
  Widget build(BuildContext context) {
    return Material(
      ...
      child: InkWell(
        onTap: () {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        ...
      ),
    );
  }
}
```

Dengan menambahkan `onTap`, setiap kali pengguna menekan tombol, maka aplikasi akan menampilkan Snackbar sesuai tombol yang ditekan.
</details>

## Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya.

**Stateless widget** seperti namanya merupakan widget yang bersifat statis atau tidak akan berubah selama aplikasi berjalan. Biasanya, widget ini digunakan pada bagian-bagian aplikasi yang memang tidak akan berubah atau tidak memerlukan interaksi dari pengguna. Sedangkan, **stateful widget** adalah widget yang bersifat interaktif dan dapat berubah selama aplikasi berjalan. Widget ini memberikan respon terhadap interaksi yang dilakukan oleh pengguna.

Secara umum, perbedaan utamanya terletak pada fleksibilitas kedua widget, di mana `stateless` tidak dapat diubah ketika aplikasi sudah berjalan, sedangkan `stateful` dapat berubah sesuai dengan interaksi bersama pengguna.

## Sebutkan widget apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.
- **MaterialApp**: Root widget yang menyediakan berbagai konfigurasi design untuk aplikasi yang sedang kita buat.
- **Scaffold**: Menyediakan struktur dasar untuk halaman aplikasi.
- **AppBar**: Menyediakan bar di bagian atas aplikasi.
- **Card**: Menampilkan konten dalam bentuk kartu, sehingga konten lebih terstruktur dan rapi.
- **Column**: Menyusun child widget secara vertikal.
- **Row**: Menyusun child widget secara horizontal.
- **Icon**: Menyediakan dan menampilkan ikon grafis.
- **InkWell**: Memberikan efek sentuhan berupa animasi ripple.
- **Padding**: Memberikan jarak di sekitar widget.
- **SnackBar**: Menampilkan pesan singkat di bagian bawah layar.
- **GridView**: Menampilkan item dalam format grid.

## Apa fungsi dari setState()? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.

`setState()` merupakan fungsi yang digunakan untuk memperbarui state dari widget yang kita gunakan. Ketika fungsi ini dipanggil, Flutter akan membangun/merender ulang widget yang dipengaruhi oleh perubahan state ketika aplikasi berjalan, sehingga data yang ditampilkan pada aplikasi merupakan data terbaru.

Penggunaan `setState()` sendiri memengaruhi variabel-variabel yang terdapat dalam `StatefulWidget`, yaitu variabel-variabel yang rentan berubah ketika berinteraksi dengan pengguna. Pada aplikasi ini, kedepannya `setState()` akan digunakan pada beberapa fitur, seperti penambahan barang ataupun perubahan data yang perlu dilakukan secara langsung melalui _front-end_.

## Jelaskan perbedaan antara const dengan final.
Secara umum, perbedaannya dapat dilihat dari fleksibilitas data di dalamnya. `const` digunakan ketika nilai dari variabel kita ketahui saat _compile time_ dan tidak ingin diubah. Dengan demikian, `const` cocok untuk variabel-variabel statis yang tidak berinteraksi dengan pengguna. Sedangkan, `final` digunakan untuk nilai yang diketahui saat _runtime_ berlangsung. Dengan demikian, nilai dari variabel dapat ditentukan saat aplikasi berjalan. `final` sering digunakan untuk nilai statis/tetap yang diperoleh dari input pengguna.

## Tugas 8

## Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?

Dalam flutter, `const` biasanya digunakan untuk mendeklarasikan objek yang nilainya statik atau tidak berubah selama aplikasi berjalan (bersifat immutable). Penggunaan `const` sendiri memiliki keuntungan pada sisi efisiensi sumber dayanya. Dengan menggunakan `const`, objek akan dibuat pada waktu _compile_ dan hanya akan disimpan sekali selama program berjalan. Dengan demikian, sumber daya yang digunakan menjadi lebih sedikit. Namun, `const` memiliki kekurangan, yaitu tidak dapat digunakan untuk widget ataupun objek yang bersifat dinamis atau nilainya berubah sesuai interaksi ketika aplikasi berjalan.

## Jelaskan dan bandingkan penggunaan Column dan Row pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!

Pada Flutter, `Column` dan `Row` merupakan layout widget yang digunakan untuk menyusun elemen secara vertikal (`Column`) dari atas ke bawah dan horizontal (`Row`) dari kiri ke kanan.

- **Column**

  ```flutter
  Column(
    children: [
      const Padding(
        padding: EdgeInsets.only(top: 16.0),
        child: Text(
          'Welcome to Marquette',
          style: TextStyle(
            fontWeight: FontWeight.bold,
            fontSize: 18.0,
          ),
        ),
      ),
      GridView.count(
        primary: true,
        padding: const EdgeInsets.all(20),
        crossAxisSpacing: 10,
        mainAxisSpacing: 10,
        crossAxisCount: 3,
        shrinkWrap: true,
        children: items.map((ItemHomepage item) {
          return ItemCard(item);
        }).toList(),
      ),
    ],
  )
  ```

- **Row**

  ```flutter
  Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
      InfoCard(title: 'NPM', content: npm),
      InfoCard(title: 'Name', content: name),
      InfoCard(title: 'Class', content: className),
    ],
  )
  ```

## Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!

Pada tugas individu ini, saya menggunakan beberapa elemen input, seperti `TextFormField` yang berfungsi untuk input teks, yaitu untuk nama, jumlah, dan deksripsi produk serta `ElevatedButton` sebagai tombol submit untuk menyimpan produk yang telah saya buat.

Selain kedua elemen input tersebut, Flutter masih memiliki beberapa elemen input lainnya, seperti `Checkbox`, `Radio`, dan `Switch`. Elemen-elemen ini tidak saya gunakan pada tugas kali ini karna pengimplementasiannya belum terlalu diperlukan dan masih dapat di-_handle_ menggunakan kedua elemen yang saya sebutkan di awal.

## Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?

Dalam Flutter, kita dapat mengatur tema dengan memanfaatkan `ThemeData` pada `MaterialApp`. Kita dapat mendefinisikan tema global untuk aplikasi yang kita miliki, seperti warna utama, font, latar belakang, dan elemen-elemen lainnya. Secara pribadi, pada tugas ini saya baru mengimplementasikan warna utama dan _secondary_ yang dapat dilihat pada potongan kode berikut:

```flutter
theme: ThemeData(
  colorScheme: ColorScheme.fromSwatch(
    primarySwatch: Colors.deepPurple,
  ).copyWith(secondary: Colors.deepPurple[400]),
  useMaterial3: true,
)
```

## Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?

Pada Flutter, navigasi dapat ditangani dengan memanfaatkan `Navigator`, seperti `Navigator.push` untuk menambahkan halaman/page baru ke stack dan `Navigator.pushReplacement` ketika kita ingin mengganti halaman saat ini dengan halaman baru, sehingga kita dapat menghindari lapisan stack yang terlalu banyak. Dengan memanfaatkan `Navigator` ini, saya dapat membuat navigasi yang lebih efisien dan fleksibel, sehingga `user` yang menggunakan aplikasi ini tidak akan kesulitan saat berpindah halaman. 