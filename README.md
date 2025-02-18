import java.util.ArrayList;                // Mengimpor kelas ArrayList dari paket java.util.
import java.util.Scanner;                 // Mengimpor kelas Scanner dari paket java.util.

public class KafeOrder {                  // Mendeklarasikan kelas KafeOrder.
    static class MenuItem {               // Mendeklarasikan kelas statis MenuItem.
        String name;                      // Mendeklarasikan atribut name bertipe String.
        int price;                        // Mendeklarasikan atribut price bertipe int.

        MenuItem(String name, int price) {// Konstruktor untuk menginisialisasi name dan price.
            this.name = name;
            this.price = price;
        }
    }

    public static void main(String[] args) {         // Metode main, titik masuk program.
        Scanner scanner = new Scanner(System.in);   // Membuat objek Scanner untuk membaca input.

        // Daftar menu
        MenuItem[] menu = {                         // Membuat array objek MenuItem dengan daftar menu.
            new MenuItem("Nasi Goreng", 20000),
            new MenuItem("Mie Goreng", 15000),
            new MenuItem("Roti Bakar", 12000),
            new MenuItem("Kentang Goreng", 10000),
            new MenuItem("Teh Tarik", 8000),
            new MenuItem("Cappucino", 20000),
            new MenuItem("Chocolate Ice", 25000)
        };

        ArrayList<String> orderList = new ArrayList<>();   // Membuat ArrayList untuk menyimpan nama pesanan.
        ArrayList<Integer> orderPrices = new ArrayList<>(); // Membuat ArrayList untuk menyimpan harga pesanan.

        while (true) {                                     // Loop tak terbatas.
            System.out.println("\n=== Selamat Datang di Kafe ==="); // Mencetak pesan selamat datang.
            System.out.println("=== Menu ===");                      // Mencetak judul menu.
            for (int i = 0; i < menu.length; i++) {                  // Loop untuk menampilkan menu.
                System.out.println((i + 1) + ". " + menu[i].name + " - Rp" + menu[i].price);
            }

            System.out.println("\nPilih opsi berikut:");             // Mencetak opsi yang tersedia.
            System.out.println("1. Tambah Pesanan");
            System.out.println("2. Lihat Daftar Pesanan");
            System.out.println("3. Hitung Total Biaya");
            System.out.println("4. Selesai");

            System.out.print("Masukkan pilihan Anda: ");              // Membaca pilihan pengguna.
            int choice = scanner.nextInt();

            switch (choice) {                                        // Menjalankan aksi berdasarkan pilihan pengguna.
                case 1:
                    System.out.print("Masukkan nomor menu yang ingin dipesan: ");
                    int menuChoice = scanner.nextInt();

                    if (menuChoice < 1 || menuChoice > menu.length) { // Memeriksa validitas nomor menu.
                        System.out.println("Pilihan menu tidak valid.");
                        break;
                    }

                    System.out.print("Masukkan jumlah pesanan: ");
                    int quantity = scanner.nextInt();

                    String order = menu[menuChoice - 1].name + " x" + quantity;  // Membuat string pesanan.
                    int totalPrice = menu[menuChoice - 1].price * quantity;    // Menghitung total harga.

                    orderList.add(order);                         // Menambahkan pesanan ke orderList.
                    orderPrices.add(totalPrice);                  // Menambahkan harga ke orderPrices.

                    System.out.println(order + " berhasil ditambahkan ke pesanan.");
                    break;

                case 2:
                    System.out.println("\n=== Daftar Pesanan ===");  // Mencetak daftar pesanan.
                    int subtotal = 0;
                    for (int i = 0; i < orderList.size(); i++) {
                        System.out.println((i + 1) + ". " + orderList.get(i) + " - Rp" + orderPrices.get(i));
                        subtotal += orderPrices.get(i);
                    }
                    System.out.println("Total Biaya Sementara: Rp" + subtotal);  // Mencetak subtotal.
                    break;

                case 3:
                    int total = 0;
                    for (int price : orderPrices) {
                        total += price;
                    }
                    System.out.println("Total biaya seluruh pesanan: Rp" + total);  // Mencetak total biaya.
                    break;

                case 4:
                    System.out.println("Terima kasih telah memesan. Selamat menikmati!");  // Mencetak pesan terima kasih.
                    scanner.close();                                 // Menutup Scanner.
                    return;                                          // Mengakhiri program.

                default:
                    System.out.println("Pilihan tidak valid. Silakan coba lagi.");  // Mencetak pesan pilihan tidak valid.
            }
        }
    }
}
