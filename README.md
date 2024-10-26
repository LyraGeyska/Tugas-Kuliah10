# Penggunaan iReport untuk Membuat Laporan

## Pengertian Report
Report merupakan proses atau hasil dari pembuatan laporan dari data yang ada dalam sebuah aplikasi. Report biasanya berupa lembar laporan yang berisikan data terstruktur misalnya sebuah tabel, grafik, ataupun sebuah ringkasan.

## A. Langkah-langkah Instalasi Plugin iReport 

### 1. Download iReport, jangan lupa extract file yang sudah di download.

### 2. Kemudian buka netbeans, masuk pada menu Tools > Plugins
![image](https://github.com/user-attachments/assets/dd0e13f7-0956-4852-b05f-28704df7838a)


Pilih Downloaded > Add Plugins... > masukkan file plugins iReport yang sudah didownload > Open, Akan muncul tampilan seperti berikut :
![image](https://github.com/user-attachments/assets/eb83589f-3d72-4c81-9e66-7c888eaf6830)

Setelah itu centang ketiga file, dan lakukan Instalasi.

## B. Langkah-Langkah Menambahkan JasperReport pada Netbeans
### 1. Download file Library pada repository, kemudian extract.
### 2. Buka menu Tools > Libraries
![image](https://github.com/user-attachments/assets/1c1b7dcd-2ded-4026-b730-446c620bded9)

### 3. Kemudian hapus Library JasperReport yang sebelumnya sudah ada, dan buat Library baru.
![image](https://github.com/user-attachments/assets/f3cb467e-cb5b-42c4-844a-faf6dfd8703d)

### 4. Buat Library baru dan beri nama JasperReport, lalu OK.
![image](https://github.com/user-attachments/assets/c18a0c43-d31e-4b08-9708-74658ad28aaf)

### 5. Kemudian klik kanan Folder Libraries > Add Library > Pilih JasperReport > Add Library
![image](https://github.com/user-attachments/assets/94b8443a-847b-4a5c-b24e-bb623c972a1b)
![image](https://github.com/user-attachments/assets/72d6ce6c-4b1a-48e9-9c6a-58df705f3218)

### 6. Tampilan setelah Library berhasil ditambahkan :
![image](https://github.com/user-attachments/assets/94fbd10a-22e0-4b70-a9ab-8771e7e209c9)

## C. Membuat iReport pada Netbeans

### 1. Buat file report dengan cara klik kanan pada package projek > New > Other > Report > Report Wizard > Next
![image](https://github.com/user-attachments/assets/a22d5c8c-e794-4740-be3e-6f8907379b9b)
![image](https://github.com/user-attachments/assets/79262fb6-769e-4fd9-9aef-63193113fe36)

### 2. Pilih Layout sesuai yang anda inginkan, kemudian Next >
![image](https://github.com/user-attachments/assets/9e567122-3d64-44c4-9d4f-1055902a3649)

### 3. Beri nama pada file anda.
![image](https://github.com/user-attachments/assets/daba517f-6ff9-4942-84d9-b18275131c7f)

### 4. Buat koneksi database dengan cara klik new > Database JDBC connection > Next
![image](https://github.com/user-attachments/assets/08e49834-1c40-41b7-90ad-4cce5a80a9be)

Isi sesuai database anda, (pada gambar yang dicoret orange, adalah nama_database anda, ubah sesuai dengan nama database anda) > Save.
![image](https://github.com/user-attachments/assets/e3342db5-70c9-4446-8e4e-7fcf4175bcc4)

pilih koneksi yang sudah anda buat, dan isi SQL pada kotak Query (SQL).
![image](https://github.com/user-attachments/assets/7ca0738a-1ac0-4be6-8026-0082ee2e3e5e)
SELECT * FROM nama_table
![image](https://github.com/user-attachments/assets/760644a5-60d2-449a-807c-ecb63c29f06c)

### 5. Ikuti langkah selanjutnya, klik tombol pada kotak merah, kemudian next sampai selesai.
![image](https://github.com/user-attachments/assets/f4efffc5-6ca3-4201-83a3-508afdf8aede)
![image](https://github.com/user-attachments/assets/92fa816e-a302-45b4-9c32-de3d255c586e)

Hasil akhir akan seperti ini, dan Finish
![image](https://github.com/user-attachments/assets/8bcbf629-c702-4b52-97d1-1e49afde5f31)

Edit Sesuai yang anda inginkan.
![image](https://github.com/user-attachments/assets/fcc87333-c3fa-474d-9c58-881b10f54358)

### 6. Buka file Java Swing, kemudian buatlah button Cetak.
![image](https://github.com/user-attachments/assets/6b2f8cee-6725-4910-89f4-91f63459bdb2)

### 7. Ubah variabel menjadi btnCetak, kemudian double click pada button tersebut.
Masukkan code berikut :
<pre>
  private void btnCetakActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        String driver = "org.postgresql.Driver";
        String koneksi = "jdbc:postgresql://localhost:5432/nama_database";
        String user = "postgres";
        String password = "password_database";
        File reportFile = new File(".");
        String dirr = "";

        try {
            Class.forName(driver);
            Connection conn = DriverManager.getConnection(koneksi, user, password);
            Statement stmt = conn.createStatement();
            String sql = "SELECT * FROM matakuliah";
            dirr = reportFile.getCanonicalPath() + "/src/UTSPBO/"; //letak file .jrxml anda
            JasperDesign design = JRXmlLoader.load(dirr + "reportMatakuliah.jrxml"); //nama nama_file.jrxml anda
            JasperReport jr = JasperCompileManager.compileReport(design);
            ResultSet rs = stmt.executeQuery(sql);
            JRResultSetDataSource rsDataResource = new JRResultSetDataSource(rs);
            JasperPrint jp = JasperFillManager.fillReport(jr, new HashMap(), rsDataResource);
            JasperViewer.viewReport(jp);
        } catch (ClassNotFoundException | SQLException | IOException | JRException ex) {
            JOptionPane.showMessageDialog(null, "\nGagal Mencetak\n" + ex,
                    "Kesalahan", JOptionPane.ERROR_MESSAGE);
        }
    }  
</pre>

Kemudian Runing

## D. Cara Kerja atau Demo iReport
### 1. Running Program, pastikan anda sudah menginputkan data.
![image](https://github.com/user-attachments/assets/d4175fe0-7813-4ab9-b7b3-e4c1c3558ce2)

### 2. Klik button cetak, dan hasil report akan seperti berikut,
![image](https://github.com/user-attachments/assets/87ec3042-4bc7-4d63-8822-8a6a3cb25c9a)

File tersebut bisa disimpan dan bisa langsung di print





