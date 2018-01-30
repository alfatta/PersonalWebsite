---
title     : Sortir Array Berdasarkan Child Array PHP
date      : 2017-09-13 15:06:34
modified  : 2017-11-30 21:26:14
tag       : PHP, Fungsi, Sortir
image     : sortir-array-berdasarkan-child-array-php
---

Dalam salah satu kesempatan saya bertemu permasalahan saat akan mengurutkan data yang sudah berupa array. Namun <!--more-->yang jadi masalah ialah saya ingin mengurutkannya berdasarkan item yang ada didalam setiap item dalam array utama.

Berikut ilustrasinya :
Nama dan jumlah buah terdapat dalam sebuah array. Akan diurutkan menurut jumlahnya.
``` php
<?php
// Sebelum diurutkan
$buah = array(
    array('jumlah'=>5, 'nama'=>'Apel'),
    array('jumlah'=>2, 'nama'=>'Pisang'),
    array('jumlah'=>4, 'nama'=>'Mangga'),
    array('jumlah'=>1, 'nama'=>'Jambu'),
    array('jumlah'=>3, 'nama'=>'Anggur')
);
// menjadi
$buah = array(
    array('jumlah'=>1, 'nama'=>'Jambu'),
    array('jumlah'=>2, 'nama'=>'Pisang'),
    array('jumlah'=>3, 'nama'=>'Anggur'),
    array('jumlah'=>4, 'nama'=>'Mangga'),
    array('jumlah'=>5, 'nama'=>'Apel')
);
```
Jadi setelah mencari cara di google, ternyata php telah menyiapkan fungsi untuk melakukan pengurutan item array dengan fungsi usort. Namun untuk dapat mengurutkan sesuai permasalahan diatas, perlu dilakukan sedikit trik.

Secara biasa fungsi usort berjalan dengan cara seperti ini :
``` php
<?php
$a = array(3, 2, 5, 6, 1);
usort($a, function ($a, $b) {
    if ($a == $b) return 0;
    return ($a < $b) ? -1 : 1;
});
```
Fungsi usort akan mengevaluasi array menggunakan fungsi yang didefinisikan. Dalam contoh tersebut setiap item akan dibandingkan apakah sama, lebih kecil, atau lebih besar dari item lainnya.

Untuk permasalahan pengurutan berdasarkan child, fungsi yang didefinisikan harus diubah, yakni yang dibandingkan haruslah menyatakan item dalam array. Seperti ini :

``` php
<?php
usort($buah, function ($a, $b) {
    if ($a['jumlah'] == $b['jumlah']) return 0;
    return ($a['jumlah'] < $b['jumlah']) ? -1 : 1;
});
```


Untuk mencobanya seperti ini :
```php
<?php
$buah = array(
    array('jumlah'=>5, 'nama'=>'Apel'),
    array('jumlah'=>2, 'nama'=>'Pisang'),
    array('jumlah'=>4, 'nama'=>'Mangga'),
    array('jumlah'=>1, 'nama'=>'Jambu'),
    array('jumlah'=>3, 'nama'=>'Anggur')
);
foreach ($buah as $item) {
    echo $item['nama'].":".$item['jumlah'];
    echo '<br>';
}
echo '==========<br>';
usort($buah, function ($a, $b) {
    if ($a['jumlah'] == $b['jumlah']) return 0;
    return ($a['jumlah'] < $b['jumlah']) ? -1 : 1;
});
foreach ($buah as $item) {
    echo $item['nama'].":".$item['jumlah'];
    echo '<br>';
}
```
