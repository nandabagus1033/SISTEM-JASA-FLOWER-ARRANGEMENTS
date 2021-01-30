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
--------------------------------------------------------------------------
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
--------------------------------------------------------------------------
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
 --------------------------------------------------------------------------
 1)CUSTOMER.java
 --------------------------------------------------------------------------
  
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
    
    
2)MAIN.java
--------------------------------------------------------------------------
       
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

3)BUNGA.java
--------------------------------------------------------------------------

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

4)BUNGA ALAMI.java
--------------------------------------------------------------------------

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

5)BUNGA SINTETIS.java
--------------------------------------------------------------------------

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
  
  

6)BUNGA DATA MODEL.java
--------------------------------------------------------------------------
       package karanganbungafx;

       import java.sql.Connection;
       import java.sql.PreparedStatement;
       import java.sql.ResultSet;
       import java.sql.SQLException;
       import java.util.logging.Level;
       import java.util.logging.Logger;
       import javafx.collections.FXCollections;
       import javafx.collections.ObservableList;
       import karanganbungafx.database.DBHelper;

       public class BungaDataModel {
    public final Connection conn;
    
    public BungaDataModel(String driver) throws SQLException {
        this.conn = DBHelper.getConnection(driver);
    }
    
    public void addBAlami(BungaAlami alami) throws SQLException{
        String insertBunga = "INSERT INTO bunga (nama_bunga)"
                + "VALUES (?)";
        PreparedStatement stmtBunga = conn.prepareStatement(insertBunga);
        stmtBunga.setString(1,alami.getNamaBunga());
        stmtBunga.execute();
        
        String insertAlmi = "INSERT INTO bungan_alami (nama_bunga, hari)"
                + "VALUES (?,?)";
        PreparedStatement stmtAlami = conn.prepareStatement(insertAlmi);
        stmtAlami.setString(1,alami.getNamaBunga());
        stmtAlami.setInt(2,alami.getHari());
        stmtAlami.execute();
    }
    
    public void addBSintetis(BungaSintetis sintetis) throws SQLException{
        String insertBunga = "INSERT INTO bunga (nama_bunga)"
                + "VALUES (?)";
        PreparedStatement stmtBunga = conn.prepareStatement(insertBunga);
        stmtBunga.setString(1,sintetis.getNamaBunga());
        stmtBunga.execute();
        
        String insertSintetis = "INSERT INTO bunga_sintetis (nama_bunga, bahan)"
                + "VALUES (?,?)";
        PreparedStatement stmtAlami = conn.prepareStatement(insertSintetis);
        stmtAlami.setString(1,sintetis.getNamaBunga());
        stmtAlami.setString(2,sintetis.getBahan());
        stmtAlami.execute();
    }
    
    public void addCustomer(Customer cutom) throws SQLException{
        String insertBunga = "INSERT INTO customer (id_customer,bunga_pilihan,tanggal,ucapan)"
                + "VALUES (?,?,?,?)";
        PreparedStatement stmtBunga = conn.prepareStatement(insertBunga);
        stmtBunga.setInt(1,cutom.getIDCustom());
        stmtBunga.setString(2,cutom.getPesanBunga());
        stmtBunga.setString(3,cutom.getTanggal());
        stmtBunga.setString(4,cutom.getUcapan());
        stmtBunga.execute();
    }
    
    public int nextID() throws SQLException{
        String sql = "SELECT MAX(id_customer) from customer";
        ResultSet rs = conn.createStatement().executeQuery(sql);
        while (rs.next()){
                return rs.getInt(1)==0?10001:rs.getInt(1)+1;
                }
        return 10001;
    }
    
    public ObservableList<String> getNamaBunga(){
        ObservableList<String> data = FXCollections.observableArrayList();  
        String sql ="SELECT nama_bunga FROM bunga";
        try {
            ResultSet rs = conn.createStatement().executeQuery(sql);
            while (rs.next()){
                data.add(rs.getString(1));
                }
        } catch (SQLException ex) {
            Logger.getLogger(BungaDataModel.class.getName()).log(Level.SEVERE, null, ex);
        }
        return data;
    }
    
    public ObservableList<BungaAlami> getDataAlami() throws SQLException{
        ObservableList<BungaAlami> data = FXCollections.observableArrayList();  
        String sql ="SELECT nama_bunga, hari FROM bungan_alami";
        
        ResultSet rs = conn.createStatement().executeQuery(sql);
        while(rs.next()){
            data.add(new BungaAlami(rs.getString(1),rs.getInt(2)));
        }
            
        return data;
    }
    public ObservableList<BungaSintetis> getDataSintetis() throws SQLException{
        ObservableList<BungaSintetis> data = FXCollections.observableArrayList();  
        String sql ="SELECT nama_bunga, bahan FROM bunga_sintetis";
        
        ResultSet rs = conn.createStatement().executeQuery(sql);
        while(rs.next()){
            data.add(new BungaSintetis(rs.getString(1),rs.getString(2)));
        }
            
        return data;
    }
    public ObservableList<Customer> getDataCustomer() throws SQLException{
        ObservableList<Customer> data = FXCollections.observableArrayList();  
        String sql ="SELECT id_customer, bunga_pilihan, tanggal, ucapan FROM customer";
        
        ResultSet rs = conn.createStatement().executeQuery(sql);
        while(rs.next()){
            data.add(new Customer(rs.getInt(1),rs.getString(2),rs.getString(3),rs.getString(4)));
        }
            
        return data;
    }

}

7)KARANGAN DOCUMENT CONTROLLER.java
--------------------------------------------------------------------------
       package karanganbungafx;

       import java.net.URL;
       import java.sql.SQLException;
       import java.util.ResourceBundle;
       import java.util.logging.Level;
       import java.util.logging.Logger;
       import javafx.collections.FXCollections;
       import javafx.collections.ObservableList;
       import javafx.event.ActionEvent;
       import javafx.fxml.FXML;
       import javafx.fxml.Initializable;
       import javafx.scene.control.Button;
       import javafx.scene.control.ComboBox;
       import javafx.scene.control.DatePicker;
       import javafx.scene.control.Label;
       import javafx.scene.control.TableColumn;
       import javafx.scene.control.TableView;
       import javafx.scene.control.TextField;
       import javafx.scene.control.cell.PropertyValueFactory;

       public class KaranganDocumentContoller implements Initializable {
    
    public BungaDataModel BDM;
    
    @FXML
    private Label DBStatus;
    
    @FXML
    private TextField tf_bungaA;

    @FXML
    private Button btn_add1;

    @FXML
    private ComboBox<Integer> cb_hari;

    @FXML
    private Button btn_refresh1;

    @FXML
    private Button btn_clear1;

    @FXML
    private TableView<BungaAlami> tab_BAlami;

    @FXML
    private TableColumn<BungaAlami, String> c_NamaAlami;

    @FXML
    private TableColumn<BungaAlami, Integer> c_layu;

    @FXML
    private TextField tf_namaS;

    @FXML
    private Button btn_Add2;

    @FXML
    private ComboBox<String> cb_bahan;

    @FXML
    private Button btn_refresh2;

    @FXML
    private Button btn_clear2;

    @FXML
    private TableView<BungaSintetis> tab_BSintetis;

    @FXML
    private TableColumn<BungaSintetis, String> c_namaSintetis;

    @FXML
    private TableColumn<BungaSintetis, String> c_bahan;

    @FXML
    private TextField tf_ID;

    @FXML
    private Button btn_add3;

    @FXML
    private TextField tf_ucapan;

    @FXML
    private ComboBox<String> cb_pilihan;

    @FXML
    private DatePicker dt_tanggal;

    @FXML
    private Button btn_refresh3;

    @FXML
    private Button btn_clear3;

    @FXML
    private TableView<Customer> tab_Customer;

    @FXML
    private TableColumn<Customer, Integer> c_ID;

    @FXML
    private TableColumn<Customer, String> c_pilihan;

    @FXML
    private TableColumn<Customer, String> c_tanggal;

    @FXML
    private TableColumn<Customer, String> c_ucapan;

    @FXML
    void handleAdd1(ActionEvent event) {
        BungaAlami BA = new BungaAlami(tf_bungaA.getText(), cb_hari.getValue());        
        
        try {
            BDM.addBAlami(BA);
            btn_refresh1.fire();
            btn_clear1.fire();
            cb_pilihan.setItems(BDM.getNamaBunga());
        } catch (SQLException ex) {
            Logger.getLogger(KaranganDocumentContoller.class.getName()).log(Level.SEVERE, null, ex);
        }

    }

    @FXML
    void handleAdd2(ActionEvent event) {
        BungaSintetis BS = new BungaSintetis(tf_namaS.getText(), cb_bahan.getValue());        
        
        try {
            BDM.addBSintetis(BS);
            btn_refresh2.fire();
            btn_clear2.fire();
            cb_pilihan.setItems(BDM.getNamaBunga());
        } catch (SQLException ex) {
            Logger.getLogger(KaranganDocumentContoller.class.getName()).log(Level.SEVERE, null, ex);
        }
    }

    @FXML
    void handleAdd3(ActionEvent event) {
        Customer ct = new Customer(Integer.parseInt(tf_ID.getText()), cb_pilihan.getValue(), String.valueOf(dt_tanggal.getValue()), tf_ucapan.getText());        
        
        try {
            BDM.addCustomer(ct);
            btn_refresh3.fire();
            btn_clear3.fire();
            
        } catch (SQLException ex) {
            Logger.getLogger(KaranganDocumentContoller.class.getName()).log(Level.SEVERE, null, ex);
        }
    }

    @FXML
    void handleClear1(ActionEvent event) {
        tf_bungaA.setText(null);
    }

    @FXML
    void handleClear2(ActionEvent event) {
        tf_namaS.setText(null);
    }

    @FXML
    void handleClear3(ActionEvent event) throws SQLException {
        tf_ID.setText(String.valueOf(BDM.nextID()));
        tf_ucapan.setText(null);
    }   

    @FXML
    void handleRefresh1(ActionEvent event) throws SQLException {
        ObservableList<BungaAlami> data = BDM.getDataAlami();
        c_NamaAlami.setCellValueFactory(new PropertyValueFactory<>("namaBunga"));
        c_layu.setCellValueFactory(new PropertyValueFactory<>("hari"));
        tab_BAlami.setItems(data);
    }

    @FXML
    void handleRefresh2(ActionEvent event) throws SQLException {
        ObservableList<BungaSintetis> data = BDM.getDataSintetis();
        c_namaSintetis.setCellValueFactory(new PropertyValueFactory<>("namaBunga"));
        c_bahan.setCellValueFactory(new PropertyValueFactory<>("bahan"));
        tab_BSintetis.setItems(data);
    }

    @FXML
    void handleRefresh3(ActionEvent event) throws SQLException {
        ObservableList<Customer> data = BDM.getDataCustomer();
        c_ID.setCellValueFactory(new PropertyValueFactory<>("IDCustom"));
        c_pilihan.setCellValueFactory(new PropertyValueFactory<>("PesanBunga"));
        c_tanggal.setCellValueFactory(new PropertyValueFactory<>("tanggal"));
        c_ucapan.setCellValueFactory(new PropertyValueFactory<>("ucapan"));
        tab_Customer.setItems(data);
    }
    
    @Override
    public void initialize(URL url, ResourceBundle rb) {
        // TODO
        ObservableList<Integer> layu = FXCollections.observableArrayList(1,2,3,4,5,6,7,8,9);
        ObservableList<String> bahan = FXCollections.observableArrayList("Kain","plastik","karet","kertas");
        cb_hari.setItems(layu);
        cb_bahan.setItems(bahan);
        
        try {
            BDM = new BungaDataModel("MYSQL");
            DBStatus.setText(BDM.conn==null?"Gagal Terhubung":"Terhubung");
            tf_ID.setText(String.valueOf(BDM.nextID()));
            cb_pilihan.setItems(BDM.getNamaBunga());
            btn_refresh1.fire();
            btn_refresh2.fire();
            btn_refresh3.fire();
        } catch (SQLException ex) {
            Logger.getLogger(KaranganDocumentContoller.class.getName()).log(Level.SEVERE, null, ex);
        }
    }    
    
}      
