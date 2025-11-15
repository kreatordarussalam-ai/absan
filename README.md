<!doctype html>
<html lang="id" class="h-full">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Absensi Digital MAS PP Darussalam Kunir</title>
 <script src="https://cdn.tailwindcss.com"></script>
 <script 
src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
 <script src="/_sdk/data_sdk.js"></script>
 <script src="/_sdk/element_sdk.js"></script>
 <style>
 body {
 box-sizing: border-box;
 }
 .fade-in {
 animation: fadeIn 0.5s ease-in;
 }
 @keyframes fadeIn {
 from { opacity: 0; transform: translateY(20px); }
 to { opacity: 1; transform: translateY(0); }
 }
 .card-hover {
 transition: all 0.3s ease;
 }
 .card-hover:hover {
 transform: translateY(-2px);
 box-shadow: 0 10px 25px rgba(0,0,0,0.1);
 }
 .logo-preview {
 width: 96px;
 height: 96px;
 object-fit: contain;
 border-radius: 8px;
 }
 .photo-preview {
 width: 64px;
 height: 64px;
 object-fit: cover;
 border-radius: 50%;
 }
 .modal {
 backdrop-filter: blur(4px);
 }
 .loading-spinner {
 border: 3px solid #f3f3f3;
 border-top: 3px solid #16a34a;
 border-radius: 50%;
 width: 20px;
 height: 20px;
 animation: spin 1s linear infinite;
 }
 @keyframes spin {
 0% { transform: rotate(0deg); }
 100% { transform: rotate(360deg); }
 }
 </style>
 <style>@view-transition { navigation: auto; }</style>
</head>
<body class="h-full bg-gradient-to-br from-blue-50 to-green-50 font-sans">
 <div id="app" class="min-h-full"><!-- Halaman Sampul -->
 <div id="cover-page" class="min-h-full flex items-center justify-center p-6">
 <div class="bg-white rounded-2xl shadow-2xl p-8 max-w-lg w-full text-center fade￾in"><!-- Logo Sekolah -->
 <div class="mb-6">
 <div id="logo-container" class="w-24 h-24 mx-auto mb-4 flex items-center justify￾center">
 <svg id="default-logo" class="w-24 h-24 text-green-600" fill="currentColor" 
viewbox="0 0 24 24"><path d="M12 3L1 9l4 2.18v6L12 21l7-3.82v-6l2-
1.09V17h2V9L12 3zm6.82 6L12 12.72 5.18 9 12 5.28 18.82 9zM17 15.99l-5 2.73-5-
2.73v-3.72L12 15l5-2.73v3.72z" />
 </svg><img id="custom-logo" class="logo-preview hidden" alt="Logo Sekolah">
 </div><input type="file" id="logo-upload" accept="image/*" class="hidden"> 
<button id="upload-logo-btn" class="text-sm text-green-600 hover:text-green-700 
underline"> Upload Logo Sekolah </button>
 </div><!-- Nama Sekolah -->
 <h1 id="school-name" class="text-2xl font-bold text-gray-800 mb-2">MAS PP 
DARUSSALAM KUNIR</h1>
 <p id="school-address" class="text-gray-600 mb-4 text-sm">Jln. Kunir Rt. 24/09, 
Desa Simpar, Kec. Cipunagara Kab. Subang</p><!-- Pilihan Tahun Ajaran -->
 <div class="mb-6"><label for="tahun-ajaran-select" class="block text-sm font￾medium text-gray-700 mb-2">Tahun Ajaran</label> <select id="tahun-ajaran-select" 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500 focus:border-transparent"> <option 
value="2024/2025">2024/2025</option> <option value="2025/2026" 
selected>2025/2026</option> <option value="2026/2027">2026/2027</option> 
<option value="2027/2028">2027/2028</option> <option 
value="2028/2029">2028/2029</option> <option 
value="2029/2030">2029/2030</option> </select>
 </div><!-- Judul Aplikasi -->
 <div class="border-t border-b border-gray-200 py-4 mb-6">
 <h2 class="text-xl font-semibold text-green-700">ABSENSI DIGITAL</h2>
 <p class="text-gray-600 text-sm mt-1">Sistem Kehadiran Siswa &amp; Guru</p>
 </div><!-- Tombol Masuk --> <button id="enter-btn" class="w-full bg-green-600 
hover:bg-green-700 text-white font-semibold py-3 px-6 rounded-lg transition 
duration-300 transform hover:scale-105"> Masuk Aplikasi </button>
 </div>
 </div><!-- Halaman Utama -->
 <div id="main-page" class="hidden min-h-full"><!-- Header -->
 <header class="bg-white shadow-sm border-b">
 <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
 <div class="flex justify-between items-center py-4">
 <div class="flex items-center space-x-3">
 <div class="w-8 h-8 flex items-center justify-center">
 <svg id="header-default-logo" class="w-8 h-8 text-green-600" 
fill="currentColor" viewbox="0 0 24 24"><path d="M12 3L1 9l4 2.18v6L12 21l7-
3.82v-6l2-1.09V17h2V9L12 3zm6.82 6L12 12.72 5.18 9 12 5.28 18.82 9zM17 
15.99l-5 2.73-5-2.73v-3.72L12 15l5-2.73v3.72z" />
 </svg><img id="header-custom-logo" class="w-8 h-8 object-contain hidden" 
alt="Logo">
 </div>
 <div>
 <h1 class="text-xl font-bold text-gray-900">Absensi Digital</h1>
 <p class="text-sm text-gray-600">MAS PP Darussalam Kunir • <span 
id="current-year">2025/2026</span></p>
 </div>
 </div>
 <div class="flex items-center space-x-4">
 <div class="text-sm text-gray-600"><span id="current-date"></span>
 </div><button id="back-to-cover" class="text-gray-600 hover:text-gray-800 
transition duration-200">
 <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 
24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 
19l-7-7m0 0l7-7m-7 7h18" />
 </svg></button>
 </div>
 </div>
 </div>
 </header>
 <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6"><!-- Tab Navigation -->
 <div class="mb-6">
 <nav class="flex space-x-1 bg-gray-100 rounded-lg p-1 overflow-x-auto"><button 
id="tab-absensi" class="tab-btn flex-shrink-0 py-2 px-4 text-sm font-medium 
rounded-md transition duration-200 bg-white text-green-700 shadow-sm"> Input 
Absensi </button> <button id="tab-rekap" class="tab-btn flex-shrink-0 py-2 px-4 text￾sm font-medium rounded-md transition duration-200 text-gray-600 hover:text-gray-
800"> Rekap Kehadiran </button> <button id="tab-siswa" class="tab-btn flex-shrink-
0 py-2 px-4 text-sm font-medium rounded-md transition duration-200 text-gray-600 
hover:text-gray-800"> Data Siswa </button> <button id="tab-guru" class="tab-btn 
flex-shrink-0 py-2 px-4 text-sm font-medium rounded-md transition duration-200 text￾gray-600 hover:text-gray-800"> Data Guru </button> <button id="tab-kenaikan" 
class="tab-btn flex-shrink-0 py-2 px-4 text-sm font-medium rounded-md transition 
duration-200 text-gray-600 hover:text-gray-800"> Kenaikan Kelas </button> <button 
id="tab-rapat" class="tab-btn flex-shrink-0 py-2 px-4 text-sm font-medium rounded￾md transition duration-200 text-gray-600 hover:text-gray-800"> Rapat </button> 
<button id="tab-kehadiran-rapat" class="tab-btn flex-shrink-0 py-2 px-4 text-sm font￾medium rounded-md transition duration-200 text-gray-600 hover:text-gray-800"> 
Kehadiran Rapat </button> <button id="tab-laporan" class="tab-btn flex-shrink-0 py-
2 px-4 text-sm font-medium rounded-md transition duration-200 text-gray-600 
hover:text-gray-800"> Laporan </button>
 </nav>
 </div><!-- Form Input Absensi -->
 <div id="form-absensi" class="fade-in"><!-- Mode Selection -->
 <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Mode Absensi</h2>
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4"><button id="mode-individual" 
class="mode-btn p-4 border-2 border-green-500 bg-green-50 text-green-700 
rounded-lg transition duration-300 hover:bg-green-100">
 <div class="text-center">
 <svg class="w-8 h-8 mx-auto mb-2" fill="currentColor" viewbox="0 0 24 
24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-
2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z" />
 </svg>
 <h3 class="font-semibold">Absensi Individual</h3>
 <p class="text-sm mt-1">Input satu per satu</p>
 </div></button> <button id="mode-class" class="mode-btn p-4 border-2 border￾gray-300 text-gray-600 rounded-lg transition duration-300 hover:border-green-500 
hover:text-green-700 hover:bg-green-50">
 <div class="text-center">
 <svg class="w-8 h-8 mx-auto mb-2" fill="currentColor" viewbox="0 0 24 
24"><path d="M16 4c0-1.11.89-2 2-2s2 .89 2 2-.89 2-2 2-2-.89-2-2zM4 18v-
4h3v4h2v-7.5c0-1.1-.9-2-2-2s-2 .9-2 2V18H4zm14.5-2.5c0-.83-.67-1.5-1.5-1.5s-
1.5.67-1.5 1.5.67 1.5 1.5 1.5 1.5-.67 1.5-1.5zm3.5-.5c0 1.11-.89 2-2 2h-1v4h-2v-
6.5c0-1.1.9-2 2-2h1c1.11 0 2 .89 2 2z" />
 </svg>
 <h3 class="font-semibold">Absensi Per Kelas</h3>
 <p class="text-sm mt-1">Input seluruh kelas</p>
 </div></button>
 </div>
 </div><!-- Individual Mode -->
 <div id="individual-mode" class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Input Kehadiran 
Individual</h2>
 <form id="attendance-form" class="space-y-4">
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div><label for="role" class="block text-sm font-medium text-gray-700 mb-
1">Status</label> <select id="role" name="role" required class="w-full px-3 py-2 
border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border￾transparent"> <option value="">Pilih Status</option> <option 
value="Siswa">Siswa</option> <option value="Guru">Guru</option> </select>
 </div>
 <div><label for="nama" class="block text-sm font-medium text-gray-700 mb-
1">Nama Lengkap</label> <select id="nama" name="nama" required class="w-full 
px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 
focus:border-transparent"> <option value="">Pilih Nama</option> </select>
 </div>
 <div><label for="kelas" class="block text-sm font-medium text-gray-700 mb-
1">Kelas/Mata Pelajaran</label> <input type="text" id="kelas" name="kelas" 
readonly class="w-full px-3 py-2 border border-gray-300 rounded-lg bg-gray-50">
 </div>
 <div><label for="status" class="block text-sm font-medium text-gray-700 mb-
1">Kehadiran</label> <select id="status" name="status" required class="w-full px-3 
py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 
focus:border-transparent"> <option value="">Pilih Kehadiran</option> <option 
value="Hadir">Hadir</option> <option value="Izin">Izin</option> <option 
value="Sakit">Sakit</option> <option value="Alfa">Alfa</option> </select>
 </div>
 </div><button type="submit" id="submit-btn" class="w-full bg-green-600 
hover:bg-green-700 text-white font-semibold py-3 px-6 rounded-lg transition 
duration-300 flex items-center justify-center"> <span id="submit-text">Simpan 
Absensi</span>
 <div id="submit-loading" class="loading-spinner ml-2 hidden"></div></button>
 </form>
 </div><!-- Class Mode -->
 <div id="class-mode" class="hidden bg-white rounded-xl shadow-lg p-6 mb-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Absensi Per 
Kelas</h2><!-- Class Selection -->
 <div class="mb-6"><label for="class-select" class="block text-sm font-medium 
text-gray-700 mb-2">Pilih Kelas</label> <select id="class-select" class="w-full px-3 
py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 
focus:border-transparent"> <option value="">Pilih Kelas</option> <option value="X 
IPA 1">X IPA 1</option> <option value="X IPA 2">X IPA 2</option> <option value="X 
IPS 1">X IPS 1</option> <option value="X IPS 2">X IPS 2</option> <option 
value="XI IPA 1">XI IPA 1</option> <option value="XI IPA 2">XI IPA 2</option> 
<option value="XI IPS 1">XI IPS 1</option> <option value="XI IPS 2">XI IPS 
2</option> <option value="XII IPA 1">XII IPA 1</option> <option value="XII IPA 
2">XII IPA 2</option> <option value="XII IPS 1">XII IPS 1</option> <option 
value="XII IPS 2">XII IPS 2</option> </select>
 </div><!-- Student List for Class Attendance -->
 <div id="class-attendance-container" class="hidden">
 <div class="flex justify-between items-center mb-4">
 <h3 class="text-lg font-semibold text-gray-800">Daftar Siswa</h3>
 <div class="flex space-x-2"><button id="mark-all-present" class="bg-green-600 
hover:bg-green-700 text-white px-4 py-2 rounded-lg text-sm transition duration-300"> 
Semua Hadir </button> <button id="reset-attendance" class="bg-gray-500 hover:bg￾gray-600 text-white px-4 py-2 rounded-lg text-sm transition duration-300"> Reset 
</button>
 </div>
 </div>
 <div id="class-student-list" class="space-y-3 max-h-96 overflow-y-auto mb-
6"><!-- Student attendance list will be populated here -->
 </div><button id="save-class-attendance" class="w-full bg-green-600 hover:bg￾green-700 text-white font-semibold py-3 px-6 rounded-lg transition duration-300 flex 
items-center justify-center"> <span id="save-class-text">Simpan Absensi 
Kelas</span>
 <div id="save-class-loading" class="loading-spinner ml-2 
hidden"></div></button>
 </div>
 </div>
 </div><!-- Rekap Kehadiran -->
 <div id="rekap-kehadiran" class="hidden"><!-- Statistik -->
 <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
 <div class="bg-green-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-green-700" id="count-hadir">
 0
 </div>
 <div class="text-sm text-green-600">
 Hadir
 </div>
 </div>
 <div class="bg-yellow-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-yellow-700" id="count-izin">
 0
 </div>
 <div class="text-sm text-yellow-600">
 Izin
 </div>
 </div>
 <div class="bg-blue-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-blue-700" id="count-sakit">
 0
 </div>
 <div class="text-sm text-blue-600">
 Sakit
 </div>
 </div>
 <div class="bg-red-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-red-700" id="count-alfa">
 0
 </div>
 <div class="text-sm text-red-600">
 Alfa
 </div>
 </div>
 </div><!-- Filter -->
 <div class="bg-white rounded-xl shadow-lg p-4 mb-6">
 <div class="grid grid-cols-1 md:grid-cols-4 gap-4 items-center"><select id="filter￾role" class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500"> <option value="">Semua Status</option> <option 
value="Siswa">Siswa</option> <option value="Guru">Guru</option> </select> 
<select id="filter-status" class="px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500"> <option value="">Semua Kehadiran</option> 
<option value="Hadir">Hadir</option> <option value="Izin">Izin</option> <option 
value="Sakit">Sakit</option> <option value="Alfa">Alfa</option> </select> <input 
type="date" id="filter-date" class="px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500"> <button id="export-attendance-btn" class="bg￾blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition duration-300"> 
Export Excel </button>
 </div>
 </div><!-- Daftar Absensi -->
 <div class="bg-white rounded-xl shadow-lg overflow-hidden">
 <div class="px-6 py-4 border-b border-gray-200">
 <h3 class="text-lg font-semibold text-gray-800">Daftar Kehadiran</h3>
 </div>
 <div id="attendance-list" class="divide-y divide-gray-200 max-h-96 overflow-y￾auto">
 <div class="p-6 text-center text-gray-500">
 Belum ada data absensi. Silakan input kehadiran terlebih dahulu.
 </div>
 </div>
 </div>
 </div><!-- Data Siswa -->
 <div id="data-siswa" class="hidden">
 <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <div class="flex flex-wrap justify-between items-center mb-4 gap-4">
 <h2 class="text-lg font-semibold text-gray-800">Data Siswa</h2>
 <div class="flex flex-wrap gap-2"><button id="download-student-template-btn" 
class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition 
duration-300 text-sm"> Download Template </button> <button id="upload-student￾excel-btn" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg 
transition duration-300 text-sm"> Upload Excel </button> <button id="add-student￾btn" class="bg-purple-600 hover:bg-purple-700 text-white px-4 py-2 rounded-lg 
transition duration-300 text-sm"> Tambah Manual </button>
 </div>
 </div><!-- Filter Kelas -->
 <div class="mb-4"><select id="filter-kelas" class="px-3 py-2 border border-gray-
300 rounded-lg focus:ring-2 focus:ring-green-500"> <option value="">Semua 
Kelas</option> <option value="X IPA 1">X IPA 1</option> <option value="X IPA 2">X 
IPA 2</option> <option value="X IPS 1">X IPS 1</option> <option value="X IPS 
2">X IPS 2</option> <option value="XI IPA 1">XI IPA 1</option> <option value="XI 
IPA 2">XI IPA 2</option> <option value="XI IPS 1">XI IPS 1</option> <option 
value="XI IPS 2">XI IPS 2</option> <option value="XII IPA 1">XII IPA 1</option> 
<option value="XII IPA 2">XII IPA 2</option> <option value="XII IPS 1">XII IPS 
1</option> <option value="XII IPS 2">XII IPS 2</option> </select>
 </div><!-- Daftar Siswa -->
 <div id="student-list" class="space-y-4 max-h-96 overflow-y-auto"><!-- Data 
siswa akan dimuat di sini -->
 </div>
 </div><!-- Form Tambah Siswa -->
 <div id="add-student-form" class="hidden bg-white rounded-xl shadow-lg p-6">
 <h3 class="text-lg font-semibold text-gray-800 mb-4">Tambah Siswa Baru</h3>
 <form id="student-form" class="space-y-4">
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div><label for="student-nama" class="block text-sm font-medium text-gray-
700 mb-1">Nama Lengkap</label> <input type="text" id="student-nama" 
name="nama" required class="w-full px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500">
 </div>
 <div><label for="student-nisn" class="block text-sm font-medium text-gray-700 
mb-1">NISN</label> <input type="text" id="student-nisn" name="nisn" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500">
 </div>
 <div><label for="student-kelas" class="block text-sm font-medium text-gray-
700 mb-1">Kelas</label> <select id="student-kelas" name="kelas" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500"> <option value="">Pilih Kelas</option> <option value="X IPA 1">X IPA 
1</option> <option value="X IPA 2">X IPA 2</option> <option value="X IPS 1">X 
IPS 1</option> <option value="X IPS 2">X IPS 2</option> <option value="XI IPA 
1">XI IPA 1</option> <option value="XI IPA 2">XI IPA 2</option> <option value="XI 
IPS 1">XI IPS 1</option> <option value="XI IPS 2">XI IPS 2</option> <option 
value="XII IPA 1">XII IPA 1</option> <option value="XII IPA 2">XII IPA 2</option> 
<option value="XII IPS 1">XII IPS 1</option> <option value="XII IPS 2">XII IPS 
2</option> </select>
 </div>
 <div><label for="student-jk" class="block text-sm font-medium text-gray-700 
mb-1">Jenis Kelamin</label> <select id="student-jk" name="jenis_kelamin" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500"> <option value="">Pilih Jenis Kelamin</option> <option value="Laki￾laki">Laki-laki</option> <option value="Perempuan">Perempuan</option> </select>
 </div>
 <div><label for="student-foto" class="block text-sm font-medium text-gray-700 
mb-1">Upload Foto</label> <input type="file" id="student-foto" accept="image/*" 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500">
 </div>
 </div>
 <div class="flex space-x-4"><button type="submit" class="bg-green-600 
hover:bg-green-700 text-white px-6 py-2 rounded-lg transition duration-300"> 
Simpan Siswa </button> <button type="button" id="cancel-student-btn" class="bg￾gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition duration-
300"> Batal </button>
 </div>
 </form>
 </div>
 </div><!-- Data Guru -->
 <div id="data-guru" class="hidden">
 <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <div class="flex flex-wrap justify-between items-center mb-4 gap-4">
 <h2 class="text-lg font-semibold text-gray-800">Data Guru</h2>
 <div class="flex flex-wrap gap-2"><button id="download-teacher-template-btn" 
class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition 
duration-300 text-sm"> Download Template </button> <button id="upload-teacher￾excel-btn" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg 
transition duration-300 text-sm"> Upload Excel </button> <button id="add-teacher￾btn" class="bg-purple-600 hover:bg-purple-700 text-white px-4 py-2 rounded-lg 
transition duration-300 text-sm"> Tambah Manual </button>
 </div>
 </div><!-- Daftar Guru -->
 <div id="teacher-list" class="space-y-4 max-h-96 overflow-y-auto"><!-- Data 
guru akan dimuat di sini -->
 </div>
 </div><!-- Form Tambah Guru -->
 <div id="add-teacher-form" class="hidden bg-white rounded-xl shadow-lg p-6">
 <h3 class="text-lg font-semibold text-gray-800 mb-4">Tambah Guru Baru</h3>
 <form id="teacher-form" class="space-y-4">
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div><label for="teacher-nama" class="block text-sm font-medium text-gray-
700 mb-1">Nama Lengkap</label> <input type="text" id="teacher-nama" 
name="nama" required class="w-full px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500">
 </div>
 <div><label for="teacher-nip" class="block text-sm font-medium text-gray-700 
mb-1">NIP</label> <input type="text" id="teacher-nip" name="nip" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500">
 </div>
 <div><label for="teacher-mapel" class="block text-sm font-medium text-gray-
700 mb-1">Mata Pelajaran</label> <input type="text" id="teacher-mapel" 
name="mata_pelajaran" required class="w-full px-3 py-2 border border-gray-300 
rounded-lg focus:ring-2 focus:ring-green-500">
 </div>
 <div><label for="teacher-jk" class="block text-sm font-medium text-gray-700 
mb-1">Jenis Kelamin</label> <select id="teacher-jk" name="jenis_kelamin" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500"> <option value="">Pilih Jenis Kelamin</option> <option value="Laki￾laki">Laki-laki</option> <option value="Perempuan">Perempuan</option> </select>
 </div>
 <div><label for="teacher-foto" class="block text-sm font-medium text-gray-700 
mb-1">Upload Foto</label> <input type="file" id="teacher-foto" accept="image/*" 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500">
 </div>
 </div>
 <div class="flex space-x-4"><button type="submit" class="bg-green-600 
hover:bg-green-700 text-white px-6 py-2 rounded-lg transition duration-300"> 
Simpan Guru </button> <button type="button" id="cancel-teacher-btn" class="bg￾gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition duration-
300"> Batal </button>
 </div>
 </form>
 </div>
 </div><!-- Kenaikan Kelas -->
 <div id="kenaikan-kelas" class="hidden">
 <div class="bg-white rounded-xl shadow-lg p-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Kenaikan Kelas</h2>
 <div class="grid grid-cols-1 md:grid-cols-2 gap-6"><!-- Naik Kelas -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-green-700 mb-3">Naik Kelas</h3>
 <form id="promote-form" class="space-y-4">
 <div><label for="promote-from" class="block text-sm font-medium text-gray-
700 mb-1">Dari Kelas</label> <select id="promote-from" class="w-full px-3 py-2 
border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500"> <option 
value="">Pilih Kelas Asal</option> <option value="X IPA 1">X IPA 1</option> 
<option value="X IPA 2">X IPA 2</option> <option value="X IPS 1">X IPS 
1</option> <option value="X IPS 2">X IPS 2</option> <option value="XI IPA 1">XI 
IPA 1</option> <option value="XI IPA 2">XI IPA 2</option> <option value="XI IPS 
1">XI IPS 1</option> <option value="XI IPS 2">XI IPS 2</option> </select>
 </div>
 <div><label for="promote-to" class="block text-sm font-medium text-gray-700 
mb-1">Ke Kelas</label> <select id="promote-to" class="w-full px-3 py-2 border 
border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500"> <option 
value="">Pilih Kelas Tujuan</option> <option value="XI IPA 1">XI IPA 1</option> 
<option value="XI IPA 2">XI IPA 2</option> <option value="XI IPS 1">XI IPS 
1</option> <option value="XI IPS 2">XI IPS 2</option> <option value="XII IPA 1">XII 
IPA 1</option> <option value="XII IPA 2">XII IPA 2</option> <option value="XII IPS 
1">XII IPS 1</option> <option value="XII IPS 2">XII IPS 2</option> </select>
 </div><button type="submit" class="w-full bg-green-600 hover:bg-green-700 
text-white py-2 px-4 rounded-lg transition duration-300"> Proses Kenaikan Kelas 
</button>
 </form>
 </div><!-- Tinggal Kelas -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-red-700 mb-3">Tinggal Kelas</h3>
 <form id="repeat-form" class="space-y-4">
 <div><label for="repeat-student" class="block text-sm font-medium text-gray-
700 mb-1">Pilih Siswa</label> <select id="repeat-student" class="w-full px-3 py-2 
border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500"> <option 
value="">Pilih Siswa</option> </select>
 </div>
 <div><label for="repeat-reason" class="block text-sm font-medium text-gray-
700 mb-1">Alasan</label> <textarea id="repeat-reason" rows="3" class="w-full px-3 
py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500" 
placeholder="Masukkan alasan tinggal kelas"></textarea>
 </div><button type="submit" class="w-full bg-red-600 hover:bg-red-700 text￾white py-2 px-4 rounded-lg transition duration-300"> Proses Tinggal Kelas </button>
 </form>
 </div>
 </div><!-- Riwayat Kenaikan Kelas -->
 <div class="mt-6 border-t pt-6">
 <h3 class="font-semibold text-gray-800 mb-4">Riwayat Kenaikan Kelas</h3>
 <div id="promotion-history" class="space-y-2">
 <p class="text-gray-500 text-sm">Belum ada riwayat kenaikan kelas.</p>
 </div>
 </div>
 </div>
 </div><!-- Rapat -->
 <div id="rapat" class="hidden"><!-- Mode Selection -->
 <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Jenis Rapat</h2>
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4"><button id="rapat-guru" 
class="rapat-type-btn p-4 border-2 border-green-500 bg-green-50 text-green-700 
rounded-lg transition duration-300 hover:bg-green-100">
 <div class="text-center">
 <svg class="w-8 h-8 mx-auto mb-2" fill="currentColor" viewbox="0 0 24 
24"><path d="M12 2C13.1 2 14 2.9 14 4C14 5.1 13.1 6 12 6C10.9 6 10 5.1 10 4C10 
2.9 10.9 2 12 2ZM21 9V7L15 1H5C3.89 1 3 1.89 3 3V21C3 22.11 3.89 23 5 
23H11V21H5V19H9V17H5V15H11V13H5V11H9V9H5V7H13V9H21ZM13 
13V15H15V13H13ZM17 13V15H19V13H17ZM13 17V19H15V17H13ZM17 
17V19H19V17H17Z" />
 </svg>
 <h3 class="font-semibold">Rapat Guru</h3>
 <p class="text-sm mt-1">Rapat dewan guru</p>
 </div></button> <button id="rapat-staf" class="rapat-type-btn p-4 border-2 
border-gray-300 text-gray-600 rounded-lg transition duration-300 hover:border￾green-500 hover:text-green-700 hover:bg-green-50">
 <div class="text-center">
 <svg class="w-8 h-8 mx-auto mb-2" fill="currentColor" viewbox="0 0 24 
24"><path d="M16 4C18.2 4 20 5.8 20 8S18.2 12 16 12 12 10.2 12 8 13.8 4 16 
4M16 14C20.4 14 24 15.8 24 18V20H8V18C8 15.8 11.6 14 16 14M8.5 4C10.7 4 
12.5 5.8 12.5 8S10.7 12 8.5 12 4.5 10.2 4.5 8 6.3 4 8.5 4M8.5 14C12.9 14 16.5 15.8 
16.5 18V20H0V18C0 15.8 4.1 14 8.5 14Z" />
 </svg>
 <h3 class="font-semibold">Rapat Staf</h3>
 <p class="text-sm mt-1">Rapat staf administrasi</p>
 </div></button>
 </div>
 </div><!-- Meeting Form -->
 <div id="meeting-form" class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-4">Buat Rapat Baru</h2>
 <form id="create-meeting-form" class="space-y-4">
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div><label for="meeting-title" class="block text-sm font-medium text-gray-700 
mb-1">Judul Rapat</label> <input type="text" id="meeting-title" name="title" required 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500">
 </div>
 <div><label for="meeting-date" class="block text-sm font-medium text-gray-
700 mb-1">Tanggal Rapat</label> <input type="date" id="meeting-date" 
name="date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500">
 </div>
 <div><label for="meeting-time" class="block text-sm font-medium text-gray-700 
mb-1">Waktu Mulai</label> <input type="time" id="meeting-time" name="time" 
required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 
focus:ring-green-500">
 </div>
 <div><label for="meeting-location" class="block text-sm font-medium text-gray-
700 mb-1">Tempat</label> <input type="text" id="meeting-location" name="location" 
required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 
focus:ring-green-500" placeholder="Ruang Guru / Aula / dll">
 </div>
 </div>
 <div><label for="meeting-agenda" class="block text-sm font-medium text-gray-
700 mb-1">Agenda Rapat</label> <textarea id="meeting-agenda" name="agenda" 
rows="4" required class="w-full px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500" placeholder="Masukkan agenda rapat (pisahkan 
dengan enter untuk setiap poin)"></textarea>
 </div><button type="submit" id="create-meeting-btn" class="w-full bg-green-600 
hover:bg-green-700 text-white font-semibold py-3 px-6 rounded-lg transition 
duration-300 flex items-center justify-center"> <span id="create-meeting-text">Buat 
Rapat</span>
 <div id="create-meeting-loading" class="loading-spinner ml-2 
hidden"></div></button>
 </form>
 </div><!-- Meeting List -->
 <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
 <div class="flex justify-between items-center mb-4">
 <h2 class="text-lg font-semibold text-gray-800">Daftar Rapat</h2><select 
id="filter-meeting-type" class="px-3 py-2 border border-gray-300 rounded-lg 
focus:ring-2 focus:ring-green-500"> <option value="">Semua Rapat</option> 
<option value="Rapat Guru">Rapat Guru</option> <option value="Rapat 
Staf">Rapat Staf</option> </select>
 </div>
 <div id="meeting-list" class="space-y-4 max-h-96 overflow-y-auto">
 <div class="p-6 text-center text-gray-500">
 Belum ada rapat yang dibuat.
 </div>
 </div>
 </div>
 </div><!-- Meeting Detail Modal -->
 <div id="meeting-detail-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 
modal flex items-center justify-center z-50">
 <div class="bg-white rounded-xl p-6 max-w-4xl w-full mx-4 max-h-[90vh] 
overflow-y-auto">
 <div class="flex justify-between items-center mb-6">
 <h3 class="text-xl font-semibold text-gray-800" id="modal-meeting-title">Detail 
Rapat</h3><button id="close-meeting-modal" class="text-gray-500 hover:text-gray-
700">
 <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 
24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 
18L18 6M6 6l12 12" />
 </svg></button>
 </div><!-- Meeting Info -->
 <div id="meeting-info" class="mb-6 p-4 bg-gray-50 rounded-lg"><!-- Meeting 
details will be populated here -->
 </div><!-- Attendance Section -->
 <div class="mb-6">
 <h4 class="text-lg font-semibold text-gray-800 mb-4">Absensi Peserta</h4>
 <div id="meeting-attendance-list" class="space-y-3 max-h-64 overflow-y-auto 
mb-4"><!-- Attendance list will be populated here -->
 </div>
 <div class="flex space-x-2"><button id="mark-all-present-meeting" class="bg￾green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg text-sm transition 
duration-300"> Semua Hadir </button> <button id="save-meeting-attendance" 
class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg text-sm 
transition duration-300 flex items-center"> <span id="save-meeting-attendance￾text">Simpan Absensi</span>
 <div id="save-meeting-attendance-loading" class="loading-spinner ml-2 
hidden"></div></button>
 </div>
 </div><!-- Minutes Section -->
 <div class="mb-6">
 <h4 class="text-lg font-semibold text-gray-800 mb-4">Notulen Rapat</h4>
 <div class="space-y-4">
 <div><label for="meeting-minutes" class="block text-sm font-medium text-gray-
700 mb-2">Isi Notulen</label> <textarea id="meeting-minutes" rows="8" class="w￾full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500" 
placeholder="Masukkan hasil pembahasan, keputusan, dan tindak lanjut 
rapat..."></textarea>
 </div>
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div><label for="meeting-decisions" class="block text-sm font-medium text￾gray-700 mb-2">Keputusan Rapat</label> <textarea id="meeting-decisions" 
rows="4" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 
focus:ring-green-500" placeholder="Keputusan yang diambil dalam 
rapat..."></textarea>
 </div>
 <div><label for="meeting-followup" class="block text-sm font-medium text￾gray-700 mb-2">Tindak Lanjut</label> <textarea id="meeting-followup" rows="4" 
class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring￾green-500" placeholder="Tindak lanjut yang harus dilakukan..."></textarea>
 </div>
 </div>
 <div class="flex space-x-4"><button id="save-minutes" class="bg-purple-600 
hover:bg-purple-700 text-white px-6 py-2 rounded-lg transition duration-300 flex 
items-center"> <span id="save-minutes-text">Simpan Notulen</span>
 <div id="save-minutes-loading" class="loading-spinner ml-2 
hidden"></div></button> <button id="export-minutes" class="bg-orange-600 
hover:bg-orange-700 text-white px-6 py-2 rounded-lg transition duration-300"> 
Export Notulen </button>
 </div>
 </div>
 </div>
 </div>
 </div><!-- Kehadiran Rapat -->
 <div id="kehadiran-rapat" class="hidden"><!-- Statistik Kehadiran Rapat -->
 <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
 <div class="bg-green-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-green-700" id="count-rapat-hadir">
 0
 </div>
 <div class="text-sm text-green-600">
 Hadir Rapat
 </div>
 </div>
 <div class="bg-red-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-red-700" id="count-rapat-tidak-hadir">
 0
 </div>
 <div class="text-sm text-red-600">
 Tidak Hadir
 </div>
 </div>
 <div class="bg-blue-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-blue-700" id="count-total-rapat">
 0
 </div>
 <div class="text-sm text-blue-600">
 Total Rapat
 </div>
 </div>
 <div class="bg-purple-100 rounded-lg p-4 text-center">
 <div class="text-2xl font-bold text-purple-700" id="count-peserta-aktif">
 0
 </div>
 <div class="text-sm text-purple-600">
 Peserta Aktif
 </div>
 </div>
 </div><!-- Filter Kehadiran Rapat -->
 <div class="bg-white rounded-xl shadow-lg p-4 mb-6">
 <div class="grid grid-cols-1 md:grid-cols-4 gap-4 items-center"><select id="filter￾rapat-type" class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 
focus:ring-green-500"> <option value="">Semua Jenis Rapat</option> <option 
value="Rapat Guru">Rapat Guru</option> <option value="Rapat Staf">Rapat 
Staf</option> </select> <select id="filter-rapat-status" class="px-3 py-2 border 
border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500"> <option 
value="">Semua Status</option> <option value="Hadir">Hadir</option> <option 
value="Tidak Hadir">Tidak Hadir</option> </select> <input type="date" id="filter￾rapat-date" class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 
focus:ring-green-500"> <button id="export-meeting-attendance-btn" class="bg-blue-
600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition duration-300"> 
Export Excel </button>
 </div>
 </div><!-- Daftar Kehadiran Rapat -->
 <div class="bg-white rounded-xl shadow-lg overflow-hidden">
 <div class="px-6 py-4 border-b border-gray-200">
 <h3 class="text-lg font-semibold text-gray-800">Daftar Kehadiran Rapat</h3>
 </div>
 <div id="meeting-attendance-list-view" class="divide-y divide-gray-200 max-h-96 
overflow-y-auto">
 <div class="p-6 text-center text-gray-500">
 Belum ada data kehadiran rapat.
 </div>
 </div>
 </div><!-- Rekap Per Peserta -->
 <div class="bg-white rounded-xl shadow-lg p-6 mt-6">
 <h3 class="text-lg font-semibold text-gray-800 mb-4">Rekap Kehadiran Per 
Peserta</h3>
 <div id="participant-summary" class="space-y-4 max-h-64 overflow-y-auto">
 <div class="p-4 text-center text-gray-500">
 Belum ada data peserta rapat.
 </div>
 </div>
 </div>
 </div><!-- Laporan -->
 <div id="laporan" class="hidden">
 <div class="bg-white rounded-xl shadow-lg p-6">
 <h2 class="text-lg font-semibold text-gray-800 mb-6">Laporan &amp; Export 
Data</h2>
 <div class="grid grid-cols-1 md:grid-cols-2 gap-6"><!-- Export Siswa -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-blue-700 mb-3">Export Data Siswa</h3>
 <div class="space-y-3"><button id="export-all-students-btn" class="w-full bg￾blue-600 hover:bg-blue-700 text-white py-2 px-4 rounded-lg transition duration-300"> 
Export Semua Siswa </button>
 <div class="flex space-x-2"><select id="export-student-class" class="flex-1 px-
3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"> <option 
value="">Pilih Kelas</option> <option value="X IPA 1">X IPA 1</option> <option 
value="X IPA 2">X IPA 2</option> <option value="X IPS 1">X IPS 1</option> 
<option value="X IPS 2">X IPS 2</option> <option value="XI IPA 1">XI IPA 
1</option> <option value="XI IPA 2">XI IPA 2</option> <option value="XI IPS 1">XI 
IPS 1</option> <option value="XI IPS 2">XI IPS 2</option> <option value="XII IPA 
1">XII IPA 1</option> <option value="XII IPA 2">XII IPA 2</option> <option 
value="XII IPS 1">XII IPS 1</option> <option value="XII IPS 2">XII IPS 2</option>
</select> <button id="export-class-students-btn" class="bg-blue-600 hover:bg-blue-
700 text-white py-2 px-4 rounded-lg transition duration-300"> Export Kelas </button>
 </div>
 </div>
 </div><!-- Export Guru -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-green-700 mb-3">Export Data Guru</h3>
 <div class="space-y-3"><button id="export-all-teachers-btn" class="w-full bg￾green-600 hover:bg-green-700 text-white py-2 px-4 rounded-lg transition duration-
300"> Export Semua Guru </button>
 </div>
 </div><!-- Export Absensi -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-purple-700 mb-3">Export Rekap Absensi</h3>
 <div class="space-y-3">
 <div class="grid grid-cols-2 gap-2"><input type="date" id="export-date-from" 
class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-
500"> <input type="date" id="export-date-to" class="px-3 py-2 border border-gray-
300 rounded-lg focus:ring-2 focus:ring-purple-500">
 </div><button id="export-attendance-range-btn" class="w-full bg-purple-600 
hover:bg-purple-700 text-white py-2 px-4 rounded-lg transition duration-300"> Export 
Absensi Periode </button>
 </div>
 </div><!-- Export Individual -->
 <div class="border rounded-lg p-4">
 <h3 class="font-semibold text-orange-700 mb-3">Export Individual</h3>
 <div class="space-y-3"><select id="export-individual-person" class="w-full px-3 
py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500"> 
<option value="">Pilih Siswa/Guru</option> </select> <button id="export-individual￾btn" class="w-full bg-orange-600 hover:bg-orange-700 text-white py-2 px-4 rounded￾lg transition duration-300"> Export Data Individual </button>
 </div>
 </div>
 </div>
 </div>
 </div>
 </div>
 </div><!-- Modal Upload Excel -->
 <div id="upload-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 modal 
flex items-center justify-center z-50">
 <div class="bg-white rounded-xl p-6 max-w-md w-full mx-4">
 <h3 class="text-lg font-semibold text-gray-800 mb-4" id="modal-title">Upload File 
Excel</h3>
 <div class="space-y-4"><input type="file" id="excel-file-input" accept=".xlsx,.xls" 
class="w-full px-3 py-2 border border-gray-300 rounded-lg">
 <div class="text-sm text-gray-600">
 <p>Format file yang didukung: .xlsx, .xls</p>
 <p>Pastikan format sesuai dengan template yang telah diunduh.</p>
 </div>
 <div class="flex space-x-4"><button id="upload-excel-btn" class="flex-1 bg￾green-600 hover:bg-green-700 text-white py-2 px-4 rounded-lg transition duration-
300"> Upload </button> <button id="cancel-upload-btn" class="flex-1 bg-gray-500 
hover:bg-gray-600 text-white py-2 px-4 rounded-lg transition duration-300"> Batal 
</button>
 </div>
 </div>
 </div>
 </div><!-- Hidden file inputs --> <input type="file" id="student-excel-input" 
accept=".xlsx,.xls" class="hidden"> <input type="file" id="teacher-excel-input" 
accept=".xlsx,.xls" class="hidden">
 </div>
 <script>
 // Konfigurasi default
 const defaultConfig = {
 nama_sekolah: "MAS PP DARUSSALAM KUNIR",
 alamat_sekolah: "Jln. Kunir Rt. 24/09, Desa Simpar, Kec. Cipunagara Kab. 
Subang",
 kepala_sekolah: ""
 };
 // State management
 let currentData = [];
 let currentTab = 'absensi';
 let currentYear = '2025/2026';
 let isLoading = false;
 let logoUrl = null;
 let uploadType = '';
 let currentMeetingType = 'Rapat Guru';
 let currentMeeting = null;
 // Data handler untuk SDK
 const dataHandler = {
 onDataChanged(data) {
 currentData = data.filter(item => item.tahun_ajaran === currentYear);
 updateStatistics();
 renderAttendanceList();
 renderStudentList();
 renderTeacherList();
 updateNameDropdown();
 updateRepeatStudentDropdown();
 updateIndividualExportDropdown();
 renderMeetingList();
 updateMeetingAttendanceStatistics();
 renderMeetingAttendanceListView();
 renderParticipantSummary();
 }
 };
 // Inisialisasi SDK
 async function initializeApp() {
 if (window.dataSdk) {
 const result = await window.dataSdk.init(dataHandler);
 if (!result.isOk) {
 console.error("Failed to initialize data SDK");
 }
 }
 if (window.elementSdk) {
 await window.elementSdk.init({
 defaultConfig,
 onConfigChange: async (config) => {
 document.getElementById('school-name').textContent = 
config.nama_sekolah || defaultConfig.nama_sekolah;
 document.getElementById('school-address').textContent = 
config.alamat_sekolah || defaultConfig.alamat_sekolah;
 },
 mapToCapabilities: (config) => ({
 recolorables: [
 {
 get: () => config.primary_color || "#16a34a",
 set: (value) => {
 config.primary_color = value;
 window.elementSdk.setConfig({ primary_color: value });
 }
 }
 ],
 borderables: [],
 fontEditable: undefined,
 fontSizeable: undefined
 }),
 mapToEditPanelValues: (config) => new Map([
 ["nama_sekolah", config.nama_sekolah || 
defaultConfig.nama_sekolah],
 ["alamat_sekolah", config.alamat_sekolah || 
defaultConfig.alamat_sekolah],
 ["kepala_sekolah", config.kepala_sekolah || 
defaultConfig.kepala_sekolah]
 ])
 });
 }
 updateCurrentDate();
 setInterval(updateCurrentDate, 60000); // Update setiap menit
 }
 function updateCurrentDate() {
 const now = new Date();
 const options = { 
 weekday: 'long', 
 year: 'numeric', 
 month: 'long', 
 day: 'numeric',
 timeZone: 'Asia/Jakarta'
 };
 document.getElementById('current-date').textContent = 
now.toLocaleDateString('id-ID', options);
 }
 // Logo upload functionality
 document.getElementById('upload-logo-btn').addEventListener('click', () => {
 document.getElementById('logo-upload').click();
 });
 document.getElementById('logo-upload').addEventListener('change', (e) => {
 const file = e.target.files[0];
 if (file) {
 const reader = new FileReader();
 reader.onload = (e) => {
 logoUrl = e.target.result;
 updateLogoDisplay();
 };
 reader.readAsDataURL(file);
 }
 });
 function updateLogoDisplay() {
 const defaultLogos = document.querySelectorAll('#default-logo, #header￾default-logo');
 const customLogos = document.querySelectorAll('#custom-logo, #header￾custom-logo');
 if (logoUrl) {
 defaultLogos.forEach(logo => logo.classList.add('hidden'));
 customLogos.forEach(logo => {
 logo.src = logoUrl;
 logo.classList.remove('hidden');
 });
 } else {
 defaultLogos.forEach(logo => logo.classList.remove('hidden'));
 customLogos.forEach(logo => logo.classList.add('hidden'));
 }
 }
 // Tahun ajaran selection
 document.getElementById('tahun-ajaran-select').addEventListener('change', (e) 
=> {
 currentYear = e.target.value;
 document.getElementById('current-year').textContent = currentYear;
 });
 // State for attendance modes
 let currentAttendanceMode = 'individual';
 let selectedClass = '';
 let classStudents = [];
 // Event listeners
 document.getElementById('enter-btn').addEventListener('click', () => {
 currentYear = document.getElementById('tahun-ajaran-select').value;
 document.getElementById('current-year').textContent = currentYear;
 document.getElementById('cover-page').classList.add('hidden');
 document.getElementById('main-page').classList.remove('hidden');
 // Trigger data refresh for selected year
 if (window.dataSdk) {
 dataHandler.onDataChanged(currentData);
 }
 });
 document.getElementById('back-to-cover').addEventListener('click', () => {
 document.getElementById('main-page').classList.add('hidden');
 document.getElementById('cover-page').classList.remove('hidden');
 });
 // Attendance mode switching
 document.getElementById('mode-individual').addEventListener('click', () => 
switchAttendanceMode('individual'));
 document.getElementById('mode-class').addEventListener('click', () => 
switchAttendanceMode('class'));
 // Class attendance functionality
 document.getElementById('class-select').addEventListener('change', 
handleClassSelection);
 document.getElementById('mark-all-present').addEventListener('click', 
markAllPresent);
 document.getElementById('reset-attendance').addEventListener('click', 
resetClassAttendance);
 document.getElementById('save-class-attendance').addEventListener('click', 
saveClassAttendance);
 // Tab switching
 document.getElementById('tab-absensi').addEventListener('click', () => 
switchTab('absensi'));
 document.getElementById('tab-rekap').addEventListener('click', () => 
switchTab('rekap'));
 document.getElementById('tab-siswa').addEventListener('click', () => 
switchTab('siswa'));
 document.getElementById('tab-guru').addEventListener('click', () => 
switchTab('guru'));
 document.getElementById('tab-kenaikan').addEventListener('click', () => 
switchTab('kenaikan'));
 document.getElementById('tab-rapat').addEventListener('click', () => 
switchTab('rapat'));
 document.getElementById('tab-kehadiran-rapat').addEventListener('click', () => 
switchTab('kehadiran-rapat'));
 document.getElementById('tab-laporan').addEventListener('click', () => 
switchTab('laporan'));
 function switchTab(tab) {
 currentTab = tab;
 
 // Update tab buttons
 document.querySelectorAll('.tab-btn').forEach(btn => {
 btn.classList.remove('bg-white', 'text-green-700', 'shadow-sm');
 btn.classList.add('text-gray-600', 'hover:text-gray-800');
 });
 
 // Hide all content
 document.getElementById('form-absensi').classList.add('hidden');
 document.getElementById('rekap-kehadiran').classList.add('hidden');
 document.getElementById('data-siswa').classList.add('hidden');
 document.getElementById('data-guru').classList.add('hidden');
 document.getElementById('kenaikan-kelas').classList.add('hidden');
 document.getElementById('rapat').classList.add('hidden');
 document.getElementById('kehadiran-rapat').classList.add('hidden');
 document.getElementById('laporan').classList.add('hidden');
 
 // Show selected content and update tab
 const tabMap = {
 'absensi': ['tab-absensi', 'form-absensi'],
 'rekap': ['tab-rekap', 'rekap-kehadiran'],
 'siswa': ['tab-siswa', 'data-siswa'],
 'guru': ['tab-guru', 'data-guru'],
 'kenaikan': ['tab-kenaikan', 'kenaikan-kelas'],
 'rapat': ['tab-rapat', 'rapat'],
 'kehadiran-rapat': ['tab-kehadiran-rapat', 'kehadiran-rapat'],
 'laporan': ['tab-laporan', 'laporan']
 };
 if (tabMap[tab]) {
 const [tabId, contentId] = tabMap[tab];
 document.getElementById(tabId).classList.add('bg-white', 'text-green-700', 
'shadow-sm');
 document.getElementById(tabId).classList.remove('text-gray-600', 
'hover:text-gray-800');
 document.getElementById(contentId).classList.remove('hidden');
 }
 }
 // Update nama dropdown based on role
 document.getElementById('role').addEventListener('change', 
updateNameDropdown);
 function updateNameDropdown() {
 const role = document.getElementById('role').value;
 const namaSelect = document.getElementById('nama');
 
 namaSelect.innerHTML = '<option value="">Pilih Nama</option>';
 
 if (!role) return;
 const people = currentData.filter(item => 
 item.type === (role === 'Siswa' ? 'student' : 'teacher')
 );
 
 people.forEach(person => {
 const option = document.createElement('option');
 option.value = person.nama;
 option.textContent = `${person.nama} ${person.kelas ? '(' + person.kelas + 
')' : person.mata_pelajaran ? '(' + person.mata_pelajaran + ')' : ''}`;
 option.dataset.kelas = person.kelas || person.mata_pelajaran || '';
 option.dataset.id = person.id;
 namaSelect.appendChild(option);
 });
 }
 // Handle nama selection
 document.getElementById('nama').addEventListener('change', (e) => {
 const selectedOption = e.target.selectedOptions[0];
 if (selectedOption && selectedOption.dataset.kelas) {
 document.getElementById('kelas').value = selectedOption.dataset.kelas;
 } else {
 document.getElementById('kelas').value = '';
 }
 });
 // Form submission
 document.getElementById('attendance-form').addEventListener('submit', async 
(e) => {
 e.preventDefault();
 
 if (isLoading) return;
 
 if (currentData.length >= 999) {
 showToast("Batas maksimum 999 data absensi telah tercapai. Silakan 
hapus beberapa data terlebih dahulu.", "error");
 return;
 }
 const formData = new FormData(e.target);
 const selectedOption = 
document.getElementById('nama').selectedOptions[0];
 
 const attendanceData = {
 id: Date.now().toString(),
 nama: formData.get('nama'),
 nisn: selectedOption?.dataset.nisn || '',
 nip: selectedOption?.dataset.nip || '',
 role: formData.get('role'),
 kelas: formData.get('kelas') || '',
 mata_pelajaran: formData.get('kelas') || '',
 tanggal: new Date().toISOString().split('T')[0],
 status: formData.get('status'),
 waktu: new Date().toLocaleTimeString('id-ID'),
 foto_url: '',
 tahun_ajaran: currentYear,
 type: 'attendance',
 jenis_kelamin: '',
 tempat_lahir: '',
 tanggal_lahir: '',
 alamat: '',
 no_hp: ''
 };
 setLoading(true);
 
 if (window.dataSdk) {
 const result = await window.dataSdk.create(attendanceData);
 if (result.isOk) {
 e.target.reset();
 showToast("Data absensi berhasil disimpan!", "success");
 switchTab('rekap');
 } else {
 showToast("Gagal menyimpan data absensi. Silakan coba lagi.", 
"error");
 }
 }
 
 setLoading(false);
 });
 // Student management
 document.getElementById('add-student-btn').addEventListener('click', () => {
 document.getElementById('add-student-form').classList.remove('hidden');
 });
 document.getElementById('cancel-student-btn').addEventListener('click', () => {
 document.getElementById('add-student-form').classList.add('hidden');
 document.getElementById('student-form').reset();
 });
 document.getElementById('student-form').addEventListener('submit', async (e) 
=> {
 e.preventDefault();
 
 if (currentData.length >= 999) {
 showToast("Batas maksimum 999 data telah tercapai.", "error");
 return;
 }
 const formData = new FormData(e.target);
 const fotoFile = document.getElementById('student-foto').files[0];
 let fotoUrl = '';
 if (fotoFile) {
 fotoUrl = await convertFileToBase64(fotoFile);
 }
 const studentData = {
 id: `student_${Date.now()}`,
 nama: formData.get('nama'),
 nisn: formData.get('nisn'),
 nip: '',
 role: "Siswa",
 kelas: formData.get('kelas'),
 mata_pelajaran: '',
 tanggal: new Date().toISOString().split('T')[0],
 status: "",
 waktu: "",
 foto_url: fotoUrl,
 tahun_ajaran: currentYear,
 type: "student",
 jenis_kelamin: formData.get('jenis_kelamin'),
 tempat_lahir: '',
 tanggal_lahir: '',
 alamat: '',
 no_hp: ''
 };
 if (window.dataSdk) {
 const result = await window.dataSdk.create(studentData);
 if (result.isOk) {
 e.target.reset();
 document.getElementById('add-student-form').classList.add('hidden');
 showToast("Siswa baru berhasil ditambahkan!", "success");
 } else {
 showToast("Gagal menambahkan siswa baru.", "error");
 }
 }
 });
 // Teacher management
 document.getElementById('add-teacher-btn').addEventListener('click', () => {
 document.getElementById('add-teacher-form').classList.remove('hidden');
 });
 document.getElementById('cancel-teacher-btn').addEventListener('click', () => {
 document.getElementById('add-teacher-form').classList.add('hidden');
 document.getElementById('teacher-form').reset();
 });
 document.getElementById('teacher-form').addEventListener('submit', async (e) 
=> {
 e.preventDefault();
 
 if (currentData.length >= 999) {
 showToast("Batas maksimum 999 data telah tercapai.", "error");
 return;
 }
 const formData = new FormData(e.target);
 const fotoFile = document.getElementById('teacher-foto').files[0];
 let fotoUrl = '';
 if (fotoFile) {
 fotoUrl = await convertFileToBase64(fotoFile);
 }
 const teacherData = {
 id: `teacher_${Date.now()}`,
 nama: formData.get('nama'),
 nisn: '',
 nip: formData.get('nip'),
 role: "Guru",
 kelas: '',
 mata_pelajaran: formData.get('mata_pelajaran'),
 tanggal: new Date().toISOString().split('T')[0],
 status: "",
 waktu: "",
 foto_url: fotoUrl,
 tahun_ajaran: currentYear,
 type: "teacher",
 jenis_kelamin: formData.get('jenis_kelamin'),
 tempat_lahir: '',
 tanggal_lahir: '',
 alamat: '',
 no_hp: ''
 };
 if (window.dataSdk) {
 const result = await window.dataSdk.create(teacherData);
 if (result.isOk) {
 e.target.reset();
 document.getElementById('add-teacher-form').classList.add('hidden');
 showToast("Guru baru berhasil ditambahkan!", "success");
 } else {
 showToast("Gagal menambahkan guru baru.", "error");
 }
 }
 });
 // File conversion helper
 function convertFileToBase64(file) {
 return new Promise((resolve, reject) => {
 const reader = new FileReader();
 reader.onload = () => resolve(reader.result);
 reader.onerror = reject;
 reader.readAsDataURL(file);
 });
 }
 // Filter functionality
 document.getElementById('filter-role').addEventListener('change', 
renderAttendanceList);
 document.getElementById('filter-status').addEventListener('change', 
renderAttendanceList);
 document.getElementById('filter-date').addEventListener('change', 
renderAttendanceList);
 document.getElementById('filter-kelas').addEventListener('change', 
renderStudentList);
 function setLoading(loading) {
 isLoading = loading;
 const submitBtn = document.getElementById('submit-btn');
 const submitText = document.getElementById('submit-text');
 const submitLoading = document.getElementById('submit-loading');
 
 if (loading) {
 submitBtn.disabled = true;
 submitText.textContent = 'Menyimpan...';
 submitLoading.classList.remove('hidden');
 submitBtn.classList.add('opacity-50');
 } else {
 submitBtn.disabled = false;
 submitText.textContent = 'Simpan Absensi';
 submitLoading.classList.add('hidden');
 submitBtn.classList.remove('opacity-50');
 }
 }
 function showToast(message, type) {
 const toast = document.createElement('div');
 toast.className = `fixed top-4 right-4 px-6 py-3 rounded-lg shadow-lg z-50 
transform transition-all duration-300 ${
 type === 'success' ? 'bg-green-500 text-white' : 'bg-red-500 text-white'
 }`;
 toast.textContent = message;
 toast.style.transform = 'translateX(100%)';
 document.body.appendChild(toast);
 
 setTimeout(() => {
 toast.style.transform = 'translateX(0)';
 }, 100);
 
 setTimeout(() => {
 toast.style.transform = 'translateX(100%)';
 setTimeout(() => toast.remove(), 300);
 }, 3000);
 }
 function updateStatistics() {
 const attendanceData = currentData.filter(item => item.type === 
'attendance');
 const stats = {
 hadir: attendanceData.filter(item => item.status === 'Hadir').length,
 izin: attendanceData.filter(item => item.status === 'Izin').length,
 sakit: attendanceData.filter(item => item.status === 'Sakit').length,
 alfa: attendanceData.filter(item => item.status === 'Alfa').length
 };
 document.getElementById('count-hadir').textContent = stats.hadir;
 document.getElementById('count-izin').textContent = stats.izin;
 document.getElementById('count-sakit').textContent = stats.sakit;
 document.getElementById('count-alfa').textContent = stats.alfa;
 }
 function renderAttendanceList() {
 const container = document.getElementById('attendance-list');
 const filterRole = document.getElementById('filter-role').value;
 const filterStatus = document.getElementById('filter-status').value;
 const filterDate = document.getElementById('filter-date').value;
 let filteredData = currentData.filter(item => {
 if (item.type !== 'attendance') return false;
 if (filterRole && item.role !== filterRole) return false;
 if (filterStatus && item.status !== filterStatus) return false;
 if (filterDate && item.tanggal !== filterDate) return false;
 return true;
 });
 // Sort by newest first
 filteredData.sort((a, b) => new Date(b.tanggal + ' ' + b.waktu) - new 
Date(a.tanggal + ' ' + a.waktu));
 if (filteredData.length === 0) {
 container.innerHTML = '<div class="p-6 text-center text-gray-500">Tidak 
ada data yang sesuai dengan filter.</div>';
 return;
 }
 container.innerHTML = filteredData.map(item => {
 const statusColors = {
 'Hadir': 'bg-green-100 text-green-800',
 'Izin': 'bg-yellow-100 text-yellow-800',
 'Sakit': 'bg-blue-100 text-blue-800',
 'Alfa': 'bg-red-100 text-red-800'
 };
 const photoDisplay = item.foto_url ? 
 `<img src="${item.foto_url}" class="photo-preview" alt="Foto 
${item.nama}">` :
 `<div class="w-16 h-16 bg-gray-200 rounded-full flex items-center 
justify-center text-2xl">${item.jenis_kelamin === 'Perempuan' ? '👩' : '👨'}</div>`;
 return `
 <div class="p-4 hover:bg-gray-50 transition duration-200">
 <div class="flex items-center justify-between">
 <div class="flex items-center space-x-4">
 ${photoDisplay}
 <div>
 <h4 class="font-semibold text-gray-900">${item.nama}</h4>
 <p class="text-sm text-gray-600">${item.role} ${item.kelas || 
item.mata_pelajaran ? '• ' + (item.kelas || item.mata_pelajaran) : ''}</p>
 <p class="text-xs text-gray-500">${item.tanggal} • 
${item.waktu}</p>
 </div>
 </div>
 <div class="flex items-center space-x-3">
 <span class="px-3 py-1 rounded-full text-xs font-medium 
${statusColors[item.status]}">${item.status}</span>
 <button onclick="deleteAttendance('${item.id}')" class="text-red-
500 hover:text-red-700 transition duration-200">
 <svg class="w-5 h-5" fill="none" stroke="currentColor" 
viewBox="0 0 24 24">
 <path stroke-linecap="round" stroke-linejoin="round" 
stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-
1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
 </svg>
 </button>
 </div>
 </div>
 </div>
 `;
 }).join('');
 }
 function renderStudentList() {
 const container = document.getElementById('student-list');
 const filterKelas = document.getElementById('filter-kelas').value;
 let students = currentData.filter(item => {
 if (item.type !== 'student') return false;
 if (filterKelas && item.kelas !== filterKelas) return false;
 return true;
 });
 // Sort by class and name
 students.sort((a, b) => {
 if (a.kelas !== b.kelas) return a.kelas.localeCompare(b.kelas);
 return a.nama.localeCompare(b.nama);
 });
 if (students.length === 0) {
 container.innerHTML = '<div class="p-6 text-center text-gray-500">Tidak 
ada data siswa.</div>';
 return;
 }
 container.innerHTML = students.map(student => {
 const photoDisplay = student.foto_url ? 
 `<img src="${student.foto_url}" class="photo-preview" alt="Foto 
${student.nama}">` :
 `<div class="w-16 h-16 bg-gray-200 rounded-full flex items-center 
justify-center text-2xl">${student.jenis_kelamin === 'Perempuan' ? '👩🎓' : 
'👨🎓'}</div>`;
 return `
 <div class="border rounded-lg p-4 hover:bg-gray-50 transition duration-
200">
 <div class="flex items-center justify-between">
 <div class="flex items-center space-x-4">
 ${photoDisplay}
 <div>
 <h4 class="font-semibold text-gray-
900">${student.nama}</h4>
 <p class="text-sm text-gray-600">NISN: ${student.nisn}</p>
 <p class="text-sm text-green-600">${student.kelas}</p>
 <p class="text-xs text-gray-500">${student.jenis_kelamin}</p>
 </div>
 </div>
 <button onclick="deleteStudent('${student.id}')" class="text-red-500 
hover:text-red-700 transition duration-200">
 <svg class="w-5 h-5" fill="none" stroke="currentColor" 
viewBox="0 0 24 24">
 <path stroke-linecap="round" stroke-linejoin="round" stroke￾width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 
7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
 </svg>
 </button>
 </div>
 </div>
 `;
 }).join('');
 }
 function renderTeacherList() {
 const container = document.getElementById('teacher-list');
 let teachers = currentData.filter(item => item.type === 'teacher');
 // Sort by name
 teachers.sort((a, b) => a.nama.localeCompare(b.nama));
 if (teachers.length === 0) {
 container.innerHTML = '<div class="p-6 text-center text-gray-500">Tidak 
ada data guru.</div>';
 return;
 }
 container.innerHTML = teachers.map(teacher => {
 const photoDisplay = teacher.foto_url ? 
 `<img src="${teacher.foto_url}" class="photo-preview" alt="Foto 
${teacher.nama}">` :
 `<div class="w-16 h-16 bg-gray-200 rounded-full flex items-center 
justify-center text-2xl">${teacher.jenis_kelamin === 'Perempuan' ? '👩🏫' : 
'👨🏫'}</div>`;
 return `
 <div class="border rounded-lg p-4 hover:bg-gray-50 transition duration-
200">
 <div class="flex items-center justify-between">
 <div class="flex items-center space-x-4">
 ${photoDisplay}
 <div>
 <h4 class="font-semibold text-gray-
900">${teacher.nama}</h4>
 <p class="text-sm text-gray-600">NIP: ${teacher.nip}</p>
 <p class="text-sm text-blue-
600">${teacher.mata_pelajaran}</p>
 <p class="text-xs text-gray-500">${teacher.jenis_kelamin}</p>
 </div>
 </div>
 <button onclick="deleteTeacher('${teacher.id}')" class="text-red-500 
hover:text-red-700 transition duration-200">
 <svg class="w-5 h-5" fill="none" stroke="currentColor" 
viewBox="0 0 24 24">
 <path stroke-linecap="round" stroke-linejoin="round" stroke￾width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 
7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
 </svg>
 </button>
 </div>
 </div>
 `;
 }).join('');
 }
 function updateRepeatStudentDropdown() {
 const select = document.getElementById('repeat-student');
 const students = currentData.filter(item => item.type === 'student');
 
 select.innerHTML = '<option value="">Pilih Siswa</option>';
 
 students.forEach(student => {
 const option = document.createElement('option');
 option.value = student.id;
 option.textContent = `${student.nama} (${student.kelas})`;
 select.appendChild(option);
 });
 }
 function updateIndividualExportDropdown() {
 const select = document.getElementById('export-individual-person');
 const people = currentData.filter(item => item.type === 'student' || item.type 
=== 'teacher');
 
 select.innerHTML = '<option value="">Pilih Siswa/Guru</option>';
 
 people.forEach(person => {
 const option = document.createElement('option');
 option.value = person.id;
 option.textContent = `${person.nama} (${person.role})`;
 select.appendChild(option);
 });
 }
 // Excel template downloads
 document.getElementById('download-student-template￾btn').addEventListener('click', downloadStudentTemplate);
 document.getElementById('download-teacher-template￾btn').addEventListener('click', downloadTeacherTemplate);
 function downloadStudentTemplate() {
 const template = [
 ['Nama Lengkap', 'NISN', 'Kelas', 'Jenis Kelamin', 'Tempat Lahir', 'Tanggal 
Lahir', 'Alamat', 'No HP'],
 ['Contoh Siswa', '1234567890', 'X IPA 1', 'Laki-laki', 'Jakarta', '2005-01-01', 
'Jl. Contoh No. 1', '081234567890']
 ];
 
 const ws = XLSX.utils.aoa_to_sheet(template);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Template Siswa');
 XLSX.writeFile(wb, `Template_Siswa_${currentYear.replace('/', '-')}.xlsx`);
 }
 function downloadTeacherTemplate() {
 const template = [
 ['Nama Lengkap', 'NIP', 'Mata Pelajaran', 'Jenis Kelamin', 'Tempat Lahir', 
'Tanggal Lahir', 'Alamat', 'No HP'],
 ['Contoh Guru', '123456789012345678', 'Matematika', 'Laki-laki', 'Jakarta', 
'1980-01-01', 'Jl. Contoh No. 1', '081234567890']
 ];
 
 const ws = XLSX.utils.aoa_to_sheet(template);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Template Guru');
 XLSX.writeFile(wb, `Template_Guru_${currentYear.replace('/', '-')}.xlsx`);
 }
 // Excel upload functionality
 document.getElementById('upload-student-excel-btn').addEventListener('click', 
() => {
 uploadType = 'student';
 document.getElementById('modal-title').textContent = 'Upload Data Siswa';
 document.getElementById('upload-modal').classList.remove('hidden');
 });
 document.getElementById('upload-teacher-excel-btn').addEventListener('click', 
() => {
 uploadType = 'teacher';
 document.getElementById('modal-title').textContent = 'Upload Data Guru';
 document.getElementById('upload-modal').classList.remove('hidden');
 });
 document.getElementById('cancel-upload-btn').addEventListener('click', () => {
 document.getElementById('upload-modal').classList.add('hidden');
 document.getElementById('excel-file-input').value = '';
 });
 document.getElementById('upload-excel-btn').addEventListener('click', async () 
=> {
 const fileInput = document.getElementById('excel-file-input');
 const file = fileInput.files[0];
 
 if (!file) {
 showToast('Pilih file Excel terlebih dahulu!', 'error');
 return;
 }
 try {
 const data = await readExcelFile(file);
 if (uploadType === 'student') {
 await processStudentData(data);
 } else if (uploadType === 'teacher') {
 await processTeacherData(data);
 }
 
 document.getElementById('upload-modal').classList.add('hidden');
 fileInput.value = '';
 showToast(`Data ${uploadType === 'student' ? 'siswa' : 'guru'} berhasil 
diupload!`, 'success');
 } catch (error) {
 showToast('Gagal memproses file Excel. Pastikan format sesuai 
template.', 'error');
 }
 });
 function readExcelFile(file) {
 return new Promise((resolve, reject) => {
 const reader = new FileReader();
 reader.onload = (e) => {
 try {
 const data = new Uint8Array(e.target.result);
 const workbook = XLSX.read(data, { type: 'array' });
 const sheetName = workbook.SheetNames[0];
 const worksheet = workbook.Sheets[sheetName];
 const jsonData = XLSX.utils.sheet_to_json(worksheet);
 resolve(jsonData);
 } catch (error) {
 reject(error);
 }
 };
 reader.onerror = reject;
 reader.readAsArrayBuffer(file);
 });
 }
 async function processStudentData(data) {
 for (const row of data) {
 if (currentData.length >= 999) {
 showToast('Batas maksimum 999 data tercapai. Beberapa data tidak 
diproses.', 'error');
 break;
 }
 const studentData = {
 id: `student_${Date.now()}_${Math.random()}`,
 nama: row['Nama Lengkap'] || '',
 nisn: row['NISN'] || '',
 nip: '',
 role: "Siswa",
 kelas: row['Kelas'] || '',
 mata_pelajaran: '',
 tanggal: new Date().toISOString().split('T')[0],
 status: "",
 waktu: "",
 foto_url: '',
 tahun_ajaran: currentYear,
 type: "student",
 jenis_kelamin: row['Jenis Kelamin'] || '',
 tempat_lahir: row['Tempat Lahir'] || '',
 tanggal_lahir: row['Tanggal Lahir'] || '',
 alamat: row['Alamat'] || '',
 no_hp: row['No HP'] || ''
 };
 if (window.dataSdk && studentData.nama && studentData.nisn) {
 await window.dataSdk.create(studentData);
 }
 }
 }
 async function processTeacherData(data) {
 for (const row of data) {
 if (currentData.length >= 999) {
 showToast('Batas maksimum 999 data tercapai. Beberapa data tidak 
diproses.', 'error');
 break;
 }
 const teacherData = {
 id: `teacher_${Date.now()}_${Math.random()}`,
 nama: row['Nama Lengkap'] || '',
 nisn: '',
 nip: row['NIP'] || '',
 role: "Guru",
 kelas: '',
 mata_pelajaran: row['Mata Pelajaran'] || '',
 tanggal: new Date().toISOString().split('T')[0],
 status: "",
 waktu: "",
 foto_url: '',
 tahun_ajaran: currentYear,
 type: "teacher",
 jenis_kelamin: row['Jenis Kelamin'] || '',
 tempat_lahir: row['Tempat Lahir'] || '',
 tanggal_lahir: row['Tanggal Lahir'] || '',
 alamat: row['Alamat'] || '',
 no_hp: row['No HP'] || ''
 };
 if (window.dataSdk && teacherData.nama && teacherData.nip) {
 await window.dataSdk.create(teacherData);
 }
 }
 }
 // Export functionality
 document.getElementById('export-attendance-btn').addEventListener('click', 
exportAttendanceData);
 document.getElementById('export-all-students-btn').addEventListener('click', () 
=> exportStudentData());
 document.getElementById('export-class-students-btn').addEventListener('click', 
() => {
 const selectedClass = document.getElementById('export-student￾class').value;
 if (!selectedClass) {
 showToast('Pilih kelas terlebih dahulu!', 'error');
 return;
 }
 exportStudentData(selectedClass);
 });
 document.getElementById('export-all-teachers-btn').addEventListener('click', 
exportTeacherData);
 document.getElementById('export-attendance-range￾btn').addEventListener('click', exportAttendanceRange);
 document.getElementById('export-individual-btn').addEventListener('click', 
exportIndividualData);
 function exportAttendanceData() {
 const attendanceData = currentData.filter(item => item.type === 
'attendance');
 
 if (attendanceData.length === 0) {
 showToast('Tidak ada data absensi untuk diekspor.', 'error');
 return;
 }
 const exportData = attendanceData.map(item => ({
 'Tanggal': item.tanggal,
 'Waktu': item.waktu,
 'Nama': item.nama,
 'Role': item.role,
 'Kelas/Mata Pelajaran': item.kelas || item.mata_pelajaran,
 'Status': item.status,
 'NISN/NIP': item.nisn || item.nip
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Rekap Absensi');
 XLSX.writeFile(wb, `Rekap_Absensi_${currentYear.replace('/', '-')}.xlsx`);
 }
 function exportStudentData(filterClass = null) {
 let students = currentData.filter(item => item.type === 'student');
 
 if (filterClass) {
 students = students.filter(item => item.kelas === filterClass);
 }
 if (students.length === 0) {
 showToast('Tidak ada data siswa untuk diekspor.', 'error');
 return;
 }
 const exportData = students.map(item => ({
 'Nama Lengkap': item.nama,
 'NISN': item.nisn,
 'Kelas': item.kelas,
 'Jenis Kelamin': item.jenis_kelamin,
 'Tempat Lahir': item.tempat_lahir,
 'Tanggal Lahir': item.tanggal_lahir,
 'Alamat': item.alamat,
 'No HP': item.no_hp
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Data Siswa');
 const filename = filterClass ? 
 `Data_Siswa_${filterClass.replace(/\s+/g, '_')}_${currentYear.replace('/', '-
')}.xlsx` :
 `Data_Siswa_${currentYear.replace('/', '-')}.xlsx`;
 XLSX.writeFile(wb, filename);
 }
 function exportTeacherData() {
 const teachers = currentData.filter(item => item.type === 'teacher');
 
 if (teachers.length === 0) {
 showToast('Tidak ada data guru untuk diekspor.', 'error');
 return;
 }
 const exportData = teachers.map(item => ({
 'Nama Lengkap': item.nama,
 'NIP': item.nip,
 'Mata Pelajaran': item.mata_pelajaran,
 'Jenis Kelamin': item.jenis_kelamin,
 'Tempat Lahir': item.tempat_lahir,
 'Tanggal Lahir': item.tanggal_lahir,
 'Alamat': item.alamat,
 'No HP': item.no_hp
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Data Guru');
 XLSX.writeFile(wb, `Data_Guru_${currentYear.replace('/', '-')}.xlsx`);
 }
 function exportAttendanceRange() {
 const dateFrom = document.getElementById('export-date-from').value;
 const dateTo = document.getElementById('export-date-to').value;
 
 if (!dateFrom || !dateTo) {
 showToast('Pilih rentang tanggal terlebih dahulu!', 'error');
 return;
 }
 const attendanceData = currentData.filter(item => {
 if (item.type !== 'attendance') return false;
 return item.tanggal >= dateFrom && item.tanggal <= dateTo;
 });
 if (attendanceData.length === 0) {
 showToast('Tidak ada data absensi pada rentang tanggal tersebut.', 
'error');
 return;
 }
 const exportData = attendanceData.map(item => ({
 'Tanggal': item.tanggal,
 'Waktu': item.waktu,
 'Nama': item.nama,
 'Role': item.role,
 'Kelas/Mata Pelajaran': item.kelas || item.mata_pelajaran,
 'Status': item.status,
 'NISN/NIP': item.nisn || item.nip
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Rekap Absensi');
 XLSX.writeFile(wb, `Rekap_Absensi_${dateFrom}_${dateTo}.xlsx`);
 }
 function exportIndividualData() {
 const personId = document.getElementById('export-individual-person').value;
 
 if (!personId) {
 showToast('Pilih siswa/guru terlebih dahulu!', 'error');
 return;
 }
 const person = currentData.find(item => item.id === personId);
 const attendanceData = currentData.filter(item => 
 item.type === 'attendance' && item.nama === person.nama
 );
 if (attendanceData.length === 0) {
 showToast('Tidak ada data absensi untuk orang tersebut.', 'error');
 return;
 }
 const exportData = attendanceData.map(item => ({
 'Tanggal': item.tanggal,
 'Waktu': item.waktu,
 'Status': item.status
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Rekap Individual');
 XLSX.writeFile(wb, `Rekap_${person.nama.replace(/\s+/g, 
'_')}_${currentYear.replace('/', '-')}.xlsx`);
 }
 // Promotion and repeat functionality
 document.getElementById('promote-form').addEventListener('submit', async (e) 
=> {
 e.preventDefault();
 const fromClass = document.getElementById('promote-from').value;
 const toClass = document.getElementById('promote-to').value;
 
 if (!fromClass || !toClass) {
 showToast("Pilih kelas asal dan tujuan!", "error");
 return;
 }
 const studentsToPromote = currentData.filter(item => 
 item.type === 'student' && item.kelas === fromClass
 );
 for (const student of studentsToPromote) {
 const updatedStudent = { ...student, kelas: toClass };
 if (window.dataSdk) {
 await window.dataSdk.update(updatedStudent);
 }
 }
 showToast(`${studentsToPromote.length} siswa berhasil naik dari 
${fromClass} ke ${toClass}!`, "success");
 e.target.reset();
 });
 document.getElementById('repeat-form').addEventListener('submit', async (e) 
=> {
 e.preventDefault();
 const studentId = document.getElementById('repeat-student').value;
 const reason = document.getElementById('repeat-reason').value;
 
 if (!studentId || !reason) {
 showToast("Pilih siswa dan masukkan alasan!", "error");
 return;
 }
 showToast("Siswa berhasil diproses untuk tinggal kelas.", "success");
 e.target.reset();
 });
 async function deleteAttendance(id) {
 const item = currentData.find(item => item.id === id);
 if (!item) return;
 if (window.dataSdk) {
 const result = await window.dataSdk.delete(item);
 if (result.isOk) {
 showToast("Data absensi berhasil dihapus!", "success");
 } else {
 showToast("Gagal menghapus data absensi.", "error");
 }
 }
 }
 async function deleteStudent(id) {
 const item = currentData.find(item => item.id === id);
 if (!item) return;
 if (window.dataSdk) {
 const result = await window.dataSdk.delete(item);
 if (result.isOk) {
 showToast("Data siswa berhasil dihapus!", "success");
 } else {
 showToast("Gagal menghapus data siswa.", "error");
 }
 }
 }
 async function deleteTeacher(id) {
 const item = currentData.find(item => item.id === id);
 if (!item) return;
 if (window.dataSdk) {
 const result = await window.dataSdk.delete(item);
 if (result.isOk) {
 showToast("Data guru berhasil dihapus!", "success");
 } else {
 showToast("Gagal menghapus data guru.", "error");
 }
 }
 }
 // Attendance mode functions
 function switchAttendanceMode(mode) {
 currentAttendanceMode = mode;
 
 // Update mode buttons
 document.querySelectorAll('.mode-btn').forEach(btn => {
 btn.classList.remove('border-green-500', 'bg-green-50', 'text-green-700');
 btn.classList.add('border-gray-300', 'text-gray-600');
 });
 
 if (mode === 'individual') {
 document.getElementById('mode-individual').classList.add('border-green-
500', 'bg-green-50', 'text-green-700');
 document.getElementById('mode-individual').classList.remove('border￾gray-300', 'text-gray-600');
 document.getElementById('individual-mode').classList.remove('hidden');
 document.getElementById('class-mode').classList.add('hidden');
 } else {
 document.getElementById('mode-class').classList.add('border-green-500', 
'bg-green-50', 'text-green-700');
 document.getElementById('mode-class').classList.remove('border-gray-
300', 'text-gray-600');
 document.getElementById('individual-mode').classList.add('hidden');
 document.getElementById('class-mode').classList.remove('hidden');
 }
 }
 function handleClassSelection(e) {
 selectedClass = e.target.value;
 
 if (!selectedClass) {
 document.getElementById('class-attendance￾container').classList.add('hidden');
 return;
 }
 // Get students for selected class
 classStudents = currentData.filter(item => 
 item.type === 'student' && item.kelas === selectedClass
 ).sort((a, b) => a.nama.localeCompare(b.nama));
 if (classStudents.length === 0) {
 document.getElementById('class-attendance￾container').classList.add('hidden');
 showToast('Tidak ada siswa di kelas ini. Tambahkan siswa terlebih 
dahulu.', 'error');
 return;
 }
 renderClassStudentList();
 document.getElementById('class-attendance￾container').classList.remove('hidden');
 }
 function renderClassStudentList() {
 const container = document.getElementById('class-student-list');
 
 container.innerHTML = classStudents.map(student => {
 const photoDisplay = student.foto_url ? 
 `<img src="${student.foto_url}" class="w-12 h-12 object-cover rounded￾full" alt="Foto ${student.nama}">` :
 `<div class="w-12 h-12 bg-gray-200 rounded-full flex items-center 
justify-center text-lg">${student.jenis_kelamin === 'Perempuan' ? '👩🎓' : 
'👨🎓'}</div>`;
 return `
 <div class="flex items-center justify-between p-4 border rounded-lg 
hover:bg-gray-50 transition duration-200" data-student-id="${student.id}">
 <div class="flex items-center space-x-3">
 ${photoDisplay}
 <div>
 <h4 class="font-semibold text-gray-900">${student.nama}</h4>
 <p class="text-sm text-gray-600">NISN: ${student.nisn}</p>
 </div>
 </div>
 <div class="flex space-x-2">
 <button class="attendance-btn px-3 py-1 rounded-full text-sm font￾medium transition duration-200 bg-green-100 text-green-800 border-2 border-green-
500" data-status="Hadir">
 Hadir
 </button>
 <button class="attendance-btn px-3 py-1 rounded-full text-sm font￾medium transition duration-200 bg-gray-100 text-gray-600 border-2 border-gray-300" 
data-status="Izin">
 Izin
 </button>
 <button class="attendance-btn px-3 py-1 rounded-full text-sm font￾medium transition duration-200 bg-gray-100 text-gray-600 border-2 border-gray-300" 
data-status="Sakit">
 Sakit
 </button>
 <button class="attendance-btn px-3 py-1 rounded-full text-sm font￾medium transition duration-200 bg-gray-100 text-gray-600 border-2 border-gray-300" 
data-status="Alfa">
 Alfa
 </button>
 </div>
 </div>
 `;
 }).join('');
 // Add event listeners to attendance buttons
 container.querySelectorAll('.attendance-btn').forEach(btn => {
 btn.addEventListener('click', (e) => {
 const studentRow = e.target.closest('[data-student-id]');
 const buttons = studentRow.querySelectorAll('.attendance-btn');
 const status = e.target.dataset.status;
 
 // Reset all buttons in this row
 buttons.forEach(button => {
 button.classList.remove('bg-green-100', 'text-green-800', 'border￾green-500');
 button.classList.remove('bg-yellow-100', 'text-yellow-800', 'border￾yellow-500');
 button.classList.remove('bg-blue-100', 'text-blue-800', 'border-blue-
500');
 button.classList.remove('bg-red-100', 'text-red-800', 'border-red-500');
 button.classList.add('bg-gray-100', 'text-gray-600', 'border-gray-300');
 });
 
 // Style selected button
 const colors = {
 'Hadir': ['bg-green-100', 'text-green-800', 'border-green-500'],
 'Izin': ['bg-yellow-100', 'text-yellow-800', 'border-yellow-500'],
 'Sakit': ['bg-blue-100', 'text-blue-800', 'border-blue-500'],
 'Alfa': ['bg-red-100', 'text-red-800', 'border-red-500']
 };
 
 e.target.classList.remove('bg-gray-100', 'text-gray-600', 'border-gray-
300');
 e.target.classList.add(...colors[status]);
 
 // Store selection
 studentRow.dataset.selectedStatus = status;
 });
 });
 }
 function markAllPresent() {
 const container = document.getElementById('class-student-list');
 const hadirButtons = container.querySelectorAll('[data-status="Hadir"]');
 
 hadirButtons.forEach(btn => {
 btn.click();
 });
 }
 function resetClassAttendance() {
 const container = document.getElementById('class-student-list');
 const allButtons = container.querySelectorAll('.attendance-btn');
 const studentRows = container.querySelectorAll('[data-student-id]');
 
 // Reset all button styles
 allButtons.forEach(button => {
 button.classList.remove('bg-green-100', 'text-green-800', 'border-green-
500');
 button.classList.remove('bg-yellow-100', 'text-yellow-800', 'border-yellow-
500');
 button.classList.remove('bg-blue-100', 'text-blue-800', 'border-blue-500');
 button.classList.remove('bg-red-100', 'text-red-800', 'border-red-500');
 button.classList.add('bg-gray-100', 'text-gray-600', 'border-gray-300');
 });
 
 // Clear selections
 studentRows.forEach(row => {
 delete row.dataset.selectedStatus;
 });
 }
 async function saveClassAttendance() {
 const container = document.getElementById('class-student-list');
 const studentRows = container.querySelectorAll('[data-student-id]');
 const attendanceData = [];
 
 // Collect attendance data
 studentRows.forEach(row => {
 const studentId = row.dataset.studentId;
 const selectedStatus = row.dataset.selectedStatus;
 
 if (selectedStatus) {
 const student = classStudents.find(s => s.id === studentId);
 if (student) {
 attendanceData.push({
 id: `attendance_${Date.now()}_${studentId}`,
 nama: student.nama,
 nisn: student.nisn,
 nip: '',
 role: 'Siswa',
 kelas: student.kelas,
 mata_pelajaran: '',
 tanggal: new Date().toISOString().split('T')[0],
 status: selectedStatus,
 waktu: new Date().toLocaleTimeString('id-ID'),
 foto_url: student.foto_url || '',
 tahun_ajaran: currentYear,
 type: 'attendance',
 jenis_kelamin: student.jenis_kelamin || '',
 tempat_lahir: '',
 tanggal_lahir: '',
 alamat: '',
 no_hp: ''
 });
 }
 }
 });
 
 if (attendanceData.length === 0) {
 showToast('Pilih status kehadiran untuk minimal satu siswa!', 'error');
 return;
 }
 if (currentData.length + attendanceData.length > 999) {
 showToast('Batas maksimum 999 data akan terlampaui. Kurangi jumlah 
data atau hapus data lama.', 'error');
 return;
 }
 // Set loading state
 const saveBtn = document.getElementById('save-class-attendance');
 const saveText = document.getElementById('save-class-text');
 const saveLoading = document.getElementById('save-class-loading');
 
 saveBtn.disabled = true;
 saveText.textContent = 'Menyimpan...';
 saveLoading.classList.remove('hidden');
 saveBtn.classList.add('opacity-50');
 try {
 // Save all attendance data
 for (const data of attendanceData) {
 if (window.dataSdk) {
 const result = await window.dataSdk.create(data);
 if (!result.isOk) {
 throw new Error('Failed to save attendance data');
 }
 }
 }
 showToast(`Absensi ${attendanceData.length} siswa berhasil disimpan!`, 
'success');
 resetClassAttendance();
 switchTab('rekap');
 
 } catch (error) {
 showToast('Gagal menyimpan data absensi. Silakan coba lagi.', 'error');
 } finally {
 // Reset loading state
 saveBtn.disabled = false;
 saveText.textContent = 'Simpan Absensi Kelas';
 saveLoading.classList.add('hidden');
 saveBtn.classList.remove('opacity-50');
 }
 }
 // Meeting functionality
 document.getElementById('rapat-guru').addEventListener('click', () => 
switchMeetingType('Rapat Guru'));
 document.getElementById('rapat-staf').addEventListener('click', () => 
switchMeetingType('Rapat Staf'));
 document.getElementById('create-meeting-form').addEventListener('submit', 
createMeeting);
 document.getElementById('filter-meeting-type').addEventListener('change', 
renderMeetingList);
 document.getElementById('close-meeting-modal').addEventListener('click', 
closeMeetingModal);
 document.getElementById('mark-all-present-meeting').addEventListener('click', 
markAllPresentMeeting);
 document.getElementById('save-meeting-attendance').addEventListener('click', 
saveMeetingAttendance);
 document.getElementById('save-minutes').addEventListener('click', 
saveMinutes);
 document.getElementById('export-minutes').addEventListener('click', 
exportMinutes);
 
 // Meeting attendance filters
 document.getElementById('filter-rapat-type').addEventListener('change', 
renderMeetingAttendanceListView);
 document.getElementById('filter-rapat-status').addEventListener('change',
renderMeetingAttendanceListView);
 document.getElementById('filter-rapat-date').addEventListener('change', 
renderMeetingAttendanceListView);
 document.getElementById('export-meeting-attendance￾btn').addEventListener('click', exportMeetingAttendanceData);
 function switchMeetingType(type) {
 currentMeetingType = type;
 
 // Update meeting type buttons
 document.querySelectorAll('.rapat-type-btn').forEach(btn => {
 btn.classList.remove('border-green-500', 'bg-green-50', 'text-green-700');
 btn.classList.add('border-gray-300', 'text-gray-600');
 });
 
 if (type === 'Rapat Guru') {
 document.getElementById('rapat-guru').classList.add('border-green-500', 
'bg-green-50', 'text-green-700');
 document.getElementById('rapat-guru').classList.remove('border-gray-
300', 'text-gray-600');
 } else {
 document.getElementById('rapat-staf').classList.add('border-green-500', 
'bg-green-50', 'text-green-700');
 document.getElementById('rapat-staf').classList.remove('border-gray-300', 
'text-gray-600');
 }
 }
 async function createMeeting(e) {
 e.preventDefault();
 
 if (currentData.length >= 999) {
 showToast("Batas maksimum 999 data telah tercapai.", "error");
 return;
 }
 const formData = new FormData(e.target);
 const meetingData = {
 id: `meeting_${Date.now()}`,
 nama: formData.get('title'),
 nisn: '',
 nip: '',
 role: currentMeetingType,
 kelas: '',
 mata_pelajaran: '',
 tanggal: formData.get('date'),
 status: 'Scheduled',
 waktu: formData.get('time'),
 foto_url: '',
 tahun_ajaran: currentYear,
 type: 'meeting',
 jenis_kelamin: '',
 tempat_lahir: formData.get('location'),
 tanggal_lahir: '',
 alamat: formData.get('agenda'),
 no_hp: ''
 };
 // Set loading state
 const createBtn = document.getElementById('create-meeting-btn');
 const createText = document.getElementById('create-meeting-text');
 const createLoading = document.getElementById('create-meeting-loading');
 
 createBtn.disabled = true;
 createText.textContent = 'Membuat Rapat...';
 createLoading.classList.remove('hidden');
 createBtn.classList.add('opacity-50');
 try {
 if (window.dataSdk) {
 const result = await window.dataSdk.create(meetingData);
 if (result.isOk) {
 e.target.reset();
 showToast("Rapat berhasil dibuat!", "success");
 } else {
 showToast("Gagal membuat rapat.", "error");
 }
 }
 } finally {
 createBtn.disabled = false;
 createText.textContent = 'Buat Rapat';
 createLoading.classList.add('hidden');
 createBtn.classList.remove('opacity-50');
 }
 }
 function renderMeetingList() {
 const container = document.getElementById('meeting-list');
 const filterType = document.getElementById('filter-meeting-type').value;
 let meetings = currentData.filter(item => {
 if (item.type !== 'meeting') return false;
 if (filterType && item.role !== filterType) return false;
 return true;
 });
 // Sort by date (newest first)
 meetings.sort((a, b) => new Date(b.tanggal + ' ' + b.waktu) - new 
Date(a.tanggal + ' ' + a.waktu));
 if (meetings.length === 0) {
 container.innerHTML = '<div class="p-6 text-center text-gray-500">Tidak 
ada rapat yang sesuai dengan filter.</div>';
 return;
 }
 container.innerHTML = meetings.map(meeting => {
 const statusColors = {
 'Scheduled': 'bg-blue-100 text-blue-800',
 'Ongoing': 'bg-yellow-100 text-yellow-800',
 'Completed': 'bg-green-100 text-green-800',
 'Cancelled': 'bg-red-100 text-red-800'
 };
 const typeColors = {
 'Rapat Guru': 'text-green-600',
 'Rapat Staf': 'text-blue-600'
 };
 return `
 <div class="border rounded-lg p-4 hover:bg-gray-50 transition duration-
200 cursor-pointer" onclick="openMeetingDetail('${meeting.id}')">
 <div class="flex items-center justify-between">
 <div class="flex-1">
 <div class="flex items-center space-x-2 mb-2">
 <h4 class="font-semibold text-gray-
900">${meeting.nama}</h4>
 <span class="px-2 py-1 rounded-full text-xs font-medium 
${statusColors[meeting.status]}">${meeting.status}</span>
 </div>
 <p class="text-sm ${typeColors[meeting.role]} font￾medium">${meeting.role}</p>
 <p class="text-sm text-gray-600">📅 ${meeting.tanggal} • ⏰
${meeting.waktu}</p>
 <p class="text-sm text-gray-600">📍 ${meeting.tempat_lahir}</p>
 <p class="text-xs text-gray-500 mt-2 line-clamp-
2">${meeting.alamat}</p>
 </div>
 <div class="flex items-center space-x-2">
 <button onclick="event.stopPropagation(); 
deleteMeeting('${meeting.id}')" class="text-red-500 hover:text-red-700 transition 
duration-200">
 <svg class="w-5 h-5" fill="none" stroke="currentColor" 
viewBox="0 0 24 24">
 <path stroke-linecap="round" stroke-linejoin="round" 
stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-
1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
 </svg>
 </button>
 </div>
 </div>
 </div>
 `;
 }).join('');
 }
 function openMeetingDetail(meetingId) {
 currentMeeting = currentData.find(item => item.id === meetingId);
 if (!currentMeeting) return;
 // Populate meeting info
 document.getElementById('modal-meeting-title').textContent = 
currentMeeting.nama;
 document.getElementById('meeting-info').innerHTML = `
 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
 <div>
 <h5 class="font-semibold text-gray-700">Jenis Rapat</h5>
 <p class="text-gray-600">${currentMeeting.role}</p>
 </div>
 <div>
 <h5 class="font-semibold text-gray-700">Tanggal & Waktu</h5>
 <p class="text-gray-600">${currentMeeting.tanggal} • 
${currentMeeting.waktu}</p>
 </div>
 <div>
 <h5 class="font-semibold text-gray-700">Tempat</h5>
 <p class="text-gray-600">${currentMeeting.tempat_lahir}</p>
 </div>
 <div>
 <h5 class="font-semibold text-gray-700">Status</h5>
 <p class="text-gray-600">${currentMeeting.status}</p>
 </div>
 <div class="md:col-span-2">
 <h5 class="font-semibold text-gray-700">Agenda</h5>
 <div class="text-gray-600 whitespace-pre￾line">${currentMeeting.alamat}</div>
 </div>
 </div>
 `;
 // Load existing minutes if available
 const existingMinutes = currentData.find(item => 
 item.type === 'minutes' && item.alamat === meetingId
 );
 
 if (existingMinutes) {
 document.getElementById('meeting-minutes').value = 
existingMinutes.nama || '';
 document.getElementById('meeting-decisions').value = 
existingMinutes.tempat_lahir || '';
 document.getElementById('meeting-followup').value = 
existingMinutes.no_hp || '';
 } else {
 document.getElementById('meeting-minutes').value = '';
 document.getElementById('meeting-decisions').value = '';
 document.getElementById('meeting-followup').value = '';
 }
 // Populate attendance list
 renderMeetingAttendanceList();
 
 document.getElementById('meeting-detail-modal').classList.remove('hidden');
 }
 function renderMeetingAttendanceList() {
 const container = document.getElementById('meeting-attendance-list');
 
 // Get participants based on meeting type
 let participants = [];
 if (currentMeeting.role === 'Rapat Guru') {
 participants = currentData.filter(item => item.type === 'teacher');
 } else if (currentMeeting.role === 'Rapat Staf') {
 // For staff meetings, include both teachers and admin staff
 participants = currentData.filter(item => item.type === 'teacher');
 }
 if (participants.length === 0) {
 container.innerHTML = '<div class="p-4 text-center text-gray-500">Tidak 
ada peserta yang tersedia.</div>';
 return;
 }
 container.innerHTML = participants.map(participant => {
 const photoDisplay = participant.foto_url ? 
 `<img src="${participant.foto_url}" class="w-10 h-10 object-cover 
rounded-full" alt="Foto ${participant.nama}">` :
 `<div class="w-10 h-10 bg-gray-200 rounded-full flex items-center 
justify-center text-sm">${participant.jenis_kelamin === 'Perempuan' ? '👩🏫' : 
'👨🏫'}</div>`;
 return `
 <div class="flex items-center justify-between p-3 border rounded-lg 
hover:bg-gray-50 transition duration-200" data-participant-id="${participant.id}">
 <div class="flex items-center space-x-3">
 ${photoDisplay}
 <div>
 <h5 class="font-semibold text-gray-
900">${participant.nama}</h5>
 <p class="text-sm text-gray-
600">${participant.mata_pelajaran}</p>
 </div>
 </div>
 <div class="flex space-x-2">
 <button class="meeting-attendance-btn px-3 py-1 rounded-full text￾sm font-medium transition duration-200 bg-green-100 text-green-800 border-2 
border-green-500" data-status="Hadir">
 Hadir
 </button>
 <button class="meeting-attendance-btn px-3 py-1 rounded-full text￾sm font-medium transition duration-200 bg-gray-100 text-gray-600 border-2 border￾gray-300" data-status="Tidak Hadir">
 Tidak Hadir
 </button>
 </div>
 </div>
 `;
 }).join('');
 // Add event listeners to attendance buttons
 container.querySelectorAll('.meeting-attendance-btn').forEach(btn => {
 btn.addEventListener('click', (e) => {
 const participantRow = e.target.closest('[data-participant-id]');
 const buttons = participantRow.querySelectorAll('.meeting-attendance￾btn');
 const status = e.target.dataset.status;
 
 // Reset all buttons in this row
 buttons.forEach(button => {
 button.classList.remove('bg-green-100', 'text-green-800', 'border￾green-500');
 button.classList.remove('bg-red-100', 'text-red-800', 'border-red-500');
 button.classList.add('bg-gray-100', 'text-gray-600', 'border-gray-300');
 });
 
 // Style selected button
 if (status === 'Hadir') {
 e.target.classList.remove('bg-gray-100', 'text-gray-600', 'border-gray-
300');
 e.target.classList.add('bg-green-100', 'text-green-800', 'border-green-
500');
 } else {
 e.target.classList.remove('bg-gray-100', 'text-gray-600', 'border-gray-
300');
 e.target.classList.add('bg-red-100', 'text-red-800', 'border-red-500');
 }
 
 // Store selection
 participantRow.dataset.selectedStatus = status;
 });
 });
 }
 function markAllPresentMeeting() {
 const container = document.getElementById('meeting-attendance-list');
 const hadirButtons = container.querySelectorAll('[data-status="Hadir"]');
 
 hadirButtons.forEach(btn => {
 btn.click();
 });
 }
 async function saveMeetingAttendance() {
 const container = document.getElementById('meeting-attendance-list');
 const participantRows = container.querySelectorAll('[data-participant-id]');
 const attendanceData = [];
 
 // Collect attendance data
 participantRows.forEach(row => {
 const participantId = row.dataset.participantId;
 const selectedStatus = row.dataset.selectedStatus;
 
 if (selectedStatus) {
 const participant = currentData.find(p => p.id === participantId);
 if (participant) {
 attendanceData.push({
 id: `meeting_attendance_${Date.now()}_${participantId}`,
 nama: participant.nama,
 nisn: '',
 nip: participant.nip,
 role: 'Peserta Rapat',
 kelas: currentMeeting.nama,
 mata_pelajaran: participant.mata_pelajaran,
 tanggal: currentMeeting.tanggal,
 status: selectedStatus,
 waktu: currentMeeting.waktu,
 foto_url: participant.foto_url || '',
 tahun_ajaran: currentYear,
 type: 'meeting_attendance',
 jenis_kelamin: participant.jenis_kelamin || '',
 tempat_lahir: currentMeeting.tempat_lahir,
 tanggal_lahir: '',
 alamat: currentMeeting.id,
 no_hp: currentMeeting.role
 });
 }
 }
 });
 
 if (attendanceData.length === 0) {
 showToast('Pilih status kehadiran untuk minimal satu peserta!', 'error');
 return;
 }
 // Set loading state
 const saveBtn = document.getElementById('save-meeting-attendance');
 const saveText = document.getElementById('save-meeting-attendance-text');
 const saveLoading = document.getElementById('save-meeting-attendance￾loading');
 
 saveBtn.disabled = true;
 saveText.textContent = 'Menyimpan...';
 saveLoading.classList.remove('hidden');
 saveBtn.classList.add('opacity-50');
 try {
 // Save all attendance data
 for (const data of attendanceData) {
 if (window.dataSdk) {
 const result = await window.dataSdk.create(data);
 if (!result.isOk) {
 throw new Error('Failed to save meeting attendance');
 }
 }
 }
 showToast(`Absensi ${attendanceData.length} peserta berhasil disimpan!`, 
'success');
 
 } catch (error) {
 showToast('Gagal menyimpan absensi rapat.', 'error');
 } finally {
 // Reset loading state
 saveBtn.disabled = false;
 saveText.textContent = 'Simpan Absensi';
 saveLoading.classList.add('hidden');
 saveBtn.classList.remove('opacity-50');
 }
 }
 async function saveMinutes() {
 const minutes = document.getElementById('meeting-minutes').value;
 const decisions = document.getElementById('meeting-decisions').value;
 const followup = document.getElementById('meeting-followup').value;
 if (!minutes.trim()) {
 showToast('Masukkan isi notulen terlebih dahulu!', 'error');
 return;
 }
 // Set loading state
 const saveBtn = document.getElementById('save-minutes');
 const saveText = document.getElementById('save-minutes-text');
 const saveLoading = document.getElementById('save-minutes-loading');
 
 saveBtn.disabled = true;
 saveText.textContent = 'Menyimpan...';
 saveLoading.classList.remove('hidden');
 saveBtn.classList.add('opacity-50');
 try {
 // Check if minutes already exist
 const existingMinutes = currentData.find(item => 
 item.type === 'minutes' && item.alamat === currentMeeting.id
 );
 const minutesData = {
 id: existingMinutes ? existingMinutes.id : `minutes_${Date.now()}`,
 nama: minutes,
 nisn: '',
 nip: '',
 role: 'Notulen',
 kelas: currentMeeting.nama,
 mata_pelajaran: '',
 tanggal: currentMeeting.tanggal,
 status: 'Completed',
 waktu: currentMeeting.waktu,
 foto_url: '',
 tahun_ajaran: currentYear,
 type: 'minutes',
 jenis_kelamin: '',
 tempat_lahir: decisions,
 tanggal_lahir: '',
 alamat: currentMeeting.id,
 no_hp: followup
 };
 if (window.dataSdk) {
 const result = existingMinutes ? 
 await window.dataSdk.update(minutesData) :
 await window.dataSdk.create(minutesData);
 
 if (result.isOk) {
 showToast('Notulen berhasil disimpan!', 'success');
 } else {
 showToast('Gagal menyimpan notulen.', 'error');
 }
 }
 } finally {
 saveBtn.disabled = false;
 saveText.textContent = 'Simpan Notulen';
 saveLoading.classList.add('hidden');
 saveBtn.classList.remove('opacity-50');
 }
 }
 function exportMinutes() {
 if (!currentMeeting) return;
 const minutes = document.getElementById('meeting-minutes').value;
 const decisions = document.getElementById('meeting-decisions').value;
 const followup = document.getElementById('meeting-followup').value;
 // Get attendance data for this meeting
 const attendanceData = currentData.filter(item => 
 item.type === 'meeting_attendance' && item.alamat === currentMeeting.id
 );
 const attendanceList = attendanceData.map(item => ({
 'Nama': item.nama,
 'Mata Pelajaran': item.mata_pelajaran,
 'Status': item.status
 }));
 // Create workbook with multiple sheets
 const wb = XLSX.utils.book_new();
 // Meeting info sheet
 const meetingInfo = [
 ['NOTULEN RAPAT'],
 [''],
 ['Judul Rapat', currentMeeting.nama],
 ['Jenis Rapat', currentMeeting.role],
 ['Tanggal', currentMeeting.tanggal],
 ['Waktu', currentMeeting.waktu],
 ['Tempat', currentMeeting.tempat_lahir],
 [''],
 ['AGENDA RAPAT'],
 ...currentMeeting.alamat.split('\n').map(line => [line]),
 [''],
 ['ISI NOTULEN'],
 ...minutes.split('\n').map(line => [line]),
 [''],
 ['KEPUTUSAN RAPAT'],
 ...decisions.split('\n').map(line => [line]),
 [''],
 ['TINDAK LANJUT'],
 ...followup.split('\n').map(line => [line])
 ];
 const ws1 = XLSX.utils.aoa_to_sheet(meetingInfo);
 XLSX.utils.book_append_sheet(wb, ws1, 'Notulen');
 // Attendance sheet
 if (attendanceList.length > 0) {
 const ws2 = XLSX.utils.json_to_sheet(attendanceList);
 XLSX.utils.book_append_sheet(wb, ws2, 'Daftar Hadir');
 }
 const filename = `Notulen_${currentMeeting.nama.replace(/\s+/g, 
'_')}_${currentMeeting.tanggal}.xlsx`;
 XLSX.writeFile(wb, filename);
 }
 function closeMeetingModal() {
 document.getElementById('meeting-detail-modal').classList.add('hidden');
 currentMeeting = null;
 }
 async function deleteMeeting(id) {
 const item = currentData.find(item => item.id === id);
 if (!item) return;
 if (window.dataSdk) {
 const result = await window.dataSdk.delete(item);
 if (result.isOk) {
 showToast("Rapat berhasil dihapus!", "success");
 } else {
 showToast("Gagal menghapus rapat.", "error");
 }
 }
 }
 // Meeting attendance statistics and rendering functions
 function updateMeetingAttendanceStatistics() {
 const meetingAttendanceData = currentData.filter(item => item.type === 
'meeting_attendance');
 const meetings = currentData.filter(item => item.type === 'meeting');
 
 const stats = {
 hadir: meetingAttendanceData.filter(item => item.status === 'Hadir').length,
 tidakHadir: meetingAttendanceData.filter(item => item.status === 'Tidak 
Hadir').length,
 totalRapat: meetings.length,
 pesertaAktif: new Set(meetingAttendanceData.map(item => 
item.nama)).size
 };
 document.getElementById('count-rapat-hadir').textContent = stats.hadir;
 document.getElementById('count-rapat-tidak-hadir').textContent = 
stats.tidakHadir;
 document.getElementById('count-total-rapat').textContent = stats.totalRapat;
 document.getElementById('count-peserta-aktif').textContent = 
stats.pesertaAktif;
 }
 function renderMeetingAttendanceListView() {
 const container = document.getElementById('meeting-attendance-list-view');
 const filterType = document.getElementById('filter-rapat-type').value;
 const filterStatus = document.getElementById('filter-rapat-status').value;
 const filterDate = document.getElementById('filter-rapat-date').value;
 let filteredData = currentData.filter(item => {
 if (item.type !== 'meeting_attendance') return false;
 if (filterType && item.no_hp !== filterType) return false;
 if (filterStatus && item.status !== filterStatus) return false;
 if (filterDate && item.tanggal !== filterDate) return false;
 return true;
 });
 // Sort by newest first
 filteredData.sort((a, b) => new Date(b.tanggal + ' ' + b.waktu) - new 
Date(a.tanggal + ' ' + a.waktu));
 if (filteredData.length === 0) {
 container.innerHTML = '<div class="p-6 text-center text-gray-500">Tidak 
ada data kehadiran rapat yang sesuai dengan filter.</div>';
 return;
 }
 container.innerHTML = filteredData.map(item => {
 const statusColors = {
 'Hadir': 'bg-green-100 text-green-800',
 'Tidak Hadir': 'bg-red-100 text-red-800'
 };
 const typeColors = {
 'Rapat Guru': 'text-green-600',
 'Rapat Staf': 'text-blue-600'
 };
 const photoDisplay = item.foto_url ? 
 `<img src="${item.foto_url}" class="photo-preview" alt="Foto 
${item.nama}">` :
 `<div class="w-16 h-16 bg-gray-200 rounded-full flex items-center 
justify-center text-2xl">${item.jenis_kelamin === 'Perempuan' ? '👩🏫' : 
'👨🏫'}</div>`;
 return `
 <div class="p-4 hover:bg-gray-50 transition duration-200">
 <div class="flex items-center justify-between">
 <div class="flex items-center space-x-4">
 ${photoDisplay}
 <div>
 <h4 class="font-semibold text-gray-900">${item.nama}</h4>
 <p class="text-sm ${typeColors[item.no_hp]} font￾medium">${item.no_hp}</p>
 <p class="text-sm text-gray-600">${item.kelas}</p>
 <p class="text-sm text-gray-600">📍 ${item.tempat_lahir}</p>
 <p class="text-xs text-gray-500">${item.tanggal} • 
${item.waktu}</p>
 </div>
 </div>
 <div class="flex items-center space-x-3">
 <span class="px-3 py-1 rounded-full text-xs font-medium 
${statusColors[item.status]}">${item.status}</span>
 <button onclick="deleteMeetingAttendance('${item.id}')" 
class="text-red-500 hover:text-red-700 transition duration-200">
 <svg class="w-5 h-5" fill="none" stroke="currentColor" 
viewBox="0 0 24 24">
 <path stroke-linecap="round" stroke-linejoin="round" 
stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-
1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
 </svg>
 </button>
 </div>
 </div>
 </div>
 `;
 }).join('');
 }
 function renderParticipantSummary() {
 const container = document.getElementById('participant-summary');
 const meetingAttendanceData = currentData.filter(item => item.type === 
'meeting_attendance');
 
 // Group by participant
 const participantStats = {};
 meetingAttendanceData.forEach(item => {
 if (!participantStats[item.nama]) {
 participantStats[item.nama] = {
 nama: item.nama,
 mata_pelajaran: item.mata_pelajaran,
 foto_url: item.foto_url,
 jenis_kelamin: item.jenis_kelamin,
 totalRapat: 0,
 hadir: 0,
 tidakHadir: 0
 };
 }
 
 participantStats[item.nama].totalRapat++;
 if (item.status === 'Hadir') {
 participantStats[item.nama].hadir++;
 } else {
 participantStats[item.nama].tidakHadir++;
 }
 });
 const participants = Object.values(participantStats);
 
 if (participants.length === 0) {
 container.innerHTML = '<div class="p-4 text-center text-gray-500">Belum 
ada data peserta rapat.</div>';
 return;
 }
 // Sort by attendance rate
 participants.sort((a, b) => (b.hadir / b.totalRapat) - (a.hadir / a.totalRapat));
 container.innerHTML = participants.map(participant => {
 const attendanceRate = ((participant.hadir / participant.totalRapat) * 
100).toFixed(1);
 const photoDisplay = participant.foto_url ? 
 `<img src="${participant.foto_url}" class="w-12 h-12 object-cover 
rounded-full" alt="Foto ${participant.nama}">` :
 `<div class="w-12 h-12 bg-gray-200 rounded-full flex items-center 
justify-center text-lg">${participant.jenis_kelamin === 'Perempuan' ? '👩🏫' : 
'👨🏫'}</div>`;
 return `
 <div class="border rounded-lg p-4 hover:bg-gray-50 transition duration-
200">
 <div class="flex items-center justify-between">
 <div class="flex items-center space-x-3">
 ${photoDisplay}
 <div>
 <h5 class="font-semibold text-gray-
900">${participant.nama}</h5>
 <p class="text-sm text-gray-
600">${participant.mata_pelajaran}</p>
 </div>
 </div>
 <div class="text-right">
 <div class="text-lg font-bold text-green-
600">${attendanceRate}%</div>
 <div class="text-xs text-gray-500">
 ${participant.hadir}/${participant.totalRapat} rapat
 </div>
 <div class="flex space-x-2 mt-1">
 <span class="px-2 py-1 bg-green-100 text-green-800 text-xs 
rounded">${participant.hadir} Hadir</span>
 <span class="px-2 py-1 bg-red-100 text-red-800 text-xs 
rounded">${participant.tidakHadir} Tidak</span>
 </div>
 </div>
 </div>
 </div>
 `;
 }).join('');
 }
 function exportMeetingAttendanceData() {
 const meetingAttendanceData = currentData.filter(item => item.type === 
'meeting_attendance');
 
 if (meetingAttendanceData.length === 0) {
 showToast('Tidak ada data kehadiran rapat untuk diekspor.', 'error');
 return;
 }
 const exportData = meetingAttendanceData.map(item => ({
 'Tanggal': item.tanggal,
 'Waktu': item.waktu,
 'Nama Rapat': item.kelas,
 'Jenis Rapat': item.no_hp,
 'Tempat': item.tempat_lahir,
 'Nama Peserta': item.nama,
 'Mata Pelajaran': item.mata_pelajaran,
 'Status Kehadiran': item.status
 }));
 const ws = XLSX.utils.json_to_sheet(exportData);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb, ws, 'Kehadiran Rapat');
 XLSX.writeFile(wb, `Kehadiran_Rapat_${currentYear.replace('/', '-')}.xlsx`);
 }
 async function deleteMeetingAttendance(id) {
 const item = currentData.find(item => item.id === id);
 if (!item) return;
 if (window.dataSdk) {
 const result = await window.dataSdk.delete(item);
 if (result.isOk) {
 showToast("Data kehadiran rapat berhasil dihapus!", "success");
 } else {
 showToast("Gagal menghapus data kehadiran rapat.", "error");
 }
 }
 }
 // Initialize app
 initializeApp();
 </script>
<script>(function(){function c(){var 
b=a.contentDocument||a.contentWindow.document;if(b){var 
d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'99ec13ba71
dbec6a',t:'MTc2MzE4MTY5NS4wMDAwMDA='};var 
a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge￾platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChi
ld(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var 
a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';
a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.b
ody.appendChild(a);if('loading'!==document.readyState)c();else 
if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);els
e{var 
e=document.onreadystatechange||function(){};document.onreadystatechange=functi
on(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())
}}}})();</script></body>
</html>
