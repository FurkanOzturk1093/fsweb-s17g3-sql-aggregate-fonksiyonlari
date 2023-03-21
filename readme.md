# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın. 1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
select o.ograd,o.ogrsoyad, i.atarih from ogrenci as o
join islem as i on o.ogrno=i.ogrno

    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
     select kitapadi,turno from kitap
     where turno="6" or turno="4"
     order by turno

    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

     select o.sinif,o.ograd,o.ogrsoyad,o.ogrno,k.kitapadi from ogrenci as o
     join islem as i on i.ogrno=o.ogrno
     join kitap as k on k.kitapno=i.kitapno
     where sinif="10B" or sinif="10C"
     order by sinif
    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
    select o.ograd,o.ogrsoyad, i.atarih from ogrenci as o
    join islem as i on o.ogrno=i.ogrno

    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
    select kitapadi,turno from kitap
     where turno="6" or turno="4"
     order by turno

    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.
     select o.sinif,o.ograd,o.ogrsoyad,o.ogrno,k.kitapadi from ogrenci as o
     join islem as i on i.ogrno=o.ogrno
     join kitap as k on k.kitapno=i.kitapno
     where sinif="10B" or sinif="10C"
     order by sinif

    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.
       select o.ogrno,o.sinif,o.ograd,o.ogrsoyad,i.atarih from ogrenci as o
       left join islem as i on i.ogrno=o.ogrno
       left join kitap as k on k.kitapno=i.kitapno


    8) Kitap almayan öğrencileri listeleyin.
       select o.ogrno,o.sinif,o.ograd,o.ogrsoyad,i.atarih from ogrenci as o
       left join islem as i on i.ogrno=o.ogrno
       left join kitap as k on k.kitapno=i.kitapno
       where i.atarih is

    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.
     select count(k.kitapadi),k.kitapadi from kitap as k
       join islem as i on i.kitapno=k.kitapno
       group by k.kitapadi
       order by count(k.kitapadi) desc

    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

     select count(k.kitapadi),k.kitapadi from kitap as k
     left join islem as i on i.kitapno=k.kitapno
     group by k.kitapadi
     order by count(k.kitapadi) desc

    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.
     select o.ograd,o.ogrsoyad,k.kitapadi from ogrenci as o
     left join islem as i on i.ogrno=o.ogrno
     left join kitap as k on k.kitapno=i.kita

    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.
     select o.ograd,o.ogrsoyad,k.kitapadi,y.yazarad,y.yazarsoyad,t.turadi,i.atarih from ogrenci as o
     left join islem as i on i.ogrno=o.ogrno
     left join kitap as k on k.kitapno=i.kitapno
     left join yazar as y on y.yazarno=k.yazarno
     left join tur as t on t.turno=k.turno


    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.
     select o.ograd,o.ogrsoyad,o.sinif,count(k.kitapadi) from ogrenci as o
     left join islem as i on i.ogrno= o.ogrno
     left join kitap as k on k.kitapno=i.kitapno
     where o.sinif="10A" or o.sinif="10B"
     group by k.kitapadi

    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG
    select avg(sayfasayisi) from kitap


    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.
    select * from kitap
    where sayfasayisi>236.2444


    16) Öğrenci tablosundaki öğrenci sayısını gösterin
    select count(ogrno) from ogrenci

    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.
     select count(ograd),ograd from ogrenci
     group by ograd

    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.
     select max(sayfasayisi) from kitap

    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.
    select (sayfasayisi),kitapadi from kitap
    order by sayfasayisi desc
    limit 1


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

select (sayfasayisi) from kitap
order by sayfasayisi
limit 1

    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

select (sayfasayisi),kitapadi from kitap
order by sayfasayisi
limit 1

    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.
    select k.sayfasayisi,t.turadi from kitap as k
    join tur as t on t.turno=k.turno
    where t.turadi="Dram"
    order by k.sayfasayisi desc
    limit 1

    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.
     select sum(k.sayfasayisi) from ogrenci as o
     join islem as i on i.ogrno=o.ogrno
     join kitap as k on k.kitapno=i.kitapno
     where o.ogrno="15"

    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )
    select ograd,count(ograd) from ogrenci
    group by ograd
    order by count(ograd) desc


    26) Her sınıftaki öğrenci sayısını bulunuz.
    select count(sinif),sinif from ogrenci
    group by sinif
    order by sinif


    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.
	select count(sinif),sinif,count(cinsiyet) from ogrenci
group by sinif ,cinsiyet



    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.
select o.ogrno,count(o.ogrno),o.ograd,o.ogrsoyad,sum(k.sayfasayisi) from ogrenci as o

join islem as i on i.ogrno=o.ogrno

join kitap as k on k.kitapno=i.kitapno
group by(o.ogrno)
order by sum(k.sayfasayisi) desc

    29) Her öğrencinin okuduğu kitap sayısını getiriniz.
select count(o.ogrno) as "okunan kitap sayisi", o.ogrno,o.ograd,o.ogrsoyad from ogrenci as o

join islem as i on i.ogrno=o.ogrno

join kitap as k on k.kitapno=i.kitapno
group by ogrno
order by ogrno
