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
- [README.md Tugas 9](#tugas-9)
  - [Implementasi Checklist Tugas 9](#implementasi-checklist-tugas-9)
  - [Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan/pengiriman data JSON?](#jelaskan-mengapa-kita-perlu-membuat-model-untuk-melakukan-pengambilan-ataupun-pengiriman-data-json-apakah-akan-terjadi-error-jika-kita-tidak-membuat-model-terlebih-dahulu)
  - [Jelaskan fungsi dari library http](#jelaskan-fungsi-dari-library-http-yang-sudah-kamu-implementasikan-pada-tugas-ini)
  - [Jelaskan fungsi dari CookieRequest](#jelaskan-fungsi-dari-cookierequest-dan-jelaskan-mengapa-instance-cookierequest-perlu-untuk-dibagikan-ke-semua-komponen-di-aplikasi-flutter)
  - [Jelaskan mekanisme pengiriman data](#jelaskan-mekanisme-pengiriman-data-mulai-dari-input-hingga-dapat-ditampilkan-pada-flutter)
  - [Jelaskan mekanisme autentikasi](#jelaskan-mekanisme-autentikasi-dari-login-register-hingga-logout-mulai-dari-input-data-akun-pada-flutter-ke-django-hingga-selesainya-proses-autentikasi-oleh-django-dan-tampilnya-menu-pada-flutter)

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

## Tugas 9

## Implementasi Checklist Tugas 9
<details>
<summary>Mengimplementasikan fitur registrasi</summary>
Dalam mengimplementasikan fitur registrasi, terlebih dahulu saya menambahkan app bernama authentication pada proyek Django saya. Kemudian, saya melakukan setup routing dan menambahkan potongan kode berikut:

```py
@csrf_exempt
def register(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        username = data['username']
        password1 = data['password1']
        password2 = data['password2']

        if password1 != password2:
            return JsonResponse({
                "status": False,
                "message": "Passwords do not match."
            }, status=400)
        
        if User.objects.filter(username=username).exists():
            return JsonResponse({
                "status": False,
                "message": "Username already exists."
            }, status=400)
        
        user = User.objects.create_user(username=username, password=password1)
        user.save()
        
        return JsonResponse({
            "username": user.username,
            "status": 'success',
            "message": "User created successfully!"
        }, status=200)
    
    else:
        return JsonResponse({
            "status": False,
            "message": "Invalid request method."
        }, status=400)
```

Selanjutnya, saya membuat berkas register.dart dengan isi berikut:

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:marquette/screens/login.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

class RegisterPage extends StatefulWidget {
  const RegisterPage({super.key});

  @override
  State<RegisterPage> createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  final _confirmPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: <Widget>[
                  const Text(
                    'Register',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your username';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _confirmPasswordController,
                    decoration: const InputDecoration(
                      labelText: 'Confirm Password',
                      hintText: 'Confirm your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please confirm your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password1 = _passwordController.text;
                      String password2 = _confirmPasswordController.text;

                      final response = await request.postJson(
                          "http://127.0.0.1:8000/auth/register/",
                          jsonEncode({
                            "username": username,
                            "password1": password1,
                            "password2": password2,
                          }));
                      if (context.mounted) {
                        if (response['status'] == 'success') {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Successfully registered!'),
                            ),
                          );
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const LoginPage()),
                          );
                        } else {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Failed to register!'),
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Register'),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
</details>

<details>
<summary>Membuat halaman login</summary>
Pada app authentication di Django sebelumnya, kita tambahkan potongan kode berikut:

```py
@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login sukses!"
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, akun dinonaktifkan."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login gagal, periksa kembali email atau kata sandi."
        }, status=401)
```

Lalu, tambahkan berkas login.dart dengan isi berikut:

```dart
import 'package:marquette/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:marquette/screens/register.dart';

void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.deepPurple,
        ).copyWith(secondary: Colors.deepPurple[400]),
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: [
                  const Text(
                    'Login',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                  ),
                  const SizedBox(height: 12.0),
                  TextField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password = _passwordController.text;
                      
                      final response = await request
                          .login("http://127.0.0.1:8000/auth/login/", {
                        'username': username,
                        'password': password,
                      });

                      if (request.loggedIn) {
                        String message = response['message'];
                        String uname = response['username'];
                        if (context.mounted) {
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => MyHomePage()),
                          );
                          ScaffoldMessenger.of(context)
                            ..hideCurrentSnackBar()
                            ..showSnackBar(
                              SnackBar(
                                  content:
                                      Text("$message Selamat datang, $uname.")),
                            );
                        }
                      } else {
                        if (context.mounted) {
                          showDialog(
                            context: context,
                            builder: (context) => AlertDialog(
                              title: const Text('Login Gagal'),
                              content: Text(response['message']),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Login'),
                  ),
                  const SizedBox(height: 36.0),
                  GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const RegisterPage()),
                      );
                    },
                    child: Text(
                      'Don\'t have an account? Register',
                      style: TextStyle(
                        color: Theme.of(context).colorScheme.primary,
                        fontSize: 16.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
</details>

<details>
<summary>Mengintegrasikan sistem autentikasi</summary>

Untuk mengintegrasikan sistem autentikasi, secara umum kita melakukan hal-hal berikut:

- Membuat view registrasi, login, dan logout pada Django
- Memanggil endpoint dari masing-masing view melalui request pada Flutter
- Melakukan pemroresan data dengan memanfaatkan JSON

</details>

<details>
<summary>Membuat model kustom</summary>
Untuk membuat model kustom, kita dapat melakukan langkah-langkah berikut:

- Mengambil konten dari endpoint /json pada localhost
- Melakukan generate model dengan memanfaatkan website Quicktype
- Membuat berkas baru bernama product_entry.dart pada subdirektori lib/models/

Berikut adalah isi dari product_entry.dart:

```dart
import 'dart:convert';

List<ProductEntry> productEntryFromJson(String str) => List<ProductEntry>.from(json.decode(str).map((x) => ProductEntry.fromJson(x)));

String productEntryToJson(List<ProductEntry> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class ProductEntry {
    String model;
    String pk;
    Fields fields;

    ProductEntry({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory ProductEntry.fromJson(Map<String, dynamic> json) => ProductEntry(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String name;
    int price;
    String description;

    Fields({
        required this.user,
        required this.name,
        required this.price,
        required this.description,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        price: json["price"],
        description: json["description"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "price": price,
        "description": description,
    };
}
```
</details>

<details>
<summary>Membuat halaman yang berisi  daftar semua item</summary>
Untuk melakukan hal ini, kita tambahkan sebuah berkas baru bernama list_productentry.dart yang akan melakukan fetch pada seluruh data dari endpoint JSON yang kita miliki. Berikut adalah isinya:

```dart
import 'package:flutter/material.dart';
import 'package:marquette/models/product_entry.dart';
import 'package:marquette/widgets/left_drawer.dart';
import 'package:provider/provider.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:marquette/screens/product_detail.dart'; 

class ProductEntryPage extends StatefulWidget {
  const ProductEntryPage({super.key});

  @override
  State<ProductEntryPage> createState() => _ProductEntryPageState();
}

class _ProductEntryPageState extends State<ProductEntryPage> {
  Future<List<ProductEntry>> fetchProduct(CookieRequest request) async {
    final response = await request.get('http://127.0.0.1:8000/json/');
    
    var data = response;
    List<ProductEntry> listProduct = [];
    for (var d in data) {
      if (d != null) {
        listProduct.add(ProductEntry.fromJson(d));
      }
    }
    return listProduct;
  }

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Product Entry List'),
      ),
      drawer: const LeftDrawer(),
      body: FutureBuilder(
        future: fetchProduct(request),
        builder: (context, AsyncSnapshot snapshot) {
          if (snapshot.data == null) {
            return const Center(child: CircularProgressIndicator());
          } else {
            if (!snapshot.hasData) {
              return const Column(
                children: [
                  Text(
                    'Belum ada data Product pada Marquette.',
                    style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                  ),
                  SizedBox(height: 8),
                ],
              );
            } else {
              return ListView.builder(
                itemCount: snapshot.data!.length,
                itemBuilder: (_, index) => Card(
                  margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                  child: InkWell(
                    onTap: () {
                      // Navigate to product detail page when tapped
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ProductDetailPage(
                            product: snapshot.data![index],
                          ),
                        ),
                      );
                    },
                    child: Padding(
                      padding: const EdgeInsets.all(20.0),
                      child: Column(
                        mainAxisAlignment: MainAxisAlignment.start,
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            snapshot.data![index].fields.name,
                            style: const TextStyle(
                              fontSize: 18.0,
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          const SizedBox(height: 10),
                          Text("Price: Rp${snapshot.data![index].fields.price}"),
                          const SizedBox(height: 10),
                          Text(
                            snapshot.data![index].fields.description,
                            maxLines: 2,
                            overflow: TextOverflow.ellipsis,
                          ),
                        ],
                      ),
                    ),
                  ),
                ),
              );
            }
          }
        },
      ),
    );
  }
}
```
</details>

<details>
<summary>Membuat halaman detail untuk setiap item</summary>
Untuk membuat halaman detail, pertama-tama saya membuat sebuah berkas baru bernama product_detail.dart dengan isi berikut:

```dart
import 'package:flutter/material.dart';
import 'package:marquette/models/product_entry.dart';

class ProductDetailPage extends StatelessWidget {
  final ProductEntry product;

  const ProductDetailPage({super.key, required this.product});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Product Detail',
          style: TextStyle(color: Colors.black),
        ),
        elevation: 0,
        leading: IconButton(
          icon: Icon(Icons.arrow_back, color: Colors.black),
          onPressed: () => Navigator.pop(context),
        ),
      ),
      body: SingleChildScrollView(
        child: SafeArea(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Container(
                width: double.infinity,
                padding: const EdgeInsets.all(20),
                child: Card(
                  elevation: 4,
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(15),
                  ),
                  child: Padding(
                    padding: const EdgeInsets.all(20),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        Text(
                          product.fields.name,
                          style: const TextStyle(
                            fontSize: 28,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                        const SizedBox(height: 20),
                        _buildInfoSection(
                          'Price',
                          'Rp${product.fields.price.toString()}',
                          Icons.attach_money,
                        ),
                        const Divider(height: 30),
                        _buildInfoSection(
                          'Description',
                          product.fields.description,
                          Icons.description,
                        ),
                        const Divider(height: 30),
                        _buildInfoSection(
                          'Product ID',
                          product.pk,
                          Icons.qr_code,
                        ),
                      ],
                    ),
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  Widget _buildInfoSection(String title, String content, IconData icon) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Row(
          children: [
            Icon(icon, size: 20, color: Colors.indigo),
            const SizedBox(width: 8),
            Text(
              title,
              style: const TextStyle(
                fontSize: 16,
                color: Colors.grey,
                fontWeight: FontWeight.w500,
              ),
            ),
          ],
        ),
        const SizedBox(height: 8),
        Container(
          width: double.infinity,
          padding: const EdgeInsets.all(12),
          decoration: BoxDecoration(
            color: Colors.grey.shade50,
            borderRadius: BorderRadius.circular(8),
            border: Border.all(color: Colors.grey.shade200),
          ),
          child: Text(
            content,
            style: const TextStyle(
              fontSize: 18,
              color: Colors.black87,
            ),
          ),
        ),
      ],
    );
  }
}
```

Setelah itu, saya menyambungkannya dengan list_productentry.dart dengan potongan kode berikut:

```dart
child: InkWell(
  onTap: () {              
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => ProductDetailPage(
          product: snapshot.data![index],
        ),
      ),
    );
  },
  ...
)
```
</details>

<details>
<summary>Melakukan filter item berdasarkan pengguna yang login</summary>
Filtering item berdasarkan pengguna yang login ini sudah dihandle pada Back-end Django, yaitu melalui potongan kode berikut:

```py
def show_json(request) :
    data = Product.objects.filter(user=request.user) # Disini
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```
</details>

## Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?

Kita memerlukan model dalam pengambilan/pengiriman data JSON karena beberapa alasan, salah satunya adalah validasi data. Dengan menggunakan model dalam proses pengambilan/pengiriman data JSON, kita memastikan data yang diproses sesuai dengan format yang diinginkan. Sehingga, kita dapat mencegah terjadinya crash pada aplikasi karena tipe data yang tidak sesuai. Selain itu, dengan menggunakan model, kode yang kita tulis menjadi lebih mudah untuk di-_maintain_ serta meningkatkan _code reusability_.

Walaupun kita tidak menggunakan model, aplikasi tetap dapat berjalan dan tidak mendapatkan error. Tapi, akan ada berbagai macam hambatan dalam melakukan pemroresan data, seperti keharusan melakukan _processing_ data JSON secara manual, kesulitan pemeliharaan aplikasi, serta rawannya kesalahan dalam konversi tipe data.

## Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini

Pada tugas ini, library HTTP digunakan untuk mempermudah kita melakukan HTTP Request serta pengambilan data dari endpoint API Django yang kita miliki. HTTP Request ini sendiri mencakup operasi-operasi seperti GET, POST, dan DELETE.

## Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

CookieRequest merupakan bagian dari package pbp_django_auth yang berperan untuk hal-hal berikut:

- **Mengelola autentikasi**: CookieRequest akan menyimpan sesi login pengguna melalui sebuah cookie

- **Managemen Session**: Dengan adanya CoookieRequest, server dapat dengan mudah membedakan pengguna yang sedang menggunakan aplikasi tersebut.

- **HTTP Request**: CookieRequest secara otomatis menambahkan cookie pada setiap request HTTP yang dilakukannya, sehingga kita tidak perlu menambahkan cookie secara manual.

Instance CookieRequest perlu dibagikan ke seluruh komponen aplikasi Flutter karena beberapa alasan, salah satunya dapat dilihat dari segi konsistensi. Dengan menambahkan CookieRequest pada semua komponen, maka kita dapat memastikan bahwa untuk setiap sesi di mana aplikasi berjalan, data yang ditampilkan sesuai dengan sesi yang sedang berlangsung. Selain itu, dengan menggunakan instance CookieRequest yang sama, maka pengguna tidak perlu melakukan login berulang kali ketika berpindah halaman.

## Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.

- **User Melakukan Input Data**: User melakukan input data pada aplikasi melalui widget-widget pada Flutter, seperti TextField yang ada pada halaman form.

- **Mengirim Request ke Server**: Selanjutnya, data yang sudah diinput oleh user akan dikirim melalui HTTP Request dengan memanfaatkan package `http` ataupun `CookieRequest` ke backend.

- **Pemroresan di Backend**: Data yang dikirim akan diterima oleh server Django dan kemudian diproses sesuai views yang sesuai. Data ini kemudian  divalidasi dan disimpan ke database (jika diperlukan), dan kemudian mengembalikan respons ke Flutter (biasanya dalam format JSON).

- **Menerima Response**: Respons dari backend akan diterima oleh Flutter.

- **Decoding dan Menampilkan Data**: Data yang diterima oleh Flutter tersebut kemudian akan diolah dengan memanfaatkan models yang ada, lalu ditampilkan ke pengguna pada front-end.

## Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
- **Proses Login**
  1. User akan memasukkan username dan password pada laman login di Flutter.
  2. Ketika button login diklik, maka data akan dikirim melalui HTTP Request dengan method POST ke endpoint /auth/login Django dengan memanfaatkan CookieRequest.
  3. Setelah data diterima pada backend, Django akan memverifikasi username dan password tersebut lalu mengembalikan respons yang sesuai dengan hasil verifikasi.
  4. Apabila login berhasil, maka CookieRequest akan menyimpan cookie dari sesi tersebut, lalu Flutter akan mengarahkan pengguna ke halaman utama.

- **Proses Register**
  1. User akan memasukkan data-data yang diperlukan untuk proses registrasi, yaitu username, password, dan konfirmasi password pada Flutter.
  2. Ketika button register diklik, maka data akan dikirimkan melalui HTTP Request dengan method POST ke endpoint /auth/register Django.
  3. Setelah data diterima oleh backend, Django akan melakukan validasi data. Jika valid, maka user baru akan dibuat. Jika tidak valid, maka Django akan mengembalikan error messages.
  4. Flutter akan menampilkan pesan sukses atau error berdasarkan respons yang dikembalikan oleh backend, lalu mengarahkan pengguna ke halaman login.

- **Proses Logout**
  1. Ketika button logout diklik, maka Flutter akan mengirim request ke endpoint /auth/logout Django dengan menggunakan CookieRequest.
  2. Pada backend, Django akan melakukan penghapusan _session_ dari pengguna.
  3. Setelah _session_ dihapus, maka Flutter akan mengarahkan user kembali ke halaman login.