# <h1 align="center">Modul 4  SINGLY LINKED LIST (BAGIAN PERTAMA) </h1>
<p align="center">Gilang Haryo Yudianto- 109082500021</p>

## Dasar Teori

### A. Singly Linked List

Linked list (biasa disebut list saja) adalah salah satu bentuk struktur data berupa serangkaian elemen data yang saling berkait dan bersifat fleksibel karena dapat tumbuh dan mengerut sesuai kebutuhan. Data yang disimpan dapat berupa data tunggal (misalnya nama bertipe string) atau data majemuk berupa record (misalnya data mahasiswa yang terdiri dari nama, NIM, dan alamat). Linked list dapat diimplementasikan menggunakan array maupun pointer, tetapi pointer lebih dipilih karena bersifat dinamis, cocok dengan sifat list yang fleksibel, dan lebih mudah menangani data yang saling berhubungan, sedangkan array bersifat statis dan lebih cocok untuk data dengan jumlah elemen maksimum yang sudah diketahui sejak awal. Singly linked list adalah model linked list yang hanya memiliki satu arah pointer, sehingga hanya memerlukan satu buah pointer, hanya dapat melakukan pembacaan maju, dan node terakhirnya menunjuk ke Nil. Model ini lebih mudah ketika melakukan penyisipan atau penghapusan di tengah list, sedangkan pencarian dilakukan secara sekuensial jika data tidak terurut.

### B. Komponen dan Istilah dalam Singly Linked List

Setiap elemen pada singly linked list terdiri dari dua bagian, yaitu data sebagai informasi utama yang disimpan dan successor sebagai penghubung ke elemen berikutnya. Beberapa istilah penting dalam singly linked list adalah sebagai berikut.

#### 1. First/Head
Pointer pada list yang menunjuk alamat elemen pertama list.

#### 2. Next
Pointer pada elemen yang berfungsi sebagai successor, yaitu penunjuk alamat elemen di depannya.

#### 3. NULL/Nil
Menandakan tidak memiliki nilai, tidak mengacu ke mana pun, atau kosong.

#### 4. Node/Simpul/Elemen
Tempat penyimpanan data pada suatu memori tertentu.

### C. Pembentukan Komponen List

Pembentukan komponen list mencakup empat proses dasar yang masingmasing memiliki fungsi tersendiri.

#### 1. Pembentukan List (CreateList)
Proses membentuk sebuah list baru dengan mengeset nilai awal first menjadi Nil sehingga list dalam keadaan kosong.

#### 2. Pengalokasian Memori (Alokasi)
Proses mengalokasikan memori untuk setiap elemen data dalam list. Pada bahasa C digunakan malloc, sedangkan pada C++ digunakan new yang lebih ringkas.

#### 3. Dealokasi
Proses menghapus memory address yang telah dialokasikan. Pada bahasa C digunakan free, sedangkan pada C++ digunakan delete.

#### 4. Pengecekan List (isEmpty)
Fungsi untuk mengecek apakah list kosong atau tidak, yang mengembalikan nilai true jika list kosong dan false jika tidak kosong.

### D. Operasi Insert

Insert adalah operasi memasukkan elemen baru ke dalam list. Terdapat tiga metode penyisipan.

#### 1. Insert First
Memasukkan elemen pada awal list. Elemen baru dialokasikan, next elemen baru diarahkan ke elemen pertama saat ini, kemudian first diarahkan ke elemen baru.

#### 2. Insert Last
Memasukkan elemen pada akhir list. Elemen baru dialokasikan dengan next bernilai Nil, kemudian next dari elemen terakhir diarahkan ke elemen baru.

#### 3. Insert After
Memasukkan elemen setelah node tertentu yang ditunjuk. Next elemen baru diarahkan ke successor dari node tersebut, kemudian next node tersebut diarahkan ke elemen baru.

### E. Operasi View

View adalah operasi dasar yang menampilkan isi setiap node dengan cara menelusuri list dari elemen pertama hingga terakhir, lalu menampilkan data yang tersimpan pada node tersebut.

### F. Operasi Delete

Delete adalah operasi pengambilan atau penghapusan elemen dari list. Terdapat tiga metode penghapusan serta satu operasi pembebasan memori.

#### 1. Delete First
Menghapus elemen pada awal list. First dipindahkan ke elemen berikutnya, kemudian elemen yang diambil dikembalikan atau didealokasi.

#### 2. Delete Last
Menghapus elemen pada akhir list. Elemen terakhir dicari, lalu next dari elemen sebelumnya diubah menjadi Nil sebelum elemen tersebut dikembalikan atau didealokasi.

#### 3. Delete After
Menghapus node setelah node tertentu. Next node yang ditunjuk dihubungkan langsung ke successor dari node yang dihapus, kemudian node yang dihapus dikembalikan atau didealokasi.

#### 4. Delete Elemen
Operasi untuk menghapus sekaligus membebaskan memori yang dipakai elemen. Fungsi yang biasa dipakai adalah dealokasi(P) untuk membebaskan memori satu elemen dan delAll(L) untuk membebaskan seluruh memori elemen dalam list sehingga list menjadi kosong.

### G. Operasi Update

Update adalah operasi dasar untuk mengubah data yang ada di dalam node pada list. Proses update biasanya diawali dengan pencarian terhadap data yang akan diubah.

### H. Primitif dan Modularisasi ADT List

Semua operasi dasar pada list disebut operasi primitif, yaitu bagian dari ADT list yang disimpan dalam dua file. File header (\*.h) menyimpan tipe data serta prototipe primitif primitif atau fungsi fungsi, sedangkan file body (\*.cpp) berisi realisasi dari prototipe tersebut. Untuk mengakses seluruh primitif, file \*.h cukup di include pada program yang menggunakannya.

## Guided 

### 1. File list.h

```C++
#ifndef LIST_H
#define LIST_H
#define Nil NULL

#include <iostream>
using namespace std;

// Struct data mahasiswa
struct mahasiswa {
    string nama;
    string nim;
    int umur;
};

typedef mahasiswa datamahasiswa;

// Forward declaration
typedef struct node *address;

// Struct node (sebelumnya typo "mode")
struct node {
    datamahasiswa isidata;
    address next;
};

// Struct LinkedList (sebelumnya "linked list" ada spasi & tanpa ;)
struct LinkedList {
    address first;
};

// Prototipe fungsi
bool isEmpty(LinkedList list);
void createList(LinkedList &list);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(LinkedList list);
void insertFirst(LinkedList &list, address nodeBaru);
void insertAfter(LinkedList &list, address nodeBaru, address Prev);
void insertLast(LinkedList &list, address nodeBaru);

void delFirst(LinkedList &list);
void delLast(LinkedList &list);
void delAfter(LinkedList &list, address nodeHapus, address nodePrev);
int nbList(LinkedList list);
void deleteList(LinkedList &list);

#endif
```
kode ini berfokus pada struktur file header C++ yang digunakan untuk mendeklarasikan ADT singly linked list berisi data mahasiswa. Di dalamnya, kita membuat wadah data lewat struct mahasiswa yang menampung tiga informasi penting: nama dan NIM (bertipe string), serta umur (bertipe int), yang kemudian diberi nama alias datamahasiswa menggunakan typedef. Biar struktur kodenya fleksibel saat saling merujuk, kita menggunakan teknik forward declaration typedef struct node *address, sehingga tipe address sudah bisa dikenali sebagai penunjuk (pointer) bahkan sebelum struct node didefinisikan secara utuh. Elemen dari list itu sendiri diwakili oleh struct node, yang berisi variabel isidata (bertipe datamahasiswa) dan pointer next (bertipe address) untuk menyambung ke elemen berikutnya. Sementara itu, struct LinkedList dibuat sangat ringkas karena hanya memiliki satu penunjuk utama bernama first untuk mengunci posisi elemen pertama.

### 2. File list.cpp

```C++
#include "list.h"
#include <iostream>
using namespace std;

// I.S = Initial State / kondisi awal
// F.S = Final State / kondisi akhir

// Fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(LinkedList List) {
    return (List.first == Nil);
}

// pembuatan linked list kosong
void createList(LinkedList &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) {
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru */
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

// penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
    node = Nil;
}

// prosedur insert
void insertFirst(LinkedList &List, address nodeBaru) {
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(LinkedList &List, address nodeBaru, address Prev) {
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(LinkedList &List, address nodeBaru) {
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

// prosedur delete
void delFirst(LinkedList &List) {
    address nodeHapus;
    if (!isEmpty(List)) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(LinkedList &List) {
    address nodeHapus, nodePrev;
    if (!isEmpty(List)) {
        nodeHapus = List.first;
        if (nodeHapus->next == Nil) {
            List.first = Nil;
            dealokasi(nodeHapus);
        } else {
            while (nodeHapus->next != Nil) {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    } else {
        cout << "List kosong" << endl;
    }
}

void delAfter(LinkedList &List, address nodeHapus, address nodePrev) {
    if (isEmpty(List)) {
        cout << "List kosong!" << endl;
    } else {
        if (nodePrev != Nil && nodePrev->next != Nil) {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

// prosedur untuk menampilkan isi list
void printList(LinkedList List) {
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) {
            cout << "Nama : " << nodeBantu->isidata.nama
                 << ", NIM : " << nodeBantu->isidata.nim
                 << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

// Function untuk menampilkan jumlah node didalam list
int nbList(LinkedList List) {
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

// prosedur untuk menghapus semua node didalam list
void deleteList(LinkedList &List) {
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while (nodeBantu != Nil) {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}
```
Kode ini berfokus pada file realisasi (.cpp) yang berisi implementasi nyata dari fungsi-fungsi singly linked list untuk data mahasiswa. Di bagian atas, program memanggil #include "list.h" agar bisa mengenali semua struktur data dan prototipe fungsi yang sudah dibuat sebelumnya, serta memasukkan #include <iostream> untuk keperluan mencetak informasi ke layar. Logika program dimulai dengan hal-hal mendasar: fungsi isEmpty akan menghasilkan nilai true jika bagian List.first masih menunjuk ke Nil, sementara prosedur createList bertugas menyetel List.first ke Nil agar list baru yang kosong terbentuk. Ketika ingin menambahkan elemen baru, fungsi alokasi akan memesan ruang di memori memakai perintah new node, mengisinya dengan data mahasiswa dari parameter, mengarahkan penunjuk next-nya ke Nil, lalu mengembalikan alamat memori tersebut. Sebaliknya, prosedur dealokasi bertugas memutus hubungan next elemen, menghapusnya dari memori memakai delete, dan mengubah pointer tersebut menjadi Nil agar tidak menjadi dangling pointer yang berbahaya bagi sistem memori.

### 3. File main.cpp

```C++
#include "list.h"
#include <iostream>
using namespace std;

int main() {
    LinkedList List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    // Baris "dataMahasiswa mhs;" DIHAPUS karena tidak digunakan

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin",  "221110014",  21);
    nodeC = alokasi("Rizal",  "231110029",  20);
    nodeD = alokasi("Satro",  "211102173",  21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    delFirst(List);
    delLast(List);
    delAfter(List, nodeD, nodeC);

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN HAPUS LIST ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    return 0;
}
```
(main.cpp) ini berfungsi sebagai panggung untuk mendemonstrasikan bagaimana ADT singly linked list digunakan dengan cara memanggil fungsi-fungsi dasar dari file lain. Di baris awal, kode memanggil #include "list.h" agar program utama mengenali tipe data LinkedList, pointer address, serta seluruh operasi yang sudah disiapkan. Di dalam fungsi main, sebuah list bernama List disiapkan bersama lima buah pointer node (nodeA sampai nodeE), yang kemudian diinisialisasi menjadi list kosong lewat perintah createList. Setelah itu, kelima node tersebut dibuat di memori menggunakan fungsi alokasi sambil diisi dengan data nama, NIM, dan umur mahasiswa.


## Unguided 

### 1. program yang dapat menyimpan data mahasiswa


### Singlylist.h
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif  
```
### Singlylist.cpp  
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.First = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}
```

### main.cpp 
```C++
#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5 = Nil;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);
    return 0;
}
```
### Output Unguided 1 :

##### Output 1
![Output 1](https://github.com/Cupa0ng/109082500021_Gilang-Haryo-Yudianto_Pertemuan-5/blob/main/Output_nomor1/Output_nomor1.png)

kode ini mengimplementasikan penerapan ADT singly linked list secara rapi dengan membaginya ke dalam tiga file terpisah. Rancangannya dimulai pada file Singlylist.h (header) yang bertugas mendeklarasikan pondasi data, seperti infotype (bertipe int) sebagai wadah nilai data, pointer address untuk penunjuk elemen, struct ElmList yang menampung variabel info serta pointer next, hingga struct List yang dibekali jangkar utama bernama First. File header yang sudah dipagari include guard (#ifndef, #define, #endif) agar aman dari error saat kompilasi ini juga memuat lima prototipe fungsi dasar: createList, alokasi, dealokasi, printInfo, dan insertFirst. Selanjutnya, seluruh logika di balik fungsi-fungsi tersebut dieksekusi secara nyata di dalam file Singlylist.cpp (body). Di sini, createList akan mengosongkan list dengan menyetel L.First ke Nil, alokasi memesan memori baru lewat perintah new ElmList sekaligus menyetel pointer next-nya ke Nil, dan dealokasi bertugas menghapus elemen menggunakan delete lalu membersihkan sisa pointernya menjadi Nil. Sementara itu, fungsi printInfo bekerja menyisir list hingga ujung untuk mencetak isinya ke layar, dan insertFirst bertugas menyisipkan elemen baru tepat di barisan paling depan. Terakhir, file main.cpp (driver) bertindak sebagai penguji dengan membuat objek list L, menginisialisasinya, lalu mengalokasikan lima angka acak (2, 0, 8, 12, dan 9) untuk dimasukkan berturut-turut memakai insertFirst. Karena karakteristik operasi insert first selalu menumpuk elemen baru di posisi paling depan, urutan angka yang keluar di layar otomatis menjadi terbalik, yakni 9 12 8 0 2 persis seperti visualisasi pada Gambar 4-14 di modul Anda. Melalui pembagian struktur seperti ini, kita bisa melihat dengan jelas bagaimana singly linked list dibangun secara dinamis menggunakan pointer dalam format kode yang modular dan profesional.



### 2. 3 FIle Terpisah 

### Singlylist.h 
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);
int nbList(List L);
void deleteList(List &L);

#endif  
```
### Singlylist.cpp 
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.First = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}

void deleteFirst(List &L, address &P) {
    if (L.First != Nil) {
        P = L.First;
        L.First = P->next;
        P->next = Nil;
    } else {
        P = Nil;
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == Nil) {
        P = Nil;
    } else if (L.First->next == Nil) {
        P = L.First;
        L.First = Nil;
    } else {
        address Q = L.First;
        while (Q->next->next != Nil) {
            Q = Q->next;
        }
        P = Q->next;
        Q->next = Nil;
    }
}

void deleteAfter(address Prec, address &P) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    } else {
        P = Nil;
    }
}

int nbList(List L) {
    int jumlah = 0;
    address P = L.First;
    while (P != Nil) {
        jumlah++;
        P = P->next;
    }
    return jumlah;
}

void deleteList(List &L) {
    address P;
    while (L.First != Nil) {
        deleteFirst(L, P);
        dealokasi(P);
    }
}
```
### main.cpp 
```C++
#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1 = Nil, P2 = Nil, P3 = Nil, P4 = Nil, P5 = Nil;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    address P;

    deleteFirst(L, P);       
    dealokasi(P);

    deleteLast(L, P); 
    dealokasi(P);

    deleteAfter(P4, P);      
    dealokasi(P);

    printInfo(L);
    cout << "Jumlah node : " << nbList(L) << endl;
    cout << endl;

    deleteList(L);
    cout << "- List Berhasil Terhapus -" << endl;
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}
```
### Output Unguided 2 :

##### Output 2
![Output 2](https://github.com/Cupa0ng/109082500021_Gilang-Haryo-Yudianto_Pertemuan-5/blob/main/Output_nomor2/Output_nomor2.png)

kode ini mengimplementasikan penerapan struktur data singly linked list lengkap dengan simulasi berbagai operasi dasarnya. Di balik layar, sistem mengandalkan fungsi createList untuk mengawali antrean kosong, alokasi untuk membooking ruang bagi node baru, dan dealokasi untuk membersihkan node dari memori komputer. Proses manipulasi datanya diperagakan lewat insertFirst yang bertugas menyisipkan node di barisan paling depan, serta trio fungsi penghapus—deleteFirst, deleteLast, dan deleteAfter—yang masing masing bertugas melepaskan node dari posisi awal, akhir, atau tepat setelah node tertentu. Selain itu, ada fungsi nbList untuk menghitung total node, printInfo untuk memamerkan isi data ke layar, serta deleteList yang siap menyapu bersih seluruh isi daftar satu demi satu. Pada fungsi utama (main), program mula mula memasukkan lima buah angka (2, 0, 8, 12, dan 9) menggunakan metode insertFirst. Karena sifat operasinya yang selalu menumpuk di depan, urutan datanya otomatis terbalik menjadi 9 \(\rightarrow \) 12 \(\rightarrow \) 8 \(\rightarrow \) 0 \(\rightarrow \) 2. Setelah itu, ketangguhan fungsi penghapusan diuji: deleteFirst mendepak angka 9 di depan, deleteLast membuang angka 2 di ujung belakang, dan deleteAfter dijalankan untuk melenyapkan data setelah angka 12, yaitu angka 8. Alhasil, barisan data menyusut dan hanya menyisakan 12 \(\rightarrow \) 0. Saat program memanggil printInfo dan nbList, layar akan menampilkan data sisa tersebut beserta jumlah totalnya, yaitu 2. Sebagai penutup, fungsi deleteList dipanggil untuk mengosongkan kembali seluruh memori hingga program berhasil menampilkan pesan sukses bahwa daftar telah bersih dengan jumlah node kembali ke angka 0.

## Kesimpulan
Modul 4 ini mengajak kita menyelami konsep dan operasi dasar singly linked list di C++ dengan memanfaatkan kekuatan pointer. Sederhananya, struktur data ini berbentuk rantai elemen searah yang fleksibel, di mana setiap elemennya menyimpan data dan alamat (next) menuju elemen berikutnya, lalu ditutup oleh penanda Nil di ujung barisan. Kita sengaja memakai pointer karena sifatnya yang dinamis, sehingga ukuran list bisa membesar atau mengecil secara otomatis sesuai kebutuhan—jauh lebih elastis ketimbang array konvensional yang ukurannya sudah dipatok sejak awal. Di awal bab, kita akan berkenalan dengan fondasi dasarnya terlebih dahulu, mulai dari cara membuat list kosong (CreateList), mengecek status keterisiannya (isEmpty), hingga trik mengelola memori komputer lewat proses alokasi (new) dan dealokasi (delete). Setelah pondasi itu kuat, kita akan langsung mempraktikkan operasi manipulasi data, seperti menyisipkan elemen baru di awal, akhir, atau tengah (insert first, last, after), serta menghapus elemen di berbagai posisi tersebut (delete first, last, after) sembari membersihkan sisa memorinya. Tidak ketinggalan, ada juga operasi view untuk menelusuri dan memamerkan seluruh isi data, serta fungsi update untuk mengubah nilai pada elemen tertentu setelah kita berhasil mencarinya. Agar proyek kode kita tidak berantakan dan tetap modular, semua fungsi utama ini akan dibungkus rapi ke dalam bentuk ADT (Abstract Data Type) yang dipisahkan menjadi file header (.h) untuk deklarasi dan file body (.cpp) untuk logika kodenya. Secara keseluruhan, modul ini dirancang sebagai wadah latihan yang seru untuk mengasah


## Referensi
[1] Deitel, P., & Deitel, H. (2017). C++ How to Program (10th ed.). Boston: Pearson.<br>
[2] Liem, I. (2003). Diktat Pemrograman Prosedural. Bandung: Departemen Teknik Informatika Institut Teknologi Bandung.<br>
[3] Laboratorium Informatika Fakultas Informatika Telkom University. (n.d.). Modul 4: Singly Linked List (Bagian Pertama), Modul Praktikum Struktur Data.<br>
[4] cppreference.com. (n.d.). new expression dan delete expression. https://en.cppreference.com/w/cpp/language/new<br>

