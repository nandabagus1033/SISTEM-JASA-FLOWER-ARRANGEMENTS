# SISTEM-JASA-FLOWER-ARRANGEMENTS
Sistem ini dapat digunakan untuk merekam data pengantaran flower arrangements, meliputi nomor nota pembelian, tanggal pembuatan, dan tanggal pengantaran. Dibuat untuk memenuhi tugas final project mata kuliah Pemrograman Berorientasi Objek tahun ajaran 2020/2021, S1 Ilmu Komputer, Universitas Lampung.


Alat-alat dari proyek ini:
@ NetBeans
@ MySQL server
@ Scene Builder

@ Class Diagram
FlowerArrangements <|-- Customer
    
    class FlowerArrangements {
      +Int No_Nota
      +Int Tanggal_Pemesanan
      +Int Tanggal_Pengantaran      
    }
    
    class Customer{
      +Int No_Nota
      +Varchar Nama
      +Varchar Alamat
    }
@ ERD
erDiagram
FlowerArrangements ||..|| Customer : is
        
FlowerArrangements {
Int No_Nota
Int Tanggal_Pemesanan
Int Tanggal_Pengantaran
}
Customer {
int No_Nota
varchar Nama
varchar Alamat
}
