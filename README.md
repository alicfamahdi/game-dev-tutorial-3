> Silakan pilih fitur lanjutan yang ingin dikerjakan. Kemudian jelaskan proses pengerjaannya di dalam sebuah dokumen teks README.md. Cantumkan juga referensi-referensi yang digunakan sebagai acuan ketika menjelaskan proses implementasi.

Fitur lanjutan yang saya implementasikan adalah:
- Double jump - karakter pemain bisa melakukan aksi loncat sebanyak dua kali.
- Crouching - karakter pemain dapat jongkok dimana sprite-nya terlihat lebih kecil (misal: sprite karakter manusianya terlihat berjongkok) dan kecepatan pergerakannya menjadi lebih lambat ketika lagi jongkok

Untuk Double Jump, saya memodifikasi kode bagian
```
if is_on_floor() and Input.is_action_just_pressed('ui_up'):
    velocity.y = jump_speed
```
Awalnya, kode hanya mengakomodasi untuk jump sekali. 
Saya mencoba untuk menghapus bagian pengecekan kondisi `is_on_floor()` agar player bisa melakukan infinite number of jumps tanpa harus menempel pada floor terlebih dahulu (saat itu saya berpikir, fiturnya seperti ini saja kali ya). Setelah itu, saya membuat `jump_count` yang menghitung player sudah jump berapa kali. Jika jump_count == 2, player tidak bisa jump lagi. Saya juga mengatur agar setiap kali player kembali menempel ke floor, `jump_count` akan reset ke 0.

Untuk Crouching, saya memodifikasi potongan kode
```
if Input.is_action_pressed("ui_left"):
    velocity.x = -walk_speed
elif Input.is_action_pressed("ui_right"):
    velocity.x =  walk_speed
else:
    velocity.x = 0
```

Pertama, saya membuat suatu kondisi. Ketika press `ui_down`, kecepatan berjalan player akan melambat menjadi setengah dari kecepatan biasanya (1/2 * 200). Conditional ini digunakan untuk kedua pergerakan `ui_left` dan `ui_right`. Jika `ui_down` tidak ditekan, kecepatan player akan kembali seperti semula (200).

Selain 2 fitur tambahan tersebut, saya juga menyesuaikan `Sprite2D` agar sesuai dengan pergerakan yang dilakukan. Misalnya, ketika diam spritenya berdiri saja, ketika berjalan menampilkan sprite walk, ketika crouch spritenya duck, dan ketika jump spritenya jump. Tampilan sprite juga akan berubah sesuai arah inputnya.

Referensi
Godot Knowledge Hub. (n.d.). How to use Sprite2D in Godot Tutorial [Video]. YouTube. https://www.youtube.com/watch?v=wPyqwL0vIvA
GameStick. (2025, January 28). How to Flip Player Sprites Easily in Godot 4.3 . Godot tutorial. [Video]. YouTube. https://www.youtube.com/watch?v=QNJOAwpJokA
