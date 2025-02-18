import java.util.ArrayList;
import java.util.Scanner;

public class KafeOrder {
    static class MenuItem {
        String name;
        int price;

        MenuItem(String name, int price) {
            this.name = name;
            this.price = price;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Daftar menu
        MenuItem[] menu = {
            new MenuItem("Nasi Goreng", 20000),
            new MenuItem("Mie Goreng", 15000),
            new MenuItem("Roti Bakar", 12000),
            new MenuItem("Kentang Goreng", 10000),
            new MenuItem("Teh Tarik", 8000),
            new MenuItem("Cappucino", 20000),
            new MenuItem("Chocolate Ice", 25000)
        };

        ArrayList<String> orderList = new ArrayList<>();
        ArrayList<Integer> orderPrices = new ArrayList<>();

        while (true) {
            System.out.println("\n=== Selamat Datang di Kafe ===");
            System.out.println("=== Menu ===");
            for (int i = 0; i < menu.length; i++) {
                System.out.println((i + 1) + ". " + menu[i].name + " - Rp" + menu[i].price);
            }

            System.out.println("\nPilih opsi berikut:");
            System.out.println("1. Tambah Pesanan");
            System.out.println("2. Lihat Daftar Pesanan");
            System.out.println("3. Hitung Total Biaya");
            System.out.println("4. Selesai");

            System.out.print("Masukkan pilihan Anda: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Masukkan nomor menu yang ingin dipesan: ");
                    int menuChoice = scanner.nextInt();

                    if (menuChoice < 1 || menuChoice > menu.length) {
                        System.out.println("Pilihan menu tidak valid.");
                        break;
                    }

                    System.out.print("Masukkan jumlah pesanan: ");
                    int quantity = scanner.nextInt();

                    String order = menu[menuChoice - 1].name + " x" + quantity;
                    int totalPrice = menu[menuChoice - 1].price * quantity;

                    orderList.add(order);
                    orderPrices.add(totalPrice);

                    System.out.println(order + " berhasil ditambahkan ke pesanan.");
                    break;

                case 2:
                    System.out.println("\n=== Daftar Pesanan ===");
                    int subtotal = 0;
                    for (int i = 0; i < orderList.size(); i++) {
                        System.out.println((i + 1) + ". " + orderList.get(i) + " - Rp" + orderPrices.get(i));
                        subtotal += orderPrices.get(i);
                    }
                    System.out.println("Total Biaya Sementara: Rp" + subtotal);
                    break;

                case 3:
                    int total = 0;
                    for (int price : orderPrices) {
                        total += price;
                    }
                    System.out.println("Total biaya seluruh pesanan: Rp" + total);
                    break;

                case 4:
                    System.out.println("Terima kasih telah memesan. Selamat menikmati!");
                    scanner.close();
                    return;

                default:
                    System.out.println("Pilihan tidak valid. Silakan coba lagi.");
            }
        }
    }
}
