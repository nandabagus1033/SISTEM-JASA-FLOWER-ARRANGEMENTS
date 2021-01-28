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
 
 1.CUSTOMER.java
  
       package karanganbungafx;

       import javafx.beans.property.IntegerProperty;
       import javafx.beans.property.SimpleIntegerProperty;
       import javafx.beans.property.SimpleStringProperty;
       import javafx.beans.property.StringProperty;
       public class Customer {
    IntegerProperty IDCustom;
    StringProperty PesanBunga;
    StringProperty tanggal;
    StringProperty ucapan;

    public Customer(Integer IDCustom, String PesanBunga, String tanggal, String ucapan) {
        this.IDCustom = new SimpleIntegerProperty(IDCustom);
        this.PesanBunga = new SimpleStringProperty(PesanBunga);
        this.tanggal = new SimpleStringProperty(tanggal);
        this.ucapan = new SimpleStringProperty(ucapan);
    }

    public Integer getIDCustom() {
        return IDCustom.get();
    }

    public void setIDCustom(Integer IDCustom) {
        this.IDCustom.set(IDCustom);
    }

    public String getPesanBunga() {
        return PesanBunga.get();
    }

    public void setPesanBunga(String PesanBunga) {
        this.PesanBunga.set(PesanBunga);
    }

    public String getTanggal() {
        return tanggal.get();
    }

    public void setTanggal(String tanggal) {
        this.tanggal.set(tanggal);
    }

    public String getUcapan() {
        return ucapan.get();
    }

    public void setUcapan(String ucapan) {
        this.ucapan.set(ucapan);
    }  
    }
    
    
2.MAIN.java
       
    package karanganbungafx;

       import java.sql.SQLException;
       import java.util.logging.Level;
       import java.util.logging.Logger;
       import javafx.application.Application;
       import static javafx.application.Application.launch;
       import javafx.fxml.FXMLLoader;
       import javafx.scene.Parent;
       import javafx.scene.Scene;
       import javafx.stage.Stage;
       import karanganbungafx.database.DBHelper;

       public class Main extends Application {
    
    @Override
    public void start(Stage stage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("KaranganFXMLDocument.fxml"));
        
        Scene scene = new Scene(root);
        
        stage.setScene(scene);
        stage.show();
    }

        public static void main(String[] args) {
        try {
            if(null != DBHelper.getConnection("MYSQL")){
            System.out.println("succes");
            } else{
            System.out.println("Gagal");
            } 
            
            
            launch(args);
            } catch (SQLException ex) {
            Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
            } 
    }
    
       }

@BUNGA

package karanganbungafx;

import javafx.beans.property.SimpleStringProperty;
import javafx.beans.property.StringProperty;
public class Bunga {
    StringProperty namaBunga;

    public Bunga(String namaBunga) {
        this.namaBunga = new SimpleStringProperty(namaBunga);
    }

    public String getNamaBunga() {
        return namaBunga.get();
    }

    public void setNamaBunga(String namaBunga) {
        this.namaBunga.set(namaBunga);
    }

}
--------------------------------------------------------------------------
@BUNGA ALAMI

package karanganbungafx;

import javafx.beans.property.IntegerProperty;
import javafx.beans.property.SimpleIntegerProperty;
public class BungaAlami extends Bunga{
    IntegerProperty hari;

    public BungaAlami(String namaBunga, int hari) {
        super(namaBunga);
        this.hari = new SimpleIntegerProperty(hari);
    }

    public Integer getHari() {
        return hari.get();
    }

    public void setHari(Integer hari) {
        this.hari.set(hari);
    }
    

}
-----------------------------------------------------
@BUNGA SINTETIS

package karanganbungafx;

import javafx.beans.property.SimpleStringProperty;
import javafx.beans.property.StringProperty;
public class BungaSintetis extends Bunga{
    StringProperty bahan;

    public BungaSintetis(String namaBunga, String bahan) {
        super(namaBunga);
        this.bahan = new SimpleStringProperty(bahan);
    }

    public String getBahan() {
        return bahan.get();
    }

    public void setBahan(String bahan) {
        this.bahan.set(bahan);
    }
    

}
--------------------------------------------------------------


 
 
    
