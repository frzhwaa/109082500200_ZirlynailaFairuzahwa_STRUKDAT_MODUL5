# <h1 align="center">Laporan Praktikum Modul 4 - SINGLY LINKED LIST (BAGIAN PERTAMA)</h1>

<p align="center">Zirlynaila Fairuzahwa - 109082500200</p>

## Dasar Teori

Linked List merupakan salah satu struktur data linear yang terdiri dari sekumpulan elemen data yang saling terhubung melalui pointer. Setiap elemen dapat menyimpan data tunggal maupun data majemuk dan memiliki hubungan dengan elemen berikutnya. Berbeda dengan array yang memiliki ukuran statis, linked list bersifat fleksibel karena elemen dapat ditambahkan atau dihapus sesuai kebutuhan. Penggunaan linked list sesuai untuk pengelolaan data yang sering mengalami perubahan, seperti penambahan, pencarian, dan penghapusan data mahasiswa [1][2].

### A. Linked List dengan Pointer<br/>

Linked list dengan pointer merupakan struktur data yang menghubungkan elemen-elemen melalui alamat memori yang ditunjuk oleh pointer. Pointer digunakan karena sifatnya yang dinamis sehingga sesuai dengan karakteristik linked list. Setiap elemen dihubungkan melalui alamat yang tersimpan pada pointer, sehingga elemen-elemen tersebut dapat membentuk suatu rangkaian data meskipun tidak harus berada pada lokasi memori yang berurutan.
<br>Penggunaan linked list memberikan fleksibilitas dalam pengelolaan data karena penambahan dan penghapusan elemen dapat dilakukan dengan mengubah hubungan pointer tanpa harus menggeser elemen lain seperti pada array [1].

#### 1. Pengertian dan Karakteristik Linked List
Linked list adalah struktur data yang terdiri dari elemen-elemen yang saling terhubung. Setiap elemen menyimpan informasi dan memiliki penghubung ke elemen lain. Data yang disimpan dapat berupa data tunggal, seperti bilangan bertipe integer, maupun data majemuk, seperti data mahasiswa yang terdiri dari nama dan NIM.
<br>Linked list dapat diimplementasikan menggunakan array maupun pointer. Namun, penggunaan pointer lebih sesuai untuk struktur data yang dinamis karena hubungan antar elemen dapat diatur melalui alamat memori. Karakteristik tersebut membuat linked list lebih fleksibel untuk pengelolaan data yang sering mengalami perubahan [1][2].

#### 2. Pointer dalam Linked List
Pointer merupakan variabel yang digunakan untuk menyimpan alamat memori suatu elemen. Dalam linked list, pointer berfungsi menghubungkan satu elemen dengan elemen lainnya. Pada bahasa C++, pengaksesan komponen melalui pointer dapat menggunakan operator panah (->), sedangkan pengaksesan anggota melalui objek secara langsung dapat menggunakan operator titik (.).
<br>Sebagai contoh, P->info digunakan untuk mengakses data yang disimpan pada elemen yang ditunjuk oleh pointer P, sedangkan P->next digunakan untuk mengakses alamat elemen berikutnya. Dengan demikian, pointer berperan penting dalam membentuk dan mengatur hubungan antar elemen linked list.

#### 3. Jenis-Jenis ADT Linked List
Model ADT yang dipelajari meliputi Singly Linked List, Doubly Linked List, Circular Linked List, Multi Linked List, Stack, Queue, Tree, dan Graph. Setiap model memiliki karakteristik dan penerapan yang berbeda sesuai kebutuhan pengolahan data.
<br>Singly Linked List menggunakan satu arah pointer untuk menghubungkan elemen. Doubly Linked List memiliki hubungan ke elemen sebelumnya dan berikutnya. Circular Linked List menghubungkan elemen terakhir kembali ke elemen awal, sedangkan Multi Linked List memungkinkan elemen memiliki lebih dari satu hubungan. Stack dan Queue merupakan struktur data yang masing-masing menerapkan prinsip LIFO (Last In, First Out) dan FIFO (First In, First Out). Tree dan Graph digunakan untuk merepresentasikan hubungan data yang lebih kompleks.

### B. Singly Linked List<br/>

Singly Linked List merupakan jenis linked list yang setiap elemennya memiliki satu pointer untuk menunjuk ke elemen berikutnya. Struktur ini memungkinkan penelusuran data dilakukan dari elemen pertama hingga elemen terakhir. Setiap elemen terdiri dari komponen info untuk menyimpan data dan next untuk menghubungkan elemen berikutnya.

#### 1. Komponen Singly Linked List
Komponen utama Singly Linked List terdiri dari node, info, next, first, dan Nil. Node merupakan tempat penyimpanan data, info menyimpan informasi, next menunjuk ke elemen berikutnya, sedangkan first menunjuk ke elemen pertama. Nilai Nil atau NULL menunjukkan bahwa pointer tidak menunjuk ke elemen mana pun.

#### 2. Pembentukan dan Pengelolaan List
Pembentukan list dilakukan dengan mengatur first menjadi Nil sehingga list berada dalam kondisi kosong. Pengalokasian memori untuk elemen baru dapat menggunakan operator new, sedangkan pembebasan memori dapat menggunakan delete. Fungsi isEmpty() digunakan untuk memeriksa apakah list kosong atau memiliki elemen.

#### 3. Operasi Dasar Singly Linked List
Operasi dasar Singly Linked List meliputi penyisipan (insert), penampilan data (view), penghapusan (delete), pencarian (searching), dan pembaruan data (update). Penyisipan dapat dilakukan di awal, akhir, atau setelah elemen tertentu. Penghapusan dilakukan dengan mengatur ulang hubungan pointer, sedangkan pencarian dilakukan dengan menelusuri elemen satu per satu. Pembaruan dilakukan dengan mengubah data pada elemen yang telah ditemukan.

## Guided

### 1. SINGLY LINKED LIST

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
void printlist(linkedlist list);
void insertFirst(linkedlist &list, address nodeBaru);
void insertAfter(linkedlist &list, address nodeBaru, address prev);
void insertLast(linkedlist &list, address nodeBaru);

void delFirst(linkedlist &list);
void delLast(linkedlist &list);
void delAfter(linkedlist &list, address nodeHapus, address nodePrev);
int nbList(linkedlist &list);
void deleteList(linkedlist &list);
#endif
```

Code list.h berisi deklarasi tipe data, struktur node, struktur linked list, serta prototipe fungsi dan prosedur yang digunakan dalam Singly Linked List. Struktur mahasiswa menyimpan data nama, NIM, dan umur, sedangkan dataMahasiswa merupakan nama lain dari tipe data mahasiswa. Tipe address digunakan sebagai pointer ke node, struktur node menyimpan informasi mahasiswa pada isidata dan pointer next untuk menunjuk node berikutnya, sedangkan struktur linkedlist memiliki pointer first yang menunjuk node pertama. Selain itu, kode ini mendeklarasikan berbagai operasi untuk membuat, menyisipkan, menghapus, menampilkan, dan menghitung node dalam list.

```C++
source code list.cpp

#include "list.h"
#include <iostream>
using namespace std;

//I.S = Initial State / kondisi awal
//F.S = Final State / kondisi akhir

//fungsi untuk cel apakah list kosong atau tidak
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

//pembuatan linked list kosong
void createList(linkedlist &List)
{
    //I.S sembarang
    //F.S terbentuk list kosong
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur)
{
    //I.S sembarang
    //F.S mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node)
{
    //I.S P terdefinisi
    //F.S memori yang digunakan node dikembalikan ke sistem
    node->next = Nil;
    delete node;
}

// prosedur" untuk insert/menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru)
{
    //I.S sembarang, P sudah dialokasikan
    //F.S menempatkan elemen list (node) pada awal list
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev)
{
    //I.S sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
    //F.S menempatkan elemen (node) sesudah elemen node Prev
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
    //I.S sembarang, nodeBaru sudah dialokasikan
    //F.S menempatkan elemen nodeBaru pada akhir list
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

// prosedur" untuk delete / menghapus node yang ada didalam list
void deleteFirst(linkedlist &List)
{
    //I.S list tidak kosong
    //F.S node pertama di list terhapus
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
    //I.S list tidak kosong
    //F.S node terakhir di list terhapus
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
        cout << "List kosong!" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev)
{
    //I.S list tidak kosong, Prev alamat salah satu link
    //F.S nodeBantu adalah alamat dari Prev->next, menghapus Prev->next dari list
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
    //I.S list mungkin kosong
    //F.S jika list tidak kosong menampilkan semua info yang ada pada list
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
    // I.S. list sudah ada
    // F.S. menghapus semua node didalam list
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while (nodeBantu != Nil)
    {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus." << endl;
}
```

Code list.cpp berisi implementasi fungsi dan prosedur untuk mengelola Singly Linked List. Fungsi isEmpty() memeriksa apakah list kosong dengan mengecek nilai first, sedangkan createList() membuat list kosong dengan mengatur first menjadi Nil. Fungsi alokasi() membuat node baru dan mengisi data mahasiswa, sementara dealokasi() membebaskan memori node menggunakan delete. Prosedur insertFirst(), insertAfter(), dan insertLast() digunakan untuk menyisipkan node pada awal, setelah node tertentu, dan akhir list. Prosedur deleteFirst(), delLast(), dan delAfter() digunakan untuk menghapus node pada posisi yang ditentukan. Selanjutnya, printList() menampilkan seluruh data mahasiswa dengan menelusuri list, nbList() menghitung jumlah node, dan deleteList() menghapus seluruh node hingga list kembali kosong.

```C++
source code main.cpp

#include "list.h"
using namespace std;

int main()
{
    linkedlist List;
    address nodeA = Nil, nodeB = Nil, nodeC = Nil, nodeD = Nil, nodeE = Nil;
    createList(List);

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "221110014", 21);
    nodeC = alokasi("Rizal", "231110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printlist(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    delFirst(List);             
    delLast(List);              
    delAfter(List, Nil, nodeC); 

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printlist(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List); 
    cout << "jumlah node : " << nbList(List) << endl;

    return 0;
}
```

Code main.cpp merupakan program utama yang menjalankan operasi Singly Linked List menggunakan fungsi dan prosedur yang telah dideklarasikan pada list.h dan diimplementasikan pada list.cpp. Program membuat list kosong menggunakan createList(), kemudian membuat lima node berisi data mahasiswa melalui fungsi alokasi(). Node-node tersebut dimasukkan ke dalam list menggunakan insertFirst(), insertLast(), dan insertAfter(). Setelah proses penyisipan, program menampilkan isi list menggunakan printlist() dan menghitung jumlah node dengan nbList(). Selanjutnya, program menghapus node pertama, node terakhir, dan node setelah nodeC, lalu menampilkan kembali isi list dan jumlah nodenya. Terakhir, deleteList() digunakan untuk menghapus seluruh node dan nbList() dipanggil kembali untuk memeriksa jumlah node setelah list dikosongkan.

## Unguided

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h”

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
    return 0;
}
```

### Output Unguided 1 :

##### Output 1

![Screenshot Output Unguided 1_1](https://github.com/frzhwaa/109082500200_ZirlynailaFairuzahwa_STRUKDAT_MODUL4/blob/main/Modul4/output/soal1.png)

Program tersebut digunakan untuk membuat sebuah singly linked list yang menyimpan data integer, menyisipkan lima elemen ke awal list, lalu menampilkan seluruh isi list. Program dibagi menjadi tiga file, yaitu singlylist.h yang berisi deklarasi tipe data dan prototipe fungsi serta prosedur, singlylist.cpp yang berisi implementasinya, serta main.cpp yang digunakan untuk menjalankan program. Pertama, pada singlylist.h dibuat tipe infotype sebagai integer, tipe address sebagai pointer ke ElmList, struct ElmList sebagai node yang berisi info untuk menyimpan data dan next untuk menunjuk node berikutnya, serta struct List yang berisi First sebagai penunjuk elemen pertama. Selanjutnya, prosedur CreateList() digunakan untuk membuat list kosong dengan mengisi L.First dengan Nil. Setelah itu, fungsi alokasi() digunakan untuk membuat sebuah node baru, yaitu dengan meminta memori menggunakan new ElmList, mengisi P->info dengan nilai x, mengisi P->next dengan Nil, dan terakhir mengembalikan alamat P. Prosedur dealokasi() digunakan untuk mengembalikan memori node ke sistem menggunakan delete, kemudian P diisi Nil agar tidak menunjuk memori yang sudah dihapus. Prosedur insertFirst() digunakan untuk menyisipkan node di awal list, yaitu dengan mengisi P->next dengan L.First agar node baru menunjuk ke elemen pertama yang lama, kemudian mengisi L.First dengan P agar node baru menjadi elemen pertama. Prosedur printInfo() digunakan untuk menampilkan isi list dengan perulangan while, yaitu dengan menyimpan L.First ke dalam pointer P, kemudian selama P tidak bernilai Nil, program menampilkan P->info dan memindahkan P ke P->next. Pada main.cpp, program membuat list L dan lima pointer P1 sampai P5, kemudian memanggil CreateList(L). Setelah itu, setiap nilai 2, 0, 8, 12, dan 9 dialokasikan menggunakan alokasi() dan disisipkan menggunakan insertFirst(). Setelah seluruh proses selesai, program memanggil printInfo(L) untuk menampilkan isi list.

Sebagai contoh, setelah CreateList(L) dipanggil, list masih kosong karena L.First bernilai Nil. Ketika alokasi(2) dan insertFirst(L, P1) dipanggil, list berisi 2. Ketika alokasi(0) dan insertFirst(L, P2) dipanggil, node 0 ditempatkan di depan sehingga list menjadi 0, 2. Proses yang sama dilakukan untuk nilai 8 sehingga list menjadi 8, 0, 2, kemudian nilai 12 sehingga list menjadi 12, 8, 0, 2, dan terakhir nilai 9 sehingga list menjadi 9, 12, 8, 0, 2. Hasilnya, ketika printInfo(L) dijalankan, program menampilkan 9 12 8 0 2, yang urutannya terbalik dari urutan pemasukan data karena setiap elemen baru selalu ditempatkan di awal list. Dengan demikian, program berhasil membuat list kosong, mengalokasikan node, menyisipkan node di awal list menggunakan pointer, serta menampilkan seluruh isi list.

## Kesimpulan

Pada praktikum Modul 4 Singly Linked List (Bagian Pertama), dapat disimpulkan bahwa materi pada modul ini membahas mengenai konsep linked list, penggunaan pointer, struktur node, serta operasi dasar dalam Singly Linked List menggunakan bahasa C++. Singly Linked List merupakan struktur data dinamis yang setiap nodenya memiliki bagian untuk menyimpan informasi dan pointer next untuk menunjuk node berikutnya. Penerapan ADT dilakukan dengan memisahkan program ke dalam file header (.h), file implementasi (.cpp), dan program utama (main.cpp) agar program lebih terstruktur dan modular.

Melalui praktikum yang telah dikerjakan, saya memahami penerapan Singly Linked List untuk menyimpan dan mengelola data. Pada program pertama, ADT Singly Linked List diterapkan untuk menyimpan data mahasiswa berupa nama, NIM, dan umur, serta melakukan operasi pembuatan list, alokasi memori, penyisipan node di awal, tengah, dan akhir list, penghapusan node, penampilan data, serta penghitungan jumlah node. Pada program kedua, Singly Linked List diterapkan untuk menyimpan data bertipe integer dengan membuat list kosong, mengalokasikan lima node bernilai 2, 0, 8, 12, dan 9, kemudian menyisipkannya menggunakan insertFirst() dan menampilkan isi list menggunakan printInfo(). Hasilnya adalah 9 12 8 0 2 karena setiap elemen baru ditempatkan di awal list.

Praktikum ini membantu saya memahami cara kerja pointer dalam menghubungkan node, pengelolaan memori melalui alokasi dan dealokasi, serta penerapan operasi dasar Singly Linked List dalam bahasa C++. Selain memahami teori, saya juga dapat menerapkan konsep tersebut untuk membuat list, menyisipkan dan menghapus elemen, menampilkan data, serta menghitung jumlah node sesuai dengan kebutuhan program.

## Referensi

[1] Sofianti, H. A., Manullang, Y. V., Tampubolon, N. A., Naibaho, L. H., & Gunawan, I. (2025). "Implementasi Struktur Data Array dan Linked List dalam Pengelolaan Data Mahasiswa." Menulis: Jurnal Penelitian Nusantara, 1(6), 871–877. https://doi.org/10.59435/menulis.v1i6.417
<br>
[2] Fitra, M. R. A., Effendi, A. A. S., & Ramadhani, F. (2025). "Implementasi Python dalam Pengolahan Data Pribadi Mahasiswa Ilmu Komputer Angkatan 23 pada Universitas Negeri Medan Menggunakan Struktur Data Linked List." JATI (Jurnal Mahasiswa Teknik Informatika), 9(1). https://doi.org/10.36040/jati.v9i1.12164
<br>
[3] Modul 4 Struktur Data. "Singly Linked List (Bagian Pertama)," Materi praktikum Struktur Data.