package config; // Menandakan file ini sudah berada di package config

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import javax.swing.JOptionPane;

public class Koneksi {
    private static Connection koneksi;

    public static Connection getKoneksi() {
        if (koneksi == null) {
            try {
                // Jalur koneksi langsung menembak ke database 'tokoatk' di Laragon
                String url = "jdbc:mysql://localhost:3306/tokoatk";
                String user = "root";
                String password = ""; // Secara default Laragon dikosongkan
                
                // Mendaftarkan Driver JDBC MySQL versi 9.x yang lu pakai
                DriverManager.registerDriver(new com.mysql.cj.jdbc.Driver());
                
                // Membuat koneksi
                koneksi = DriverManager.getConnection(url, user, password);
                System.out.println("Koneksi Sukses ke Database 'tokoatk'!");
                
            } catch (SQLException e) {
                System.out.println("Error Koneksi Database: " + e.getMessage());
                JOptionPane.showMessageDialog(null, 
                    "Gagal terhubung ke database Laragon!\nPastikan Laragon sudah di-Start All.\nError: " + e.getMessage(), 
                    "Error Koneksi", 
                    JOptionPane.ERROR_MESSAGE);
            }
        }
        return koneksi;
    }
}
