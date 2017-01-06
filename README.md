# Pisi Linux (LFS kitabına dayalı)
Pisi Operating System based on Linux From Scratch book

 Konak Sistem için Yapılması Gerekenler (ubuntu)
 
 apt-get install bsdtar binutils gcc g++ m4 make bison gawk texinfo pkg-config squashfs-tools lzip
 
 mv /usr/bin/mawk /usr/bin/mawk-eski
 
 rm /bin/sh
 
 ln -s /bin/bash /bin/sh
 
 PİSİ SİSTEMİNİN KURULUM YÖNERGELERİ

 Dikkat:
 1-Bu işlemleri root kullanıcısıyla yapınız.
 
 -Mekanizmanın Kurulması
 
 git clone https://github.com/ayhanyalcinsoy/malfs-milis.git
 
 cd malfs
 
 ilk önce host sistemin gereksinimleri karşıladığının kontrol edilmesi
 
 root@makine:/opt/malfs# ./lfs-mekanizma -gk
 
 yukarıdaki işlemin sonucuna göre gerekli gereksinimler yuklenir.
 
 ayrıca http://www.linuxfromscratch.org/lfs/view/development/prologue/hostreqs.html sayfasından versiyon kontrolü yapınız.

 gereksinimler tamamlandıktan sonra gerekli ortam değişkeni ayarı yapılır.

 root@makine:/opt/malfs# mkdir -p /mnt/lfs

 root@makine:/opt/malfs# export LFS=/mnt/lfs

 gerekli kaynak kodların indirilmesi 
 
 root@makine:/opt/malfs# ./lfs-mekanizma -ki

 birinci ayarlar yapılır
 
 root@makine:/opt/malfs# ./lfs-mekanizma -ba

 lfs kullanıcısıyla oturum acılmış olur.önsistem derlenmeye baslanır.
 
 lfs@makine:~$ ./lfs-mekanizma -td onsistem

 =======>  '/home/lfs/talimatname/onsistem/0libarchive/0libarchive#3.1.2-x86_64.mps.lz' derleme basarili
 
 yukarıdaki ifade goruldukten sonra
 
 "exit"
 
 komutu ile lfs kullanıcısından çıkılır.

 lfs önsistemin sıkıstırılması(yedeklemek için)

 root@makine:/opt/malfs# ./lfs-mekanizma -os

 üretici önsistemin yedeklenmesinden sonra üretici sisteme girmek için gerekli ayarlar yapılır.

 root@makine:/opt/malfs# ./lfs-mekanizma -ia
 
 üretici sisteme girilir.

 root@makine:/opt/malfs# ./lfs-mekanizma -cg

 root [ / ]#   ekranına düşülür."command not found" şeklinde hatalar görülebilir,normaldir.bash yuklemesinden sonra düzelecek.

 üretici sistem içersindeyken gerekli exportlar yapılır.

 root [ / ]#  export PATH=/bin:/usr/bin:/sbin:/usr/sbin:/tools/bin:/root/bin
 
 root [ / ]#  export FORCE_UNSAFE_CONFIGURE=1 

 root dizinine girilir.
 
 root [ / ]#  cd /root

 root [ / ]#  ./lfs-mekanizma -td temel

 komutu verilip temel sistemin kurulumu sağlanır.

 "bash chroot dışına çıkıp elle kurulmalıdır."  mesajı görülünce
 
 "exit" ile chroot dışına çıkılır

 root@makine:/opt/malfs# ./lfs-mekanizma -bk

 komutu verilip bash kurulumu sağlanır.

 tekrar chroot içine girilir.ortam değişkenleri ayarlandıktan sonra,temel sistem derlenmeye devam edilir.

 root@makine:/opt/malfs# ./lfs-mekanizma -cg
 
 root [ / ]#  export PATH=/bin:/usr/bin:/sbin:/usr/sbin:/tools/bin:/root/bin
 
 root [ / ]#  export FORCE_UNSAFE_CONFIGURE=1
 
 root [ / ]#  cd /root

 root [ / ]#  ./lfs-mekanizma -td temel
 
 en son aşağıdaki mesaj ile derleme bitmelidir.
 
 =======>  'ca-certificates#20160110-x86_64.mps.lz' basarili sekilde kuruldu.
 
 # PAKETÇİ ENTEGRESİ
 
 A-pisi paketçisi için

 ikincil ayarlar çalıştırılır.

 ./lfs-mekanizma -ia

 sisteme girmek için

 ./lfs-mekanizma -cg

 python derleme

 cd /root/base/python && omps

 perl modulu XML-parser kurulumu
 
 cpan shelline girilir

 cpan

 shellde bu komutla kurulur.sorular enterla geçilir.

 install XML::Parser
 
 /usr/bin/make install  -- OK  ifadesini görülürse kurulum tamamdır.exit le shellden cıkılır.

 intltool kurulumu

 cd /root/base/intltool && omps

 daha sonra pisi-arge icindeki "siralama"daki python modulleri kurulur.aşağıdaki formda.

 tar xf kaynak_kod
 
 cd kaynak_kod
 
 python setup.py install

NOT: 32bit de yaptıysanız etc/pisi/pisi.conf dosyasına gerekli ayarlar yapılır.
 
 tekrar chroot içine girilir.ortam değişkenleri ayarlandıktan sonra,temel sistem için gerekli ek paketler derlenir.

 temel sistem paketlerin paket_depo altında toplanması-paketlerin arsivlenmesi

 root [ / ]#  paketleri_arsivle

 chroottan cıkılıp,temel sistemin yedegi alınır.

 root [ / ]#  exit 
 
 root@makine:/opt/malfs# ./lfs-mekanizma -ts

 en son sisteme pisi kurulduktan sonra pspeclerin bulunduğu core repo klonlanır. 


 
 
 
