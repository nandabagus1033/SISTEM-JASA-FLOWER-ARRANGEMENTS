# SISTEM-JASA-FLOWER-ARRANGEMENTS
Sistem ini dapat digunakan untuk merekam data ID Customer, Bunga pilihan, Tanggal Pesanan, dan Ucapan dalam karangan bunga menggunakan javafx. Dalam tampilannya GUI-nya dapat menggunakan scene builder dan mengkoneksi DB ke Xampp. Dibuat untuk memenuhi tugas final project mata kuliah Pemrograman Berorientasi Objek tahun ajaran 2020/2021, S1 Ilmu Komputer, Universitas Lampung.

NANDA BAGUS PRATAMA (1917051033)

Task : Membuat program di Netbeans (Tampilan GUI, Koneksi database)
       Membuat Repository di Github


M. ARROZI IRFAN (1957051008)

Task : Membuat program di NetBeans (Membuat program class javafx),
       Membuat Class Diagram di https://mermaid-js.github.io


ARJA SYAHRIRA (1917051036)

Task : Membuat program di Netbeans (Membuat program class javafx),
       Membuat ERD di https://mermaid-js.github.io



@ CLASS DIAGRAM
      
    classDiagram
    Bunga <|-- Customer : Implements
    Bunga o-- Bunga Alami : Memiliki
    Bunga o-- Bunga Sintetis : Memiliki
    class Bunga {
    +Varchar Nama    
    }
    class Customer{
    +Int ID
    +Varchar Nama
    +Varchar TanggalPesan
    +Varchar Ucapan
    }
    class Bunga Alami{
    +Varchar LayuDalam
    }
    class Bunga Sintetis {
    +Varchar JenisBahan
    }



@ ERD

       erDiagram
       Bunga ||..|| Customer : is
       Bunga ||--|| BungaAlami : Memilki
       Bunga ||--|| BungaSintetis : Memilki   
       Bunga {
       Varchar Nama
       }
       Customer{
       Int ID
       Varchar Nama
       Varchar TanggalPesan
       Varchar Ucapan
       }
       BungaAlami{
       Varchar LayuDalam
       }
       BungaSintetis{
       Varchar JenisBahan
       }
    
    
 @ JAVAFX
 
    
 
 
    
