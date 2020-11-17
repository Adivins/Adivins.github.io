saya mengetahui cara ini sudah lama saat saya menginstall [Gentoo gnu/linux](https://www.gentoo.org/), ini sangat berguna jika terjadi masalah pada [bootloader](https://en.wikipedia.org/wiki/Booting#First-stage_boot_loader), jika terjadi masalah pada boot loader kita tidak dapat memasuki sistem operasi kita, jadi kita dapat menggunakan cara ini dan cara ini sangat berguna bagi developer jika ingin mengemas aplikasinya dengan deb atau xbps sehingga dengan mudah di install di komputer pengguna yang menggunakan distro gnu/linux yang berbeda  

<img class="img-fluid" src="https://ik.imagekit.io/ei818rceo5ypg/Screenshot_at_2019-06-16_11-01-35_p_Jv_ClU1.png" alt="GNU/Linux">

#### kegunaan :

1. Uji pengembangan perangkat lunak dalam pristine environment
2. Jalankan perangkat lunak yang dimaksudkan untuk distro gnu/linux lain
3. Jalankan perangkat lunak yang memerlukan versi lebih lama atau lebih baru dari distro Anda saat ini
4. Akses instalasi Linux di partisi yang berbeda tanpa harus reboot
5. Boot CD Live dan gunakan chroot untuk memperbaiki instalasi atau GRUB Anda
6. Akses drive di mana Anda lupa user/pass
7. memperbaiki initscript yang error

#### packages yang dibutuhkan :
* chroot (GNU coreutils) version 8.31
* sudo version 1.8.27

#### langkah-langkah :
1. mount storage yang ingin di perbaiki booloadernya
2. bukalah sebuah terminal
3. ubahlah directory ke directory dimana kita mount storage kita jika di void gnu/linux ada di /run/media/\<home\>/\<uuid\>
4. mount pseudo filesystems :  
```
sudo mount --bind /dev ./dev;
sudo mount --bind /dev/pts ./dev/pts;
sudo mount --bind /proc  ./proc;
```
5. chroot ke dalam folder drive  
```
sudo chroot ./
```

#### hal yang perlu diingat :
cara ini bukan 100% terisolasi dari sistem. Lingkungan chroot tidak pernah "di-boot", jadi ia tidak pernah memuat kernelnya sendiri, dan tidak pernah menjalankan skrip initnya sendiri.

Metode ini tentu saja bukan pengganti untuk virtualisasi, dan tidak dapat melakukan semua yang dapat dilakukan oleh perangkat lunak [VM](https://en.wikipedia.org/wiki/Virtual_machine). Sistem chroot tidak pernah benar-benar "mem-boot" atau menjalankan skrip init, dan mungkin OS chroot Anda mungkin memerlukan beberapa fitur yang tidak ditawarkan oleh kernel host Anda.

seperti itulah caranya, anda juga dapat menginstall debian chroot menggunakan debootstrap menggunakan cara [ini](https://wiki.debian.org/chroot)