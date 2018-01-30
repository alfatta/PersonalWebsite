---
title     : Tutorial Unit Testing PHP - Part 1 Set Up
date      : 2018-01-25 07:57:21
modified  : 2018-01-25 08:05:14
tag       : PHP, Testing, Unit Testing
image     : "tutorial-unit-testing-part-1-set-up"
---

Unit testing merupakan salah satu metode pengujian perangkat lunak. Pada metode ini, setiap unit dari source code diuji. <!--more-->Pengujian ini bertujuan untuk menentukan apakah setiap unit tersebut layak untuk digunakan. Dalam bahasa pemrograman PHP terdapat beberapa framework yang dapat mempermudah dalam proses unit testing. Seperti pada laman [Quora](https://www.quora.com/What-are-the-best-PHP-testing-frameworks) berikut, terdapat 5 framework yakni, PHPUnit, Codeception, Behat, PHPSpec, dan SimpleTest.

Pada kesempatan ini saya akan membahas unit testing dengan menggunakan PHPUnit karena paling populer dan dinilai sangat bagus dalam membantu proses testing. Pengujian kali ini saya lakukan dengan metode TDD (Test Driven Development), sehingga source code pengujian akan dibuat terlebih dahulu.

Pertama persiapkan direktori project. Pada contoh ini saya akan membahas kasus pengujian model yang berisi setter dan getter sederhana. Serta dalam penerapan PHPUnit saya menggunakan tools Composer. Buat direktori dan instal phpunit menggunakan composer.

``` shell
mkdir cobauji
cd cobauji
composer require phpunit/phpunit
```

Buat folder tests dan app. Folder app akan berisi source code utama dan folder tests akan berisi source code testing.

``` shell
mkdir app tests
```

Lalu ubah file `composer.json` agar dapat meload otomatis class yang akan dibuat pada folder app, sehingga berisi seperti ini:
``` json
{
    "require": {
        "phpunit/phpunit": "^6.5"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app"
        }
    }
}
```

Lalu buat file `phpunit.xml`. File ini berfungsi sebagai konfigurasi unit testing dengan PHPUnit dan juga akan menjalankan seluruh source code testing yang berada dalam folder tests. Isikan code berikut dalam file `phpunit.xml`
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="vendor/autoload.php"
        colors="true"
        verbose="true"
        stopOnFailure="false">
    <testsuites>
        <testsuite name="Test suite">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
</phpunit>
```

Sekian bagian pertama dari tutorial ini. Langkah selanjutnya akan dibahas pada kesempatan berikutnya.
