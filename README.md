# PBB2---Widget-State

// Import library utama Flutter untuk membuat UI
```dart
import 'package:flutter/material.dart';

// Fungsi utama aplikasi Flutter
// Program dimulai dari sini
void main() {
  runApp(const MyApp()); // Menjalankan widget MyApp sebagai root aplikasi
}

// Widget utama aplikasi
// StatelessWidget berarti tampilannya tidak memiliki state yang berubah
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Judul aplikasi
      title: 'Flutter Demo',

      // Tema aplikasi menggunakan Material Design
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),

      // Halaman pertama yang ditampilkan
      home: const RowColumnPage(),
    );
  }
}

// Halaman utama aplikasi
// Menggunakan StatelessWidget karena tidak ada state yang berubah
class RowColumnPage extends StatelessWidget {
  const RowColumnPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {

    // MediaQuery digunakan untuk mendapatkan ukuran layar perangkat
    MediaQueryData mediaQueryData = MediaQuery.of(context);
    double screenWidth = mediaQueryData.size.width;
    double screenHeight = mediaQueryData.size.height;

    return Scaffold(

      // AppBar adalah bagian header di atas aplikasi
      appBar: AppBar(
        title: const Text(
          'My First App',
          style: TextStyle(color: Colors.black),
        ),
        backgroundColor: Colors.orange[200],
        centerTitle: true,
      ),

      // Body utama aplikasi
      body: Column(

        // Mengatur posisi widget secara horizontal
        crossAxisAlignment: CrossAxisAlignment.center,

        // Mengatur posisi widget secara vertikal
        mainAxisAlignment: MainAxisAlignment.center,

        children: <Widget>[

          // Container pertama berisi gambar
          Container(
            child: AspectRatio(

              // Menjaga rasio gambar tetap 1:1
              aspectRatio: 1.0,

              child: Container(
                width: MediaQuery.of(context).size.width,
                margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 10.0),
                padding: EdgeInsets.all(20.0),
                color: Colors.lightBlue[100],

                // Menempatkan gambar di tengah
                child: Center(
                  child: Image.network(

                    // Mengambil gambar random dari internet
                    'https://picsum.photos/200',

                    fit: BoxFit.cover,
                    width: 500,
                  ),
                ),
              ),
            ),
          ),

          // Container kedua berisi teks
          Container(
            width: MediaQuery.of(context).size.width,
            margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 10.0),
            padding: EdgeInsets.all(20.0),
            color: Colors.pink[200],

            // Teks deskripsi
            child: Text(
              'What image is that',
              style: TextStyle(fontSize: 16),
            ),
          ),

          // Container ketiga berisi pilihan kategori
          Container(
            width: MediaQuery.of(context).size.width,
            color: Colors.yellow[200],
            padding: EdgeInsets.all(20.0),
            margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),

            // Row digunakan untuk menampilkan widget secara horizontal
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              crossAxisAlignment: CrossAxisAlignment.start,
              children: <Widget>[

                // Column pertama
                Column(
                  children: [
                    Icon(Icons.food_bank),
                    Text("Food")
                  ],
                ),

                // Column kedua
                Column(
                  children: [
                    Icon(Icons.landscape),
                    Text("Scenery")
                  ],
                ),

                // Column ketiga
                Column(
                  children: [
                    Icon(Icons.people),
                    Text("People")
                  ],
                ),
              ],
            ),
          ),

          // Widget counter yang memiliki state
          CounterCard(),
        ],
      ),
    );
  }
}

// Widget CounterCard menggunakan StatefulWidget
// StatefulWidget digunakan jika ada data yang berubah (state)
class CounterCard extends StatefulWidget {
  const CounterCard({super.key});

  @override
  State<CounterCard> createState() => _CounterCardState();
}

// State dari CounterCard
class _CounterCardState extends State<CounterCard> {

  // Variabel state untuk menyimpan nilai counter
  int _counter = 0;

  // Fungsi untuk menambah nilai counter
  void _incrementCounter() {
    setState(() {

      // setState memberi tahu Flutter bahwa UI harus diperbarui
      _counter++;

    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),
      padding: EdgeInsets.all(20.0),
      width: MediaQuery.of(context).size.width,
      color: Colors.cyan[100],

      child: Row(

        // Mengatur posisi elemen kiri dan kanan
        mainAxisAlignment: MainAxisAlignment.spaceBetween,

        children: [

          // Menampilkan nilai counter
          Text(
            "Counter here: $_counter",
            style: TextStyle(fontSize: 16),
          ),

          // Tombol untuk menambah counter
          Container(
            color: Colors.cyan[200],
            padding: EdgeInsets.all(5.0),

            child: IconButton(
              onPressed: _incrementCounter, // Memanggil fungsi increment
              icon: Icon(
                Icons.add,
                color: Colors.black,
                size: 16,
              ),
            ),
          ),
        ],
      ),
    );
  }
}
