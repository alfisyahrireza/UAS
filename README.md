import 'package:flutter/material.dart';

  
void main() => runApp(Uas());

class Uas extends StatelessWidget {
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Alfisyahri Reza',
      home: Alfisyahri6SIA1(),
    );
  }
}

class Alfisyahri6SIA1 extends StatefulWidget {
  MyTabsState createState() => new MyTabsState();
}

class MyTabsState extends State<Alfisyahri6SIA1>
    with SingleTickerProviderStateMixin {
  TabController controller;
  var _scaffoldKey = new GlobalKey<ScaffoldState>();

  void initState() {
    super.initState();
    controller = new TabController(vsync: this, length: 2);
  }

  void dispose() {
    controller.dispose();
    super.dispose();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        leading: IconButton(
            icon: Icon(Icons.menu),
            onPressed: () => _scaffoldKey.currentState.openDrawer()),
        title: Text('Alfisyahri Reza'),
        actions: <Widget>[
          IconButton(icon: Icon(Icons.search), onPressed: () {}),
          IconButton(icon: Icon(Icons.more_vert), onPressed: () {}),
        ],
        bottom: TabBar(controller: controller, tabs: <Tab>[
          Tab(text: "Input Data Kamu"),
          Tab(text: "Kalkulator"),
        ]),
      ),
      // body: TabBarView(),
      body: TabBarView(controller: controller, children: <Widget>[
        Mahasiswa(),
        Kalkulator(),
      ]),
      drawer: Menu(),
    );
  }
}
class DataMahasiswa{
  String nama;
  String jurusan;
  String jkelamin;
  
  
  DataMahasiswa({this.nama, this.jurusan, this.jkelamin});
  
}

// class Mahasiswa
class Mahasiswa extends StatefulWidget {
  _MyappState createState() => _MyappState();
}

class _MyappState extends State<Mahasiswa> {
  //deklarasi variabel
  final txtnamamhs = TextEditingController();
  final txtjurusan = TextEditingController();
  final txtjkelamin = TextEditingController();
  

  List<Widget> data = [];

  onTambah() {
    setState(() {
      data.add(ListTile(
        leading: Icon(Icons.people),
        title: Text(txtnamamhs.text),
        subtitle: Text(txtjkelamin.text),
        trailing: Text(txtjurusan.text),
      ));
      txtnamamhs.clear();
      txtjurusan.clear();
      txtjkelamin.clear();
    });
  }

  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        new Container(
          padding: EdgeInsets.all(10.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: <Widget>[
              TextField(
                controller: txtnamamhs,
                decoration: InputDecoration(hintText: 'Nama Mahasiswa'),
              ),
              TextField(
                controller: txtjurusan,
                decoration: InputDecoration(hintText: 'Jurusan'),
              ),
              TextField(
                controller: txtjkelamin,
                decoration: InputDecoration(hintText: 'Jenis Kelamin'),
              ),
              Divider(height: 5.0),
              ElevatedButton(child: Text("Tambah"), onPressed: onTambah),
            ],
          ),
        ),
        new Column(
          children: data,
        )
      ],
    );
  }
}

// class Menu
class Menu extends StatelessWidget {
  Widget build(BuildContext context) {
    return Drawer(
        elevation: 50.0,
        child: ListView(
          padding: EdgeInsets.zero,
          children: <Widget>[
            UserAccountsDrawerHeader(
              accountName: Text('Alfisyahri Reza Arrahman'),
              accountEmail: Text('rezaalfisyahri01@gmail.com'),
              currentAccountPicture: Image.network(
                  'https://lh3.googleusercontent.com/ogw/ADGmqu_n0wn9gL-PjNwUpIaQLmfzGDRHiSn8L54StneN5A=s32-c-mo'),
              decoration: BoxDecoration(color: Colors.blueAccent),
            ),
            ListTile(
              leading: Icon(Icons.account_circle),
              title: Text('Pemrograman Mobile 2'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.accessibility),
              title: Text('Sistem Informasi'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.account_balance),
              title: Text('STMIK Triguna Dharma'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.exit_to_app),
              title: Text('Keluar'),
              onTap: () {
                Navigator.pop(context);
              },
            )
          ],
        ));
  }
}

class Kalkulator extends StatefulWidget {
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<Kalkulator> {
  final txtharga = TextEditingController();
  final txtbeli = TextEditingController();

  String hasil = '' ;
  String bonus = '';
  
  onHitung() {
    setState(() {
      var harga = int.parse(txtharga.text);
      var beli = int.parse(txtbeli.text);
      var bayar = harga * beli;
      hasil = bayar.toString();
      if (bayar > 49999) {
        bonus = "Selamat Anda Mendapat Bonus Undian";
  }
        else{
        bonus = "Maaf Total Belanja Anda Belum Mencukupi";
        }
    });
  }
  
  
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(20.0),
      child: Column(
        children: <Widget>[
          TextField(
            controller: txtharga,
            decoration: new InputDecoration(
              labelText: "Input Harga",
            ),
          ),
          TextField(
            controller: txtbeli,
            decoration: new InputDecoration(
              labelText: "Input Jumlah Beli",
            ),
          ),
          ElevatedButton(
            child: Text("Hitung"),
            onPressed: onHitung,
          ),
          Text("Total Belanja = Rp.$hasil"),
          Text("$bonus"),
          Text(""),
          Text("Alfisyahri Reza Arrahman"),
        ],
      ),
    );
  }
}
