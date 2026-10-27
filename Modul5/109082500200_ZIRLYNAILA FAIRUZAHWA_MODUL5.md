# <h1 align="center">Laporan Praktikum Modul 5 - SINGLY LINKED LIST (BAGIAN KEDUA)</h1>

<p align="center">Zirlynaila Fairuzahwa - 109082500200</p>

## Dasar Teori

Singly Linked List merupakan struktur data linear yang terdiri dari node-node yang saling terhubung menggunakan pointer. Setiap node memiliki komponen untuk menyimpan informasi dan alamat node berikutnya. Struktur data ini mendukung operasi pencarian, penambahan, penghapusan, dan pengolahan data melalui perubahan hubungan pointer. Linked list dapat digunakan untuk mengelola data yang membutuhkan penambahan dan penghapusan elemen secara dinamis [1][2].

### A. Searching pada Singly Linked List<br/>

Searching merupakan operasi dasar dalam linked list yang digunakan untuk mencari node berdasarkan nilai informasi yang tersimpan di dalamnya. Proses pencarian dilakukan dengan mengunjungi setiap node mulai dari elemen pertama hingga elemen yang dicari ditemukan atau mencapai akhir list. Operasi ini membantu pelaksanaan operasi lain, seperti penyisipan setelah elemen tertentu (insert after), penghapusan setelah elemen tertentu (delete after), dan pembaruan data (update) [3].

#### 1. Pengertian dan Proses Searching
Searching dilakukan dengan membandingkan nilai info pada setiap node dengan nilai yang dicari. Proses dimulai dari node pertama yang ditunjuk oleh first, kemudian berpindah ke node berikutnya melalui pointer next. Jika nilai yang dicari ditemukan, proses dihentikan dan alamat node tersebut dikembalikan. Apabila nilai tidak ditemukan hingga mencapai akhir list, fungsi mengembalikan Nil atau NULL.

#### 2. Fungsi findElm, fFindElm, dan findBefore
Fungsi findElm(list L, infotype X) digunakan untuk mencari node yang memiliki nilai info sama dengan X. Fungsi mengembalikan alamat node jika ditemukan dan Nil jika tidak ditemukan. Pencarian dilakukan dengan menelusuri list mulai dari L.first melalui pointer next.
<br>
Fungsi fFindElm(list L, address P) digunakan untuk memeriksa apakah alamat node P terdapat dalam list. Fungsi mengembalikan true jika alamat ditemukan dan false jika tidak ditemukan. Sementara itu, fungsi findBefore(list L, address P) digunakan untuk mencari alamat node yang berada tepat sebelum node P. Jika P merupakan elemen pertama, fungsi mengembalikan Nil karena tidak terdapat node sebelumnya. Ketiga fungsi tersebut mendukung proses pencarian dan pengelolaan hubungan antarnode sesuai dengan ADT yang dijelaskan dalam modul.

#### 3. Pointer dan Komponen List dalam Proses Searching
Pointer merupakan variabel yang menyimpan alamat memori suatu node. Dalam Singly Linked List, pointer digunakan untuk mengakses node dan berpindah dari satu elemen ke elemen berikutnya. Komponen first menunjukkan node pertama, info menyimpan nilai data, sedangkan next menunjukkan alamat node berikutnya.
<br>
Pada bahasa C++, operator panah (->) digunakan untuk mengakses anggota struktur melalui pointer. Contohnya, P->info digunakan untuk membaca informasi dari node yang ditunjuk oleh P, sedangkan P->next digunakan untuk berpindah ke node berikutnya. Adapun Nil atau NULL menunjukkan bahwa pointer tidak menunjuk ke node mana pun. Komponen-komponen tersebut membantu proses pencarian dilakukan secara berurutan sampai nilai ditemukan atau akhir list tercapai.

## Guided

### 1. Searching & Update

```C++
source code list.h

#ifndef List_h
#define List_h
#define Nil NULL

#include <iostream>
using namespace std;

struct mahasiswa {
    string nama, nim;
    int umur;
};

typedef mahasiswa dataMahasiswa;
typedef struct node *address;

struct node {
    dataMahasiswa isidata;
    address next;
};

struct linkedlist {
    address first;
};

bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedlist list);
void insertFirst(linkedlist &list, address nodeBaru);
void insertAfter(linkedlist &list, address nodeBaru, address prev);
void insertLast(linkedlist &list, address nodeBaru);

void delFirst(linkedlist &list);
void delLast(linkedlist &list);
void delAfter(linkedlist &list, address nodeHapus, address nodePrev);
int nbList(linkedlist list);
void deleteList(linkedlist &list);

// TAMBAHIN FITUR UPDATE
void updateFirst(linkedlist &list);
void updateLast(linkedlist &list);
void updateAfter(linkedlist list, address &prev);
void updateByNim(linkedlist &list, string nim);

// TAMBAHAN FITUR SEARCHING
address FindNodeByData(linkedlist List, string data);
void FindNodeByAddress(linkedlist list, address node);
void FindNodeByRange(linkedlist list, int nilaiAwal, int nilaiAkhir);

#endif
```

Pada Modul 5 ini, file List.h merupakan pengembangan dari ADT Singly Linked List pada modul sebelumnya dengan menambahkan fitur update dan searching pada data mahasiswa. Kode mendeklarasikan fitur update untuk mengubah data mahasiswa pada posisi atau berdasarkan NIM tertentu, serta fitur searching untuk mencari node berdasarkan data, alamat, maupun rentang nilai umur.

```C++
source code list.cpp

#include "list.h"
#include <iostream>
using namespace std;

// I.S = Initial State / kondisi awal
// F.S = Final State / kondisi akhir

// fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedlist List)
{
    if (List.first == Nil)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// pembuatan linked list kosong
void createList(linkedlist &List)
{
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur)
{
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil */
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

// penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node)
{
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
}

// prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru)
{
    /* I.S. sembarang, P sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev)
{
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil)
    {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    }
    else
    {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru)
{
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen nodeBaru pada akhir list */
    if (isEmpty(List))
    {
        List.first = nodeBaru;
    }
    else
    {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil)
        {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

// prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(linkedlist &List)
{
    /* I.S. list tidak kosong
    F.S. node pertama di list terhapus*/
    address nodeHapus;
    if (isEmpty(List) == false)
    {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    }
    else
    {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List)
{
    /* I.S. list tidak kosong
    F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev;
    if (isEmpty(List) == false)
    {
        nodeHapus = List.first;
        if (nodeHapus->next == Nil)
        {
            List.first->next = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            while (nodeHapus->next != Nil)
            {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    }
    else
    {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev)
{
    /* I.S. list tidak kosng, Prev alamat salah satu elemen list
    F.S. nodeBantu adalah alamat dari Prev→next, menghapus Prev→next dari list */
    if (isEmpty(List) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    { // jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil)
        {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

// prosedur untuk menampilkan isi list
void printList(linkedlist List)
{
    /* I.S. list mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List))
    {
        cout << "List kosong." << endl;
    }
    else
    {
        address nodeBantu = List.first;
        while (nodeBantu != Nil)
        {
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

// function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List)
{
    /* I.S. list sudah ada
       F.S. menampilkan jumlah node didalam list*/
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil)
    {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

// prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedlist &List)
{
    /* I.S. list sudah ada
       F.S. menghapus semua node didalam list*/
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while (nodeBantu != Nil)
    {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}

// prosedur-prosedur untuk melakukan update data node
void updateFirst(linkedlist &list)
{
    if (isEmpty(list))
    {
        cout << "List kosong." << endl;
    }
    else
    {
        dataMahasiswa newData;
        cout << "Masukan nama baru : ";
        cin >> newData.nama;
        cout << "Masukan nim baru : ";
        cin >> newData.nim;
        cout << "Masukan umur baru : ";
        cin >> newData.umur;
        list.first->isidata = newData;
    }
}

void updateLast(linkedlist &list)
{
    if (isEmpty(list))
    {
        cout << "List kosong." << endl;
    }
    else
    {
        dataMahasiswa newData;
        cout << "Masukan nama baru : ";
        cin >> newData.nama;
        cout << "Masukan nim baru : ";
        cin >> newData.nim;
        cout << "Masukan umur baru : ";
        cin >> newData.umur;

        address nodeBantu = list.first;
        while (nodeBantu->next != Nil)
        {
            nodeBantu = nodeBantu->next;
        }

        nodeBantu->isidata = newData;
    }
}

void updateAfter(linkedlist list, address &prev)
{
    if (isEmpty(list))
    {
        cout << "List kosong." << endl;
    }
    else
    {
        dataMahasiswa newData;
        cout << "Masukan nama baru : ";
        cin >> newData.nama;
        cout << "Masukan nim baru : ";
        cin >> newData.nim;
        cout << "Masukan umur baru : ";
        cin >> newData.umur;

        prev->next->isidata = newData;
    }
}

void updateByNim(linkedlist &list, string nim)
{
    if (!isEmpty(list))
    {
        address nodeBantu = FindNodeByData(list, nim);

        if (nodeBantu != Nil)
        {
            dataMahasiswa newData;
            cout << "Masukan nama baru : ";
            cin >> newData.nama;
            cout << "Masukan nim baru : ";
            cin >> newData.nim;
            cout << "Masukan umur baru : ";
            cin >> newData.umur;

            nodeBantu->isidata = newData;
        }
    }
    else
    {
        cout << "List kosong!" << endl;
    }
}

// prosedur-prosedur untuk searching data didalam list
address FindNodeByData(linkedlist List, string data)
{
    /* I.S. list mungkin kosong
       F.S. menampilkan node yang sesuai dengan nama atau nim yang dicari */
    if (isEmpty(List) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        address nodeBantu = List.first;
        int posisi = 0;
        bool found = false;
        while (nodeBantu != Nil)
        {
            posisi++;
            if (nodeBantu->isidata.nama == data || nodeBantu->isidata.nim == data)
            {
                cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
                found = true;
                return nodeBantu;
            }
            nodeBantu = nodeBantu->next;
        }
        if (found == false)
        {
            cout << "Node dengan data " << data << " tidak ditemukan!" << endl;
        }
    }
    cout << endl;
    return Nil;
}

void FindNodeByAddress(linkedlist List, address node)
{
    /* I.S. list mungkin kosong
       F.S. menampilkan node yang sesuai dengan alamat yang dicari */
    if (isEmpty(List) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        address nodeBantu = List.first;
        int posisi = 0;
        bool found = false;
        while (nodeBantu != Nil)
        {
            posisi++;
            if (nodeBantu == node)
            {
                cout << "Node ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Alamat Node : " << nodeBantu << endl;
                cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if (found == false)
        {
            cout << "Node dengan alamat " << node << " tidak ditemukan dalam list!" << endl;
        }
    }
    cout << endl;
}

void FindNodeByRange(linkedlist List, int nilaiAwal, int nilaiAkhir)
{
    /* I.S. list mungkin kosong
       F.S. menampilkan semua node yang memiliki umur di dalam rentang nilaiAwal sampai nilaiAkhir */
    if (isEmpty(List) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        address nodeBantu = List.first;
        int posisi = 0;
        bool found = false;
        cout << "--- Data diatas usia " << nilaiAwal << " dan dibawah " << nilaiAkhir << " ---" << endl;
        while (nodeBantu != Nil)
        {
            posisi++;
            int umur = nodeBantu->isidata.umur;
            if (umur > nilaiAwal && umur < nilaiAkhir)
            {
                cout << "Data ditemukan pada posisi ke-" << posisi << " :" << endl;
                cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
                found = true;
            }
            nodeBantu = nodeBantu->next;
        }
        if (found == false)
        {
            cout << "Tidak ada data node dalam range tersebut!" << endl;
        }
    }
    cout << endl;
}
```

Pada Modul 4, file list.cpp berisi implementasi operasi Singly Linked List sebagai lanjutan dari modul sebelumnya, meliputi pengecekan list kosong, pembuatan list, alokasi dan dealokasi memori, penyisipan, penghapusan, penampilan, serta penghitungan jumlah node. Pada modul 5 ini, file list.cpp ditambahkan fitur update untuk mengubah data mahasiswa pada node pertama, terakhir, setelah node tertentu, atau berdasarkan NIM, serta fitur searching untuk mencari node berdasarkan nama atau NIM, alamat node, dan rentang umur tertentu.

```C++
source code main.cpp

#include "list.h"
#include <iostream>
using namespace std;

int main(){
	linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    updateFirst(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE FIRST ---" << endl;
    printList(List);

    updateLast(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE LAST ---" << endl;
    printList(List);

    updateAfter(List, nodeC);
    cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE AFTER ---" << endl;
    printList(List);

    updateByNim(List, "2211102173");
    cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE BY NIM ---" << endl;
    printList(List);
    
    return 0;
}
```

Pada Modul 4, Program pada file main.cpp membuat list kosong, mengalokasikan lima node data mahasiswa, menyisipkan node menggunakan insertFirst(), insertLast(), dan insertAfter(), kemudian menampilkan isi list serta menghitung jumlah node. Pada modul 5 ini, program ditambah fitur update untuk mengubah data mahasiswa pada node pertama, terakhir, setelah node tertentu, dan berdasarkan NIM menggunakan updateFirst(), updateLast(), updateAfter(), serta updateByNim(), kemudian menampilkan kembali isi list setelah setiap perubahan.

## Unguided

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file "Singlylist.h"

```C++
source code singlylist.h

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

void CreateList(List &L);
address alokasi(infotype x);

void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

address findElm(List L, infotype x);
int totalInfo(List L);

#endif
```

```C++
source code singlylist.cpp

#include "singlylist.h"

void CreateList(List &L) {
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

address findElm(List L, infotype x) {
    address P = L.First;
    while (P != Nil) {
        if (P->info == x) {
            return P;
        }
        P = P->next;
    }
    return Nil;
}

int totalInfo(List L) {
    int total = 0;
    address P = L.First;
    while (P != Nil) {
        total = total + P->info;
        P = P->next;
    }
    return total;
}
```

```C++
source code main.h

#include "singlylist.h"

int main()
{
    List L;
    address P1, P2, P3, P4, P5 = Nil;

    CreateList(L);

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

    address hasil = findElm(L, 8);
    if (hasil != Nil) {
        cout << hasil->info << " ditemukan dalam list" << endl;
    } else {
        cout << "8 tidak ditemukan dalam list" << endl;
    }
    cout << "Total info dari kelima elemen adalah " << totalInfo(L) << endl;
    
    return 0;
}
```

### Output Unguided 1 :

##### Output 1

![Screenshot Output Unguided 1_1](https://github.com/frzhwaa/109082500200_ZirlynailaFairuzahwa_STRUKDAT_MODUL5/blob/main/Modul5/output/soal1.png)

Pada modul sebelumnya, program dibuat untuk membentuk sebuah singly linked list berisi data integer, yaitu dengan membuat list kosong menggunakan CreateList(), membuat node menggunakan alokasi(), menyisipkan lima elemen ke awal list menggunakan insertFirst(), lalu menampilkan isinya menggunakan printInfo(). Program terbagi menjadi tiga file, yaitu singlylist.h untuk deklarasi tipe data dan prototipe, singlylist.cpp untuk implementasi, serta main.cpp untuk menjalankan program. Hasil yang ditampilkan adalah 9 12 8 0 2, yang urutannya terbalik dari urutan pemasukan karena setiap elemen baru selalu ditempatkan di awal list.
<br>
Pada Modul 5 ini, program tersebut dikembangkan dengan menambahkan dua fungsi baru sesuai Latihan 5.2, yaitu findElm() dan totalInfo(). Pertama, pada singlylist.h ditambahkan prototipe address findElm(List L, infotype x) dan int totalInfo(List L). Kedua, pada singlylist.cpp ditambahkan implementasinya. Fungsi findElm() digunakan untuk mencari elemen dengan info tertentu, yaitu dengan menyimpan L.First ke dalam pointer P, kemudian selama P tidak bernilai Nil, program memeriksa apakah P->info sama dengan x. Jika sama, fungsi langsung mengembalikan alamat P, dan jika P sudah berpindah ke P->next sampai habis tanpa menemukan data, fungsi mengembalikan Nil. Fungsi totalInfo() digunakan untuk menghitung jumlah seluruh info, yaitu dengan membuat variabel total bernilai 0, menelusuri list dengan perulangan while dari L.First, menambahkan P->info ke total pada setiap node, lalu mengembalikan nilai total. Ketiga, pada main.cpp, setelah printInfo(L) ditambahkan pemanggilan findElm(L, 8) yang hasilnya disimpan di pointer hasil. Jika hasil tidak bernilai Nil, program menampilkan "8 ditemukan dalam list", dan jika Nil, program menampilkan "8 tidak ditemukan dalam list". Setelah itu, program memanggil totalInfo(L) untuk menampilkan total info seluruh elemen.
<br>
Sebagai contoh, pada list 9, 12, 8, 0, 2, pemanggilan findElm(L, 8) menelusuri node 9, 12, lalu bertemu node 8 sehingga alamat node tersebut dikembalikan dan program menampilkan 8 ditemukan dalam list. Sementara itu, totalInfo(L) menjumlahkan 9 + 12 + 8 + 0 + 2 sehingga menghasilkan 31, dan program menampilkan Total info dari kelima elemen adalah 31. Dengan demikian, program tidak hanya dapat membuat dan menampilkan list, tetapi juga dapat mencari elemen tertentu serta menghitung jumlah seluruh data di dalam list.

## Kesimpulan

Berdasarkan pembahasan materi dan pelaksanaan praktikum Singly Linked List, dapat disimpulkan bahwa Singly Linked List merupakan struktur data linear yang setiap elemennya saling terhubung melalui pointer. Setiap node memiliki komponen info untuk menyimpan data dan next untuk menunjuk node berikutnya. Operasi searching dilakukan dengan menelusuri node mulai dari elemen pertama hingga elemen yang dicari ditemukan atau mencapai akhir list. Fungsi findElm() digunakan untuk mencari elemen berdasarkan nilai informasinya dengan mengembalikan alamat node apabila ditemukan dan Nil apabila tidak ditemukan. Pointer dan hubungan antarnode menjadi bagian penting dalam proses pencarian karena memungkinkan program mengakses setiap elemen secara berurutan.
<br>
Pada praktikum modul 5 ini, program Singly Linked List dikembangkan dari modul sebelumnya dengan menambahkan fungsi findElm() dan totalInfo(). Program terdiri dari tiga file, yaitu singlylist.h untuk deklarasi tipe data dan prototipe fungsi, singlylist.cpp untuk implementasi fungsi, serta main.cpp untuk menjalankan program. List dibentuk menggunakan CreateList(), kemudian lima node dengan nilai 2, 0, 8, 12, dan 9 dibuat menggunakan alokasi() serta dimasukkan ke awal list menggunakan insertFirst(). Hasilnya adalah urutan 9 12 8 0 2 karena setiap elemen baru ditempatkan di awal list. Selanjutnya, fungsi findElm(L, 8) berhasil menemukan elemen bernilai 8, sedangkan fungsi totalInfo() menjumlahkan seluruh nilai elemen, yaitu 9 + 12 + 8 + 0 + 2, sehingga menghasilkan total 31.
<br>
Praktikum ini membantu saya memahami cara kerja pointer dalam proses pencarian elemen pada Singly Linked List serta cara menelusuri setiap node menggunakan perulangan while. Melalui implementasi fungsi findElm(), saya dapat mencari elemen berdasarkan nilai informasi tertentu dan mengetahui apakah elemen tersebut ditemukan dalam list. Selain itu, melalui fungsi totalInfo(), saya dapat menghitung jumlah seluruh nilai informasi pada setiap node.

## Referensi

[1] Fitra, M. R. A., Effendi, A. A. S., & Ramadhani, F. (2025). "Implementasi Python dalam Pengolahan Data Pribadi Mahasiswa Ilmu Komputer Angkatan 23 pada Universitas Negeri Medan Menggunakan Struktur Data Linked List." JATI (Jurnal Mahasiswa Teknik Informatika), 9(1). https://doi.org/10.36040/jati.v9i1.12164
<br>
[2] Sofianti, H. A., Manullang, Y. V., Tampubolon, N. A., Naibaho, L. H., & Gunawan, I. (2025). "Implementasi Struktur Data Array dan Linked List dalam Pengelolaan Data Mahasiswa." Menulis: Jurnal Penelitian Nusantara, 1(6), 871–877. https://doi.org/10.59435/menulis.v1i6.417
<br>
[3] Waluyo P., S. (2021). "Implementasi Algoritma Sequential Searching pada Pembuatan Aplikasi E-Arsip Berbasis Web di UPK Artha Raharja Kecamatan Pacet." COMPUTING | Jurnal Informatika, 8(1), 22–27. https://doi.org/10.55222/computing.v8i01.567
<br>
[4] Modul 5 Struktur Data. "Singly Linked List (Bagian Kedua)." Materi praktikum Struktur Data.