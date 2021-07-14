# Multi Bahasa Laravel Localization
Dalam artikel ini kita akan mencoba untuk menggunakan fitur Laravel Localization untuk multi bahasa pada Laravel. Penggunaan multi bahasa sangat dibutuhkan agar pengguna mendapatkan informasi dengan akurat, dimana aplikasi akan menampilkan berbagai bahasa lebih dari satu.

## Laravel Localization
Fitur Laravel Localization menyediakan cara mudah untuk mengambil string dalam berbagai bahasa, memungkinkan Anda untuk dengan mudah mendukung beberapa bahasa dalam aplikasi Anda.

Laravel sudah menyediakan fitur tersebut secara bawaan dengan begitu kita dapat lebih mudah untuk menggunakan Laravel Localization.

## Persiapan
Untuk menggunakan Laravel Localization terlebih dahulu membuat folder lang untuk menaruh library bahasa, didalam folder lang terdapat folder en dan id. Bahasa Inggris akan menggunakan folder en, untuk bahasa Indonesia akan menggunakan folder id. Untuk menggunakannya, pengaturan bahasa dibuat dalam array. Didalam array akan berisi key dan value.

Key sebagai pemanggil, dan Value adalah isi dari 
Key 

Studi kasus yang akan digunakan adalah halaman form registrasi anggota, yang dimana akan menggunakan dua bahasa untuk setiap labelnnya.

## Mulai Membuat Project
Pertama, Install dahulu Laravelnnya. Perintah untuk membuat project laravel:

```
	composer create-project --prefer-dist laravel/laravel:^x.0 NamaProject
```

Setelah selesai install laravel, buat folder di dalam folder *lang* yaitu *en* dan *id*

<p align="center">
<img src="https://i.ibb.co/Kh99N4W/1.png"  style="height: 250px"/>
</p>

Lalu, buat file baru dengan nama regis.php di folder *en* dan *id*.

Didalam file regis akan berisi Key dan Value yang akan ditampilkan di halaman form registrasi.
Berikut isi dari file regis.php untuk folder en dan id:

**Resources\lang\en\regis.php**
```
<?php
return [
    'header' => 'Registration Form',
    "title" => "Please fill up form Registration below",
    "biodata" => [
        "first_name" => "First Name",
        "last_name" => "Last Name",
        "address" => "Your Address",
        "phone_number" => "Phone Number",
        "password" => "Your Password",
    ],
    "button" => "Register"
];
```
**Resources\lang\id\regis.php**

```
<?php
return [
    'header' => 'Form Registrasi',
    "title" => "Silakan isi form dibawah ini untuk registrasi",
    "biodata" => [
        "first_name" => "Nama Depan",
        "last_name" => "Nama Belakang",
        "address" => "Alamat",
        "phone_number" => "Nomor Telepon",
        "password" => "Password",
    ],
    "button" => "Register"
];
```

Selanjutnya, membuat view registernya

**Resources\views\regis.blade.php**

```
<!DOCTYPE html>
<html>

<head>
    <title>Form Register</title>
    <link href="{{url('css/regis.css')}}" rel="stylesheet" type="text/css">
</head>

<body bgcolor="#E6E6FA">
<h2>@lang('regis.header')</h2>
    <form name="" action="" method="post">
        <h2>@lang('regis.title')</h2>

        <label for="" id="">@lang('regis.biodata.first_name') :</label>
        <input type="text" name="" id=""><br />

        <label for="=" id="">@lang('regis.biodata.last_name') :</label>
        <input type="text" name="" id="="><br />

        <label for="" id="">@lang('regis.biodata.address') :</label>
        <input type="text" name="" id=""><br />

        <label for="" id="">@lang('regis.biodata.phone_number') :</label>
        <input type="text" name="" id=""><br />

        <label for="" id="">@lang('regis.biodata.password') :</label>
        <input type="password" name="" id=""><br />

        <button type="submit" value="Submit" id="button">@lang('regis.button')</button>
       

    </form>

</body>

</html>

```

lalu, membuat routenya

**Routes\web.php**

```
Route::get('/regis', function () {
    return view('regis');
});
```

Jika sudah semua dibuat, mari kita coba untuk lihat hasilnya di browser

Jalankan terlebih dahulu Laravel local development server

```
php artisan serve
```
Kemudian akses halamannya http://127.0.0.1:8000/regis

<p align="center">
<a href="https://ibb.co/Pt67SyX"><img src="https://i.ibb.co/FnDSP1Z/2.png" alt="2" border="0" /></a>
</p>

Bahasa dari halaman akan berbahasa Inggris, karena Laravel secara default menentukan bahasanya Inggris

Untuk mengganti bahasa default laravel menjadi Bahasa Indonesia hanya perlu mengganti **'locale' => 'en'** menjadi **'locale' => 'id'** pada file **app.php** di folder **config**

Maka, jika sudah diubah menjadi **'locale' => 'id'** bahasa dari halaman akan berubah menjadi bahasa Indonesia secara default

<p align='center'>
<img src="https://i.ibb.co/R6WFfW2/3.png" alt="3" border="0"></a>
<p>

Kita juga dapat menentukan bahasanya melalui Url, yaitu menggunakan setLocale pada route.

```
Route::get('/regis/{locale}', function ($locale) {
    App::setLocale($locale);
    return view('regis');
});
```
Lalu, buka halamannya http://127.0.0.1:8000/regis/en

<a href="https://ibb.co/SBTH04X"><img src="https://i.ibb.co/nj24fNs/4.png" alt="4" border="0"></a>

Halaman akan berbahasa Inggris yang sebelumnya bahasa defaultnya di set **id**. Begitu juga sebaliknya, jika ingin menampilkan halaman berbahasa Indonesia kita hanya perlu menambahkan **id** diakhir alamat http://127.0.0.1:8000/regis/id







