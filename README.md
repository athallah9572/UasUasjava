PENJELASAN

import java.util.ArrayList; 
import java.util.Scanner;  //Ini buat import library bawaan Java supaya kita bisa pakai Scanner, HashMap, dan TreeMap.

class Prestasi { //Ini class Prestasi, dipakai buat nyimpen data prestasi mahasiswa seperti nama, NIM, jenis prestasi, tingkat, dan tahun.
    
    String nama;
    String nim;
    String jenis;
    String tingkat;
    String tahun;

    public Prestasi(String nama, String nim, String jenis, String tingkat, String tahun) {
        //Ini constructor, fungsinya buat ngisi data tiap kali kita bikin objek Prestasi

        this.nama = nama;
        this.nim = nim;
        this.jenis = jenis;
        this.tingkat = tingkat;
        this.tahun = tahun;
    }

    @Override
    public String toString() {
        //Fungsi ini ngeformat data biar tampilannya rapi waktu dicetak di terminal.


        return "Nama: " + nama + ", NIM: " + nim + ", Jenis: " + jenis + ", Tingkat: " + tingkat + ", Tahun: " + tahun;
    }
}

public class PrestasiUas8 {
    - Variabel prestasiMap dipakai buat nyimpen semua prestasi pake HashMap, jadi kita bisa akses data lebih cepat pake NIM sebagai key.
    - Scanner dipakai buat ambil input dari user.
    private static ArrayList<Prestasi> prestasiList = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        menu();
    // Ini method utama yang langsung manggil menu(), jadi program bakal langsung masuk ke tampilan menu utama.
    }

    private static void menu() {
        while (true) {
            System.out.println("======= KELOMPOK 8 (Roihan, Sabrina, Atha)=======" );
            System.out.println("======= DATA PRESTASI MAHASISWA 2010-2024 =======" );
            System.out.println("\nMenu Utama:");
            System.out.println("1. Tambah Prestasi");
            System.out.println("2. Lihat Prestasi");
            System.out.println("3. Analisis Prestasi");
            System.out.println("4. Hapus Prestasi");
            System.out.println("5. Keluar");
            System.out.print("Pilih opsi (1-5): ");

            - Bagian ini cuma tampilan menu utama, biar user tahu apa aja yang bisa dilakukan
            int pilihan = scanner.nextInt();
            -  Ambil input pilihan menu dari user dan diubah ke int. Kalau input bukan angka, bakal kena error
            scanner.nextLine(); // Clear the buffer

            switch (pilihan) {
                // Pake switch-case biar gampang, tiap angka punya aksi yang beda. Kalau pilih 5, program bakal keluar.


                case 1:
                    tambahPrestasi();
                    break;
                case 2:
                    lihatPrestasi();
                    break;
                case 3:
                    analisisPrestasi();
                    break;
                case 4:
                    hapusPrestasi();
                    break;
                case 5:
                    System.out.println("Keluar dari program.");
                    return;
                default:
                    System.out.println("Pilihan tidak valid. Silakan coba lagi.");
            }
        }
    }

    private static void tambahPrestasi() {
        //Ambil input nama & NIM. trim() dipakai buat ngilangin spasi di awal & akhir.

        System.out.print("Masukkan nama mahasiswa: ");
        String nama = scanner.nextLine();
        System.out.print("Masukkan NIM mahasiswa: ");
        String nim = scanner.nextLine();
        System.out.print("Masukkan jenis prestasi: ");
        String jenis = scanner.nextLine();
        System.out.print("Masukkan tingkat prestasi (Lokal/Nasional/Internasional): ");
        String tingkat = scanner.nextLine();
    
        // Validasi tahun
        String tahun = "";
        while (true) {
            System.out.print("Masukkan tahun prestasi (antara 2010 dan 2024): ");
            tahun = scanner.nextLine();
            try {// Cetak jumlah prestasi per tahun
                int tahunInt = Integer.parseInt(tahun);  // Mengubah input menjadi integer
                if (tahunInt >= 2010 && tahunInt <= 2024) {
                    break; // Keluar dari loop jika tahun valid
                } else {
                    System.out.println("Tahun harus antara 2010 dan 2024. Silakan coba lagi.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Input tahun tidak valid. Silakan masukkan angka tahun yang valid.");
            }
        }
    
        Prestasi prestasi = new Prestasi(nama, nim, jenis, tingkat, tahun);
        prestasiList.add(prestasi);
        System.out.println("Prestasi berhasil ditambahkan!");
    }
    

    private static void lihatPrestasi() {
        if (prestasiList.isEmpty()) {
            System.out.println("Tidak ada prestasi yang dicatat.");
            return;
        }
        for (Prestasi prestasi : prestasiList) {
            System.out.println(prestasi);
        }
    }

    private static void analisisPrestasi() {
        if (prestasiList.isEmpty()) {
            System.out.println("Tidak ada prestasi yang dicatat.");
            return;
        }

        System.out.println("Analisis Prestasi berdasarkan tahun:");
        prestasiList.sort((p1, p2) -> p1.tahun.compareTo(p2.tahun)); // Sorting by year

        for (Prestasi prestasi : prestasiList) {
            System.out.println(prestasi);
        }

        // Tambahan analisis berdasarkan jenis prestasi
        System.out.println("\nAnalisis Prestasi berdasarkan jenis:");
        for (String jenis : new String[]{"Lokal", "Nasional", "Internasional"}) {
            System.out.println("\nPrestasi " + jenis + ":");
            boolean found = false;
            for (Prestasi prestasi : prestasiList) {
                if (prestasi.tingkat.equalsIgnoreCase(jenis)) {
                    System.out.println(prestasi);
                    found = true;
                }
            }
            if (!found) {
                System.out.println("Tidak ada prestasi dengan jenis " + jenis + ".");
            }
        }
    }

    private static void hapusPrestasi() {
        //Ambil input NIM atau opsi batal
        System.out.print("Masukkan NIM mahasiswa yang prestasinya ingin dihapus: ");
        String nim = scanner.nextLine();
        boolean found = false;

        for (int i = 0; i < prestasiList.size(); i++) {
            if (prestasiList.get(i).nim.equals(nim)) {
                // Opsi batal biar aman
                prestasiList.remove(i);
                found = true;
                System.out.println("Prestasi berhasil dihapus.");
                break;
            }//Hapus data berdasarkan NIM, kalau ada.
        }

        if (!found) {
            System.out.println("NIM tidak ditemukan.");
        }
    }
}
