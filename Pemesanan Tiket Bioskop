#include <iostream>
#include <vector>
#include <list>
#include <string>
#include <cstdlib>

#ifdef _WIN32
   #include <windows.h>
#else
   #include <unistd.h>
#endif

using namespace std;

// Fungsi untuk membersihkan layar
void clearScreen() {
#ifdef _WIN32
   system("cls");
#else
   system("clear");
#endif
}

// Fungsi untuk menambahkan jeda
void delay(int milliseconds) {
#ifdef _WIN32
   Sleep(milliseconds);
#else
   usleep(milliseconds * 1000);
#endif
}

// Struktur untuk menyimpan data pengguna
struct User {
   string username;
   string password;
};

// Struktur untuk menyimpan data film
struct Movie {
   string title;
   string time;
   vector<vector<bool>> seats;
};

// Kelas untuk menangani sistem pemesanan tiket
class TicketSystem {
private:
   vector<User> users;
   list<Movie> movies;
   User* loggedInUser = nullptr;

public:
   void registerUser(const string& username, const string& password) {
       clearScreen();
       for (const auto& user : users) {
           if (user.username == username) {
               cout << "Username sudah terdaftar. Silakan pilih username lain.\n";
               return;
           }
       }
       users.push_back({username, password});
       cout << "Registrasi";
       for (int i = 0; i < 3; ++i) {
           delay(500);
           cout << ".";
       }
       cout << " berhasil!\n";
   }

   void loginUser(const string& username, const string& password) {
       clearScreen();
       for (auto& user : users) {
           if (user.username == username && user.password == password) {
               loggedInUser = &user;
               cout << "Login";
               for (int i = 0; i < 3; ++i) {
                   delay(500);
                   cout << ".";
               }
               cout << " berhasil!\n";
               return;
           }
       }
       cout << "Username atau password salah.\n";
   }

   void logoutUser() {
       clearScreen();
       loggedInUser = nullptr;
       cout << "Logout";
       for (int i = 0; i < 3; ++i) {
           delay(500);
           cout << ".";
       }
       cout << " berhasil!\n";
   }

   void addMovie(const string& title, const string& time) {
       clearScreen();
       movies.push_back({title, time, vector<vector<bool>>(10, vector<bool>(10, false))});
       cout << "Film berhasil ditambahkan!\n";
   }
 void showMovies() {
        clearScreen();
        cout << "Jadwal Film:\n";
        for (const auto& movie : movies) {
            cout << "Judul: " << movie.title << " | Waktu: " << movie.time << "\n";
        }
    }

    void chooseSeat(const string& title, const string& time) {
        clearScreen();
        for (auto& movie : movies) {
            if (movie.title == title && movie.time == time) {
                cout << "Pilih kursi dengan memasukkan nomor baris dan kolom (misal 3 4 untuk baris 3 kolom 4):\n";
                cout << "Kursi tersedia [O], Kursi terpesan [X]\n\n";
                cout << "  ";
                for (size_t j = 0; j < movie.seats[0].size(); ++j) {
                    cout << " " << j << " ";
                }
                cout << endl;

                for (size_t i = 0; i < movie.seats.size(); ++i) {
                    cout << i << " ";
                    for (size_t j = 0; j < movie.seats[i].size(); ++j) {
                        cout << " [" << (movie.seats[i][j] ? "X" : "O") << "] ";
                    }
                    cout << endl;
                }

                int row, col;
                cout << "\nMasukkan nomor baris: ";
                cin >> row;
                cout << "Masukkan nomor kolom: ";
                cin >> col;

                if (row >= 0 && row < movie.seats.size() && col >= 0 && col < movie.seats[row].size() && !movie.seats[row][col]) {
                    movie.seats[row][col] = true;
                    cout << "Kursi";
                    for (int i = 0; i < 3; ++i) {
                        delay(500);
                        cout << ".";
                    }
                    cout << " berhasil dipilih!\n";
                } else {
                    cout << "Kursi tidak valid atau sudah dipesan.\n";
                }
                return;
            }
        }
        cout << "Film tidak ditemukan.\n";
    }

    void confirmBooking() {
        clearScreen();
        if (loggedInUser) {
            cout << "Tiket berhasil dipesan oleh " << loggedInUser->username << "!\n";
            cout << "Tampilkan tiket dengan barcode.\n";
        } else {
            cout << "Harap login terlebih dahulu.\n";
        }
    }
};

int main() {
   TicketSystem system;

   // Menambahkan beberapa film ke dalam sistem
   system.addMovie("The Matrix", "12:00");
   system.addMovie("Inception", "14:30");
   system.addMovie("Interstellar", "17:00");
   system.addMovie("Fight Club", "14:30");
   system.addMovie("The Dark Knight", "19:00");
   system.addMovie("Pulp Fiction", "21:30");
   system.addMovie("Forrest Gump", "10:00");
   system.addMovie("The Shawshank Redemption", "12:30");
   system.addMovie("Gladiator", "15:00");
   system.addMovie("The Godfather", "18:00");

   while (true) {
       clearScreen();
       cout << "Menu:\n";
       cout << "1. Registrasi\n";
       cout << "2. Login\n";
       cout << "3. Tambah Film\n";
       cout << "4. Lihat Jadwal Film\n";
       cout << "5. Pilih Kursi\n";
       cout << "6. Konfirmasi Pemesanan\n";
       cout << "7. Logout\n";
       cout << "8. Keluar\n";

       int choice;
       cin >> choice;

       if (choice == 8) break;

       string username, password, title, time;
       switch (choice) {
           case 1:
               cout << "Masukkan username: ";
               cin >> username;
               cout << "Masukkan password: ";
               cin >> password;
               system.registerUser(username, password);
               break;
           case 2:
               cout << "Masukkan username: ";
               cin >> username;
               cout << "Masukkan password: ";
               cin >> password;
               system.loginUser(username, password);
               break;
           case 3:
               cout << "Masukkan judul film: ";
               cin.ignore();
               getline(cin, title);
               cout << "Masukkan waktu tayang: ";
               getline(cin, time);
               system.addMovie(title, time);
               break;
           case 4:
               system.showMovies();
               break;
           case 5:
               cout << "Masukkan judul film: ";
               cin.ignore();
               getline(cin, title);
               cout << "Masukkan waktu tayang: ";
               getline(cin, time);
               system.chooseSeat(title, time);
               break;
           case 6:
               system.confirmBooking();
               break;
           case 7:
               system.logoutUser();
               break;
           default:
               cout << "Pilihan tidak valid.\n";
               break;
       }

       cout << "Tekan Enter untuk melanjutkan...";
       cin.ignore();
       cin.get();
   }

   return 0;
}
