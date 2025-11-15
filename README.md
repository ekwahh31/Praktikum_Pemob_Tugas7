# TUGAS 7 PERTEMUAN 9 PRAKTIKUM PEMOGRAMAN MOBILE
Berikut ini merupakan laporan hasil pengerjaan tugas 7 pertemuan 9 praktikum pemograman web. <br>
Nama  : Eka Bintang Wicaksono <br>
NIM   : H1D023054 <br>
Shift : B/A <br>

# Screenshoot Aplikasi

# 1. Halaman Login
<img width="503" height="1000" alt="image" src="https://github.com/user-attachments/assets/ab5ea1a8-97b5-4a54-8e41-9e61d5c98e66" />

# 2. Halaman Home
<img width="501" height="1003" alt="image" src="https://github.com/user-attachments/assets/e3567b33-bfcd-4c1c-80f6-04b1e7ae361a" />

# 3. Halaman About Me
<img width="502" height="1005" alt="image" src="https://github.com/user-attachments/assets/8666a8a8-3407-4d9e-a2bc-7d3730e82466" />

# Penjelasan Kode
1. Halaman Login
Pada halaman Login_Page terdapat State Variables yang berfungsi untuk mengontrol input username serta password
```
final TextEditingController _usernameController  
final TextEditingController _passwordController  
var namauser; 
```

dan terdapat juga _saveUsername() yang berfungsi sebagai wadah untuk menyimpan username ke local storage agar dapat diakses di halaman lain
```
void _saveUsername() async {
  SharedPreferences prefs = await SharedPreferences.getInstance(); 
  prefs.setString('username', _usernameController.text);  
}
```

2. Halaman Home
Pada Home_Page terdapat State Management yang berfungsi untuk load username dari SharedPreferences saat halaman pertama kali dibuka
```
var namauser;  
void _loadUsername() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  namauser = prefs.getString('username');  
  setState(() {});  
}

@override
void initState() {
  super.initState();
  _loadUsername();  
}
```

Pada halaman Home ini terdapat 5 card yang berisi kontak yang dapat diklik dan akan langsung di arahkan menuju halaman yang dituju
```
_buildContactCard(
  icon: Icons.email_outlined,
  title: 'Email',
  subtitle: 'bintangeka836@gmail.com',
  color: Color(0xFFEA4335),  
  url: 'mailto:bintangeka836@gmail.com',  
```

lalu untuk membuka URL eksternal menggunakan _launchURL()
```
Future<void> _launchURL(String url) async {
  final Uri uri = Uri.parse(url);  
  if (!await launchUrl(uri, mode: LaunchMode.externalApplication)) {
    // Jika gagal membuka link
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Could not launch URL'))  
```

3. Halaman About_Me
Pada halaman About_Me, card yang digunakan untuk menampilkan info personal adalah menggunakan _buildInfoCard()
```
Widget _buildInfoCard({
  required IconData icon,
  required String title,
  required String content,
  required Color color,
}) {
  return Container(
    child: Row([
      Container(  
        decoration: BoxDecoration(color: color.withOpacity(0.1)),
        child: Icon(icon, color: color),
      Column([
        Text(title),  
        Text(content),  
```

dan untuk bagian bio menggunakan container
```
Container(
  padding: EdgeInsets.all(20),
  decoration: BoxDecoration(  
    color: Colors.white,
    boxShadow: [...]
  child: Text(
    'Halo! Saya adalah mahasiswa...',  
    textAlign: TextAlign.justify,  
```

lalu untuk bagian interest menggunakan _buildInterestChip()
```
Widget _buildInterestChip(String label, Color color) {
  return Container(
    decoration: BoxDecoration(
      gradient: LinearGradient(colors: [color, ...]), 
      borderRadius: BorderRadius.circular(20),  
    child: Text(label), 
```

4. Halaman Side Menu
Pada halaman side menu, menggunakan widget yang reusable untuk menunya menggunakan _buildMenuItem()
```
Widget _buildMenuItem(
  BuildContext context, {
  required IconData icon,
  required String title,
  required String subtitle,
  required VoidCallback onTap,
}) {
  return Container(
    decoration: BoxDecoration(
      color: Colors.white.withOpacity(0.1),  
    child: ListTile(
      leading: Container(  
        child: Icon(icon, color: Color(0xFF6C63FF)),
      title: Text(title),  
      subtitle: Text(subtitle),
      trailing: Icon(Icons.arrow_forward_ios), 
      onTap: onTap, 
```
