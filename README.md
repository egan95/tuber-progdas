#include <iostream>
#include <cstdlib>
#include <stdio.h>
#include <conio.h>
#include <windows.h>
#include <string.h>
#include <time.h>
#define user "kelompok4"
#define pass "kelompok4"
#define delay Sleep
#define month 1
#define year 2014
using namespace std;

COORD coordinate;
void gotoxy(int x,int y){
    coordinate.X=x; coordinate.Y=y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),coordinate);
}

void setcolor (unsigned short color) 
{ 
HANDLE hCon = GetStdHandle(STD_OUTPUT_HANDLE);
SetConsoleTextAttribute(hCon,color);
} 
typedef struct {
	int g_pokok;
	int t_anak;
	int total_gaji;
	int gaji_semua;
} s_gaji;

//struct data pegawai
typedef struct {
	char nip[12];
	char nama[51];
	char alamat[51];
	char golongan[20];
	char jabatan[20];
	char status[20];
	s_gaji gaji;
	int jml_anak;
	char bulan_masuk[15];
	int total_banyak_bulan;
	int tahun_masuk;
} s_pegawai;

//procedure menu utama
void menu_u(int *menu_utama) {
	gotoxy(62,4);cout<<"MENU UTAMA"<<endl;
	gotoxy(51,5);cout<<"================================"<<endl;
	gotoxy(51,7);cout<<"+------------------------------+"<<endl;
	gotoxy(51,8);cout<<"|                              |"<<endl;
	gotoxy(51,9);cout<<"|  1. Input Data Pegawai       |"<<endl;
	gotoxy(51,10);cout<<"|                              |"<<endl;
	gotoxy(51,11);cout<<"|  2. Output Data Pegawai      |"<<endl;
	gotoxy(51,12);cout<<"|                              |"<<endl;
	gotoxy(51,13);cout<<"|  3. Output Data Penggajian   |"<<endl;
	gotoxy(51,14);cout<<"|                              |"<<endl;
	gotoxy(51,15);cout<<"|  0. Keluar                   |"<<endl;
	gotoxy(51,16);cout<<"|                              |"<<endl;
	gotoxy(51,17);cout<<"+------------------------------+"<<endl;
	gotoxy(51,18);cout<<"|                              |"<<endl;
	gotoxy(51,19);cout<<"|      Pilih Menu :            |";
	gotoxy(51,20);cout<<"|                              |"<<endl;
	gotoxy(51,21);cout<<"+------------------------------+"<<endl;
	gotoxy(71,19);cin>>*menu_utama;
}

//procedure sub menu data penggajian
void menu_penggajian(int *menu_sub_penggajian) {
	gotoxy(59,4);cout<<"MENU DATA PENGGAJIAN"<<endl;
	gotoxy(51,5);cout<<"===================================="<<endl;
	gotoxy(51,7);cout<<"+----------------------------------+"<<endl;
	gotoxy(51,8);cout<<"|                                  |"<<endl;	
	gotoxy(51,9);cout<<"|  1. Tampilkan Data Gaji Pegawai  |"<<endl;
	gotoxy(51,10);cout<<"|                                  |"<<endl;
	gotoxy(51,11);cout<<"|  2. Cari Data Gaji Pegawai       |"<<endl;
	gotoxy(51,12);cout<<"|                                  |"<<endl;
	gotoxy(51,13);cout<<"|  3. Statistik Gaji Pegawai       |"<<endl;
	gotoxy(51,14);cout<<"|                                  |"<<endl;
	gotoxy(51,15);cout<<"|  0. Kembali ke Menu Utama        |"<<endl;
	gotoxy(51,16);cout<<"|                                  |"<<endl;
	gotoxy(51,17);cout<<"+----------------------------------+"<<endl;
	gotoxy(51,18);cout<<"|                                  |"<<endl;
	gotoxy(51,19);cout<<"|      Pilih Menu :                |";
	gotoxy(51,20);cout<<"|                                  |"<<endl;
	gotoxy(51,21);cout<<"+----------------------------------+"<<endl;
	gotoxy(71,19);cin>>*menu_sub_penggajian;
}

//procedure sub menu tampilkan data gaji karyawan
void data_gaji_pegawai(int *menu_data_gaji_p) {
	gotoxy(61,4);cout<<"MENU URUT DATA GAJI"<<endl;
	gotoxy(51,5);cout<<"========================================="<<endl;
	gotoxy(51,7);cout<<"+---------------------------------------+"<<endl;
	gotoxy(51,8);cout<<"|                                       |"<<endl;	
	gotoxy(51,9);cout<<"|  1. Urutkan Berdasarkan NIP           |"<<endl;
	gotoxy(51,10);cout<<"|                                       |"<<endl;
	gotoxy(51,11);cout<<"|  2. Urutkan Berdasarkan Gaji          |"<<endl;
	gotoxy(51,12);cout<<"|                                       |"<<endl;
	gotoxy(51,13);cout<<"|  0. Kembali Ke Menu Data Penggajian   |"<<endl;
	gotoxy(51,14);cout<<"|                                       |"<<endl;
	gotoxy(51,15);cout<<"+---------------------------------------+"<<endl;
	gotoxy(51,16);cout<<"|                                       |"<<endl;
	gotoxy(51,17);cout<<"|         Pilih Menu :                  |";
	gotoxy(51,18);cout<<"|                                       |"<<endl;
	gotoxy(51,19);cout<<"+---------------------------------------+"<<endl;
	gotoxy(74,17);cin>>*menu_data_gaji_p;
}
//procedure sub menu cari data pegawai
void search_pegawai(int *menu_search_pegawai) {
	gotoxy(57,4);cout<<"MENU SEARCH DATA PEGAWAI"<<endl;
	gotoxy(49,5);cout<<"========================================="<<endl;
	gotoxy(49,7);cout<<"+---------------------------------------+"<<endl;
	gotoxy(49,8);cout<<"|                                       |"<<endl;	
	gotoxy(49,9);cout<<"|  1. Cari Berdasarkan NIP              |"<<endl;
	gotoxy(49,10);cout<<"|                                       |"<<endl;
	gotoxy(49,11);cout<<"|  2. Cari Berdasarkan Nama             |"<<endl;
	gotoxy(49,12);cout<<"|                                       |"<<endl;
	gotoxy(49,13);cout<<"|  0. Kembali Ke Menu Data Penggajian   |"<<endl;
	gotoxy(49,14);cout<<"|                                       |"<<endl;
	gotoxy(49,15);cout<<"+---------------------------------------+"<<endl;
	gotoxy(49,16);cout<<"|                                       |"<<endl;
	gotoxy(49,17);cout<<"|         Pilih Menu :                  |";
	gotoxy(49,18);cout<<"|                                       |"<<endl;
	gotoxy(49,19);cout<<"+---------------------------------------+"<<endl;
	gotoxy(72,17);cin>>*menu_search_pegawai;
}

//iinisialisasi data pegawai
void inisialisasi(s_pegawai data_pegawai[50]) {
	strcpy(data_pegawai[0].nip,"1023");	
	strcpy(data_pegawai[0].nama,"Edi Gunawan");
	strcpy(data_pegawai[0].alamat,"Jl.Pahlawan");
	strcpy(data_pegawai[0].golongan,"1B");
	strcpy(data_pegawai[0].jabatan,"Guru");
	strcpy(data_pegawai[0].bulan_masuk,"November");
	data_pegawai[0].tahun_masuk = 2011;
	data_pegawai[0].total_banyak_bulan = 26;
	strcpy(data_pegawai[0].status,"Menikah");
	data_pegawai[0].jml_anak=1;
	data_pegawai[0].gaji.g_pokok=4500000;
	data_pegawai[0].gaji.t_anak=250000;
	data_pegawai[0].gaji.total_gaji=4750000;
	
	strcpy(data_pegawai[1].nip,"1022");	
	strcpy(data_pegawai[1].nama,"Jhon");
	strcpy(data_pegawai[1].alamat,"Jl.DIpatiukur");
	strcpy(data_pegawai[1].golongan,"1C");
	strcpy(data_pegawai[1].jabatan,"Guru");
	strcpy(data_pegawai[1].bulan_masuk,"Juli");
	data_pegawai[1].tahun_masuk = 2012;
	data_pegawai[1].total_banyak_bulan = 18;
	strcpy(data_pegawai[1].status,"Menikah");
	data_pegawai[1].jml_anak=2;
	data_pegawai[1].gaji.g_pokok=3500000;
	data_pegawai[1].gaji.t_anak=500000;
	data_pegawai[1].gaji.total_gaji=4000000;
}
//fungsi input pegawai
s_pegawai i_pegawai() {
	s_pegawai data_pegawai;
	int golongan;
	int jabatan;
	int status;
	int bulan;
	int tahun;
	int total_bulan;
	int temp;
	int panjang;
	gotoxy(58,4);cout<<"INPUT DATA PEGAWAI"<<endl;
	gotoxy(56,5);cout<<"======================"<<endl;
	gotoxy(52,8);cout<<(char)26<<" NIP               : ";fflush(stdin);cin.get(data_pegawai.nip,11);
	//validasi untuk nip harus <= 4 karakter
	panjang = strlen(data_pegawai.nip);
	while (panjang != 4) {
		setcolor(3);
		gotoxy(69,10);cout<<"Panjang NIP Yang Diinputkan"<<endl;
		gotoxy(69,11);cout<<"Harus 4 Karakter";
		getch();
		gotoxy(69,10);cout<<"                                   "<<endl;
		gotoxy(69,11);cout<<"                                   ";
		gotoxy(74,8);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,8);cout<<(char)26<<" NIP               : ";fflush(stdin);cin.get(data_pegawai.nip,11);
		panjang = strlen(data_pegawai.nip);
	}
	gotoxy(52,10);cout<<(char)26<<" Nama              : ";fflush(stdin);cin.get(data_pegawai.nama,50);

	//validasi untuk nama harus <= 13 karakter
	panjang = strlen(data_pegawai.nama);
	while (panjang > 21) {
		setcolor(3);
		gotoxy(69,12);cout<<"Panjang Nama Yang Diinputkan"<<endl;
		gotoxy(69,13);cout<<"Tidak Boleh Lebih Dari 21 Karakter";
		getch();
		gotoxy(69,12);cout<<"                                   "<<endl;
		gotoxy(69,13);cout<<"                                   ";
		gotoxy(74,10);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,10);cout<<(char)26<<" Nama              : ";fflush(stdin);cin.get(data_pegawai.nama,50);
		panjang = strlen(data_pegawai.nama);
	}
	gotoxy(52,12);cout<<(char)26<<" Alamat            : ";fflush(stdin);cin.get(data_pegawai.alamat,50);
	//validasi untuk alamat harus <= 15 karakter
	panjang = strlen(data_pegawai.alamat);
	while (panjang > 22) {
		setcolor(3);
		gotoxy(69,14);cout<<"Panjang Alamat Yang Diinputkan"<<endl;
		gotoxy(69,15);cout<<"Tidak Boleh Lebih Dari 22 Karakter";
		getch();
		gotoxy(69,14);cout<<"                                   "<<endl;
		gotoxy(69,15);cout<<"                                   ";
		gotoxy(74,12);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,12);cout<<(char)26<<" Alamat            : ";fflush(stdin);cin.get(data_pegawai.alamat,50);
		panjang = strlen(data_pegawai.alamat);
	}
	gotoxy(52,14);cout<<"Golongan (pilih 1/2/3)";
	gotoxy(56,15);cout<<"1. 1A";
	gotoxy(56,16);cout<<"2. 1B";
	gotoxy(56,17);cout<<"3. 1C";
	gotoxy(52,18);cout<<(char)26<<" Pilih Golongan    : ";cin>>golongan;
	//validasi golongan
	while ((golongan< 1) || (golongan >3)) {
		setcolor(3);
		gotoxy(69,20);cout<<"Pilihan Golongan Tidak Terdaftar"<<endl;
		gotoxy(69,21);cout<<"Pilih 1/2/3";
		getch();
		gotoxy(69,20);cout<<"                                   "<<endl;
		gotoxy(69,21);cout<<"                                   ";
		gotoxy(74,18);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,18);cout<<(char)26<<" Pilih Golongan    : ";cin>>golongan;
	}
	
	int gaji_golongan;
	if (golongan==1) {
		strcpy(data_pegawai.golongan,"1A");
		gaji_golongan = 5000000;
	} else 	if (golongan==2) {
		strcpy(data_pegawai.golongan,"1B");
		gaji_golongan = 4000000;
	} else {
		strcpy(data_pegawai.golongan,"1C");
		gaji_golongan = 3000000;
	}
	
	gotoxy(52,20);cout<<"Jabatan (pilih 1/2/3/4)";
	gotoxy(56,21);cout<<"1. Kepala Sekolah";
	gotoxy(56,22);cout<<"2. Wakasek Kesiswaan";
	gotoxy(56,23);cout<<"3. Guru";
	gotoxy(56,24);cout<<"4. Staff TU";
	gotoxy(52,25);cout<<(char)26<<" Pilih Jabatan     : ";cin>>jabatan;
	//validasi jabatan
	while ((jabatan< 1) || (jabatan >4)) {
		setcolor(3);
		gotoxy(69,27);cout<<"Pilihan Jabatan Tidak Terdaftar"<<endl;
		gotoxy(69,28);cout<<"Pilih 1/2/3/4";
		getch();
		gotoxy(69,27);cout<<"                                   "<<endl;
		gotoxy(69,28);cout<<"                                   ";
		gotoxy(74,25);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,25);cout<<(char)26<<" Pilih Jabatan     : ";cin>>jabatan;
	}
	int gaji_jabatan;
	if (jabatan==1) {
		strcpy(data_pegawai.jabatan,"Kepala Sekolah");
		gaji_jabatan = 1000000;
	} else 	if (jabatan==2) {
		strcpy(data_pegawai.jabatan,"Wakasek Kesiswaan");
		gaji_jabatan = 750000;
	} else if (jabatan==3) {
		strcpy(data_pegawai.jabatan,"Guru");
		gaji_jabatan = 500000;
	}else{
		strcpy(data_pegawai.jabatan,"Staff TU");
		gaji_jabatan = 400000;
	}

	gotoxy(52,27);cout<<"Bulan Masuk Kerja(pilih 1-12)";
	gotoxy(56,28);cout<<"1. Januari";
	gotoxy(56,29);cout<<"2. Februari";
	gotoxy(56,30);cout<<"3. Maret";
	gotoxy(56,31);cout<<"4. April";
	gotoxy(70,28);cout<<"5. Mei";
	gotoxy(70,29);cout<<"6. Juni";
	gotoxy(70,30);cout<<"7. Juli";
	gotoxy(70,31);cout<<"8. Agustus";
	gotoxy(84,28);cout<<"9.  September";
	gotoxy(84,29);cout<<"10. Oktober";
	gotoxy(84,30);cout<<"11. November";
	gotoxy(84,31);cout<<"12. Desember";
	gotoxy(52,32);cout<<(char)26<<" Pilih Bulan       : ";cin>>bulan;
	
	//validasi bulan masuk kerja
	while ((bulan< 1) || (bulan >12)) {
		setcolor(3);
		gotoxy(69,34);cout<<"Pilihan Bulan Tidak Terdaftar"<<endl;
		gotoxy(69,35);cout<<"Pilih 1-12";
		getch();
		gotoxy(69,34);cout<<"                                   "<<endl;
		gotoxy(69,35);cout<<"                                   ";
		gotoxy(74,32);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,32);cout<<(char)26<<" Pilih Bulan       : ";cin>>bulan;
	}
	switch(bulan) {
		case 1 : strcpy(data_pegawai.bulan_masuk,"Januari"); 
			break;
		case 2 : strcpy(data_pegawai.bulan_masuk,"Februari"); 
			break;
		case 3 : strcpy(data_pegawai.bulan_masuk,"Maret"); 
			break;
		case 4 : strcpy(data_pegawai.bulan_masuk,"April"); 
			break;
		case 5 : strcpy(data_pegawai.bulan_masuk,"Mei"); 
			break;
		case 6 : strcpy(data_pegawai.bulan_masuk,"Juni"); 
			break;
		case 7 : strcpy(data_pegawai.bulan_masuk,"Juli"); 
			break;
		case 8 : strcpy(data_pegawai.bulan_masuk,"Agustus"); 
			break;
		case 9 : strcpy(data_pegawai.bulan_masuk,"September"); 
			break;
		case 10 : strcpy(data_pegawai.bulan_masuk,"Oktober"); 
			break;
		case 11 : strcpy(data_pegawai.bulan_masuk,"November"); 
			break;
		case 12 : strcpy(data_pegawai.bulan_masuk,"Desember"); 
			break;
	}
	
	gotoxy(52,34);cout<<(char)26<<" Tahun Masuk Kerja : ";cin>>data_pegawai.tahun_masuk;
	//validasi tahun masuk kerja
	while ((data_pegawai.tahun_masuk< 2000) || (data_pegawai.tahun_masuk >2014)) {
		setcolor(3);
		gotoxy(69,36);cout<<"Tahun Yang Diinputkan Salah"<<endl;
		gotoxy(69,37);cout<<"Tahun Harus Dari 2000-2014";
		getch();
		gotoxy(69,36);cout<<"                                   "<<endl;
		gotoxy(69,37);cout<<"                                   ";
		gotoxy(74,34);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,34);cout<<(char)26<<" Tahun Masuk Kerja : ";cin>>data_pegawai.tahun_masuk;
	}
	
	tahun = year-data_pegawai.tahun_masuk;
	total_bulan = tahun * 12;
	temp = bulan-month;
	data_pegawai.total_banyak_bulan = total_bulan - temp; 
		
	gotoxy(52,36);cout<<"Status (pilih 1/2)";
	gotoxy(56,37);cout<<"1. Menikah";
	gotoxy(56,38);cout<<"2. Belum Menikah";
	gotoxy(52,39);cout<<(char)26<<" Pilih Status      : ";cin>>status;
	//validasi status
	while ((status< 1) || (status >2)) {
		setcolor(3);
		gotoxy(69,41);cout<<"Pilihan Status Tidak Terdaftar"<<endl;
		gotoxy(69,42);cout<<"Pilih 1/2";
		getch();
		gotoxy(69,41);cout<<"                                   "<<endl;
		gotoxy(69,42);cout<<"                                   ";
		gotoxy(74,39);cout<<"                                   ";
		setcolor(7);
		gotoxy(52,39);cout<<(char)26<<" Pilih Status      : ";cin>>status;
	}	
	if (status==1) {
		strcpy(data_pegawai.status,"Menikah");
	} else {
		strcpy(data_pegawai.status,"Belum Menikah");
	}
	if ( status == 2) {
		data_pegawai.jml_anak = 0;
	} else {
	gotoxy(52,41);cout<<(char)26<<" Jumlah Anak       : ";cin>>data_pegawai.jml_anak;
	}
	//menghitung gaji pegawai
	int gaji_tunjangan;
	data_pegawai.gaji.t_anak = data_pegawai.jml_anak*250000;
	data_pegawai.gaji.g_pokok = gaji_golongan + gaji_jabatan;
	data_pegawai.gaji.total_gaji = data_pegawai.gaji.g_pokok + data_pegawai.gaji.t_anak;
	return data_pegawai;
}

//procedure output
void output_data_pegawai(s_pegawai data_pegawai[50], int n) {
	int i = 0;
	int k = 1;
	int j = 0;
	gotoxy(62,4);cout<<"DATA PEGAWAI";
	gotoxy(59,5);cout<<"==================";
	setcolor(3);
	gotoxy(1,7);cout<<"+==================================================================================================================================+";
	gotoxy(1,8);cout<<"|  NIP  |   NAMA                |   ALAMAT               | GOL. |  JABATAN          |  STATUS       | J.ANAK | B.Masuk   | T.Masuk |";
	gotoxy(1,9);cout<<"+==================================================================================================================================+";
	for (i=0;i<=n;i++ ) {
		setcolor(3);
		gotoxy(1,10+i+j);cout<<"|       |                       |                        |      |                   |               |        |           |         |";
		gotoxy(1,10+i+k);cout<<"|       |                       |                        |      |                   |               |        |           |         |";
		setcolor(7);
		gotoxy(3,10+i+j);cout<<data_pegawai[i].nip;	
		gotoxy(11,10+i+j);cout<<data_pegawai[i].nama;
		gotoxy(35,10+i+j);cout<<data_pegawai[i].alamat;
		gotoxy(61,10+i+j);cout<<data_pegawai[i].golongan;
		gotoxy(67,10+i+j);cout<<data_pegawai[i].jabatan;
		gotoxy(87,10+i+j);cout<<data_pegawai[i].status;
		gotoxy(105,10+i+j);cout<<data_pegawai[i].jml_anak;
		gotoxy(112,10+i+j);cout<<data_pegawai[i].bulan_masuk;
		gotoxy(125,10+i+j);cout<<data_pegawai[i].tahun_masuk;
		setcolor(3);
		gotoxy(1,10+i+k);cout<<"+-------+-----------------------+------------------------+------+-------------------+---------------+--------+-----------+---------+";
		k = k+1;
		j=j+1;	
	}
	gotoxy(1,10+i+j-1);cout<<"+==================================================================================================================================+";
	cout<<endl<<endl;
	cout<<" Keterangan : "<<endl<<endl;
	cout<<"    GOL.         : Golongan dari pegawai"<<endl<<endl;
	cout<<"    J.ANAK       : Jumlah anak dari pegawai"<<endl<<endl;
	setcolor(7);
	cout<<endl<<endl<<endl;
	cout<<" Tekan Enter untuk Kembali ke Menu Utama...";
}


//procedure sort NIP pegawai
void sort_nip(int n, s_pegawai data_pegawai[50]) {
	int i,k;
	char temp[12];
	int temp1;
	int cm_nip;
	for (i=0;i<n;i++) {
		for (k=n;k>=(i+1);k--) {
			cm_nip = strcmp(data_pegawai[k].nip,data_pegawai[k-1].nip);
			if (cm_nip<0){
				strcpy(temp,data_pegawai[k].nip);
             	strcpy(data_pegawai[k].nip,data_pegawai[k-1].nip);
             	strcpy(data_pegawai[k-1].nip,temp);
             	
             	strcpy(temp,data_pegawai[k].nama);
             	strcpy(data_pegawai[k].nama,data_pegawai[k-1].nama);
             	strcpy(data_pegawai[k-1].nama,temp);
             	
             	strcpy(temp,data_pegawai[k].alamat);
             	strcpy(data_pegawai[k].alamat,data_pegawai[k-1].alamat);
             	strcpy(data_pegawai[k-1].alamat,temp);
             	
             	strcpy(temp,data_pegawai[k].jabatan);
             	strcpy(data_pegawai[k].jabatan,data_pegawai[k-1].jabatan);
             	strcpy(data_pegawai[k-1].jabatan,temp);
			
				strcpy(temp,data_pegawai[k].golongan);
             	strcpy(data_pegawai[k].golongan,data_pegawai[k-1].golongan);
             	strcpy(data_pegawai[k-1].golongan,temp);
             	
             	strcpy(temp,data_pegawai[k].status);
             	strcpy(data_pegawai[k].status,data_pegawai[k-1].status);
             	strcpy(data_pegawai[k-1].status,temp);
             	
             	strcpy(temp,data_pegawai[k].bulan_masuk);
             	strcpy(data_pegawai[k].bulan_masuk,data_pegawai[k-1].bulan_masuk);
             	strcpy(data_pegawai[k-1].bulan_masuk,temp);
             	
				temp1 = data_pegawai[k].tahun_masuk;
             	data_pegawai[k].tahun_masuk = data_pegawai[k-1].tahun_masuk;
             	data_pegawai[k-1].tahun_masuk = temp1;
             	
            	temp1 = data_pegawai[k].total_banyak_bulan;
             	data_pegawai[k].total_banyak_bulan = data_pegawai[k-1].total_banyak_bulan;
             	data_pegawai[k-1].total_banyak_bulan = temp1;
             	
				temp1 = data_pegawai[k].jml_anak;
             	data_pegawai[k].jml_anak = data_pegawai[k-1].jml_anak;
             	data_pegawai[k-1].jml_anak = temp1;
             	
             	temp1 = data_pegawai[k].gaji.g_pokok;
             	data_pegawai[k].gaji.g_pokok = data_pegawai[k-1].gaji.g_pokok;
             	data_pegawai[k-1].gaji.g_pokok = temp1;
             	
             	temp1 = data_pegawai[k].gaji.t_anak;
             	data_pegawai[k].gaji.t_anak = data_pegawai[k-1].gaji.t_anak;
             	data_pegawai[k-1].gaji.t_anak = temp1;
             	
             	temp1 = data_pegawai[k].gaji.total_gaji;
             	data_pegawai[k].gaji.total_gaji = data_pegawai[k-1].gaji.total_gaji;
             	data_pegawai[k-1].gaji.total_gaji = temp1;
             	
                 temp1 = data_pegawai[k].gaji.gaji_semua;
             	data_pegawai[k].gaji.gaji_semua = data_pegawai[k-1].gaji.gaji_semua;
             	data_pegawai[k-1].gaji.gaji_semua = temp1;
			}
		}
	}
}

//procedure sort gaji
void sort_gaji(int n, s_pegawai data_pegawai[50]) { //masih eror
	int i,k;
	char temp[12];
	int temp1;
	for (i=0;i<n;i++) {
		for (k=n;k>=(i+1);k--) {
			if (data_pegawai[k].gaji.total_gaji < data_pegawai[k-1].gaji.total_gaji){
				             	
             	temp1 = data_pegawai[k].gaji.total_gaji;
             	data_pegawai[k].gaji.total_gaji = data_pegawai[k-1].gaji.total_gaji;
             	data_pegawai[k-1].gaji.total_gaji = temp1;
             	
             	
				strcpy(temp,data_pegawai[k].nip);
             	strcpy(data_pegawai[k].nip,data_pegawai[k-1].nip);
             	strcpy(data_pegawai[k-1].nip,temp);
             	
             	strcpy(temp,data_pegawai[k].nama);
             	strcpy(data_pegawai[k].nama,data_pegawai[k-1].nama);
             	strcpy(data_pegawai[k-1].nama,temp);
             	
             	strcpy(temp,data_pegawai[k].alamat);
             	strcpy(data_pegawai[k].alamat,data_pegawai[k-1].alamat);
             	strcpy(data_pegawai[k-1].alamat,temp);
             	
             	strcpy(temp,data_pegawai[k].jabatan);
             	strcpy(data_pegawai[k].jabatan,data_pegawai[k-1].jabatan);
             	strcpy(data_pegawai[k-1].jabatan,temp);
			
				strcpy(temp,data_pegawai[k].golongan);
             	strcpy(data_pegawai[k].golongan,data_pegawai[k-1].golongan);
             	strcpy(data_pegawai[k-1].golongan,temp);
             	
             	strcpy(temp,data_pegawai[k].status);
             	strcpy(data_pegawai[k].status,data_pegawai[k-1].status);
             	strcpy(data_pegawai[k-1].status,temp);
             	
             	strcpy(temp,data_pegawai[k].bulan_masuk);
             	strcpy(data_pegawai[k].bulan_masuk,data_pegawai[k-1].bulan_masuk);
             	strcpy(data_pegawai[k-1].bulan_masuk,temp);
             	
				temp1 = data_pegawai[k].tahun_masuk;
             	data_pegawai[k].tahun_masuk = data_pegawai[k-1].tahun_masuk;
             	data_pegawai[k-1].tahun_masuk = temp1;
             	
            	temp1 = data_pegawai[k].total_banyak_bulan;
             	data_pegawai[k].total_banyak_bulan = data_pegawai[k-1].total_banyak_bulan;
             	data_pegawai[k-1].total_banyak_bulan = temp1;
             	
				temp1 = data_pegawai[k].jml_anak;
             	data_pegawai[k].jml_anak = data_pegawai[k-1].jml_anak;
             	data_pegawai[k-1].jml_anak = temp1;
             	
             	temp1 = data_pegawai[k].gaji.g_pokok;
             	data_pegawai[k].gaji.g_pokok = data_pegawai[k-1].gaji.g_pokok;
             	data_pegawai[k-1].gaji.g_pokok = temp1;
             	
             	temp1 = data_pegawai[k].gaji.t_anak;
             	data_pegawai[k].gaji.t_anak = data_pegawai[k-1].gaji.t_anak;
             	data_pegawai[k-1].gaji.t_anak = temp1;
             	
             	temp1 = data_pegawai[k].gaji.gaji_semua;
             	data_pegawai[k].gaji.gaji_semua = data_pegawai[k-1].gaji.gaji_semua;
             	data_pegawai[k-1].gaji.gaji_semua = temp1;
			}
		}
	}
}

//procedure output sort
void output_sort(s_pegawai data_pegawai[50], int n) {
	int i = 0;
	int j = 0;
	int k = 1;
	gotoxy(61,4);cout<<"DATA GAJI PEGAWAI";
	gotoxy(58,5);cout<<"=======================";
	setcolor(3);
	gotoxy(16,7);cout<<"+===================================================================================================+";
	gotoxy(16,8);cout<<"|  NIP  |   NAMA                | GOL. |  JABATAN          |   G.POKOK   |  T.ANAK   |  TOTAL GAJI  |";
	gotoxy(16,9);cout<<"+===================================================================================================+";
	for (i=0;i<=n;i++ ) {
		setcolor(3);
		gotoxy(16,10+i+j);cout<<"|       |                       |      |                   |             |           |              |";
		setcolor(7);
		gotoxy(18,10+i+j);cout<<data_pegawai[i].nip;	
		gotoxy(26,10+i+j);cout<<data_pegawai[i].nama;
		gotoxy(51,10+i+j);cout<<data_pegawai[i].golongan;
		gotoxy(57,10+i+j);cout<<data_pegawai[i].jabatan;
		gotoxy(77,10+i+j);cout<<data_pegawai[i].gaji.g_pokok;
		gotoxy(91,10+i+j);cout<<data_pegawai[i].gaji.t_anak;
		gotoxy(103,10+i+j);cout<<data_pegawai[i].gaji.total_gaji;
		setcolor(3);
		gotoxy(16,10+i+k);cout<<"+-------+-----------------------+------+-------------------+-------------+-----------+--------------+";
		j = j+1;
		k = k+1;	
	}
	gotoxy(16,10+i
	+j-1);cout<<"+===================================================================================================+";
	cout<<endl<<endl;
	cout<<" Keterangan : "<<endl<<endl;
	cout<<"    GOL.         : Golongan dari pegawai"<<endl<<endl;
	cout<<"    G.POKOK      : Gaji Pokok yang diproleh pegawai"<<endl<<endl;
	cout<<"    T. ANAK      : Tunjangan anak yang di dapat pegawai"<<endl<<endl;
	setcolor(7);
}

void tabel_gaji(s_pegawai data_pegawai[50],int n) {
	int i;
	int j = 0;
	int temp =0;
	for (i=0;i<=n;i++) {
		temp = 10+j+i;
		j=j+1;
	}
	cout<<endl;
	temp=temp+17;
	sort_gaji(n,data_pegawai);
	gotoxy(54,temp);cout<<"GAJI TERBESAR DAN TERKECIL";
	gotoxy(51,temp+1);cout<<"================================";
	setcolor(3);
	gotoxy(9,temp+3);cout<<"+=================================================================================================================+";
	gotoxy(9,temp+4);cout<<"|    DATA      |  NIP   |   NAMA                | GOL. |  JABATAN          |  G.POKOK  |  T.ANAK   |  TOTAL GAJI  |";
	gotoxy(9,temp+5);cout<<"+--------------+--------+-----------------------+------+-------------------+-----------+-----------+--------------+";
	gotoxy(9,temp+6);cout<<"| G. Terbesar  |        |                       |      |                   |           |           |              |";
	gotoxy(9,temp+7);cout<<"+--------------+--------+-----------------------+------+-------------------+-----------+-----------+--------------+";
	gotoxy(9,temp+8);cout<<"| G. Terkecil  |        |                       |      |                   |           |           |              |";
	gotoxy(9,temp+9);cout<<"+=================================================================================================================+";
	setcolor(7);
	
	gotoxy(26,temp+8);cout<<data_pegawai[0].nip;	
	gotoxy(35,temp+8);cout<<data_pegawai[0].nama;
	gotoxy(60,temp+8);cout<<data_pegawai[0].golongan;
	gotoxy(66,temp+8);cout<<data_pegawai[0].jabatan;
	gotoxy(86,temp+8);cout<<data_pegawai[0].gaji.g_pokok;
	gotoxy(98,temp+8);cout<<data_pegawai[0].gaji.t_anak;
	gotoxy(110,temp+8);cout<<data_pegawai[0].gaji.total_gaji;
	
	gotoxy(26,temp+6);cout<<data_pegawai[n].nip;	
	gotoxy(35,temp+6);cout<<data_pegawai[n].nama;
	gotoxy(60,temp+6);cout<<data_pegawai[n].golongan;
	gotoxy(66,temp+6);cout<<data_pegawai[n].jabatan;
	gotoxy(86,temp+6);cout<<data_pegawai[n].gaji.g_pokok;
	gotoxy(98,temp+6);cout<<data_pegawai[n].gaji.t_anak;
	gotoxy(110,temp+6);cout<<data_pegawai[n].gaji.total_gaji;
	
	cout<<endl<<endl<<endl;
	cout<<endl<<endl<<endl;
	cout<<endl<<endl<<endl;
	cout<<" Tekan Enter untuk Kembali ke Menu Utama...";
}

void search_nip(s_pegawai data_pegawai[50],int n) {
	char datacari[21];
	int i;
	int banding;
	int temp[10];
	i=0;
	cout<<endl<<"Masukkan Nip Pegawai : ";fflush(stdin);cin.get(datacari,20);
	banding = strcmp(data_pegawai[i].nip,datacari);
	while((i<=n) && (banding != 0)) {
		i++;
		banding = strcmp(data_pegawai[i].nip,datacari);
	}
	banding = strcmp(data_pegawai[i].nip,datacari);
	if (banding == 0) {
		cout<<endl<<endl<<"Data dengan NIP ";setcolor(2);cout<<datacari;setcolor(7);cout<<" ditemukan";
		cout<<endl<<endl;
		cout<<"======================================="<<endl<<endl;
		cout<<" NIP               : ";setcolor(2);cout<<data_pegawai[i].nip<<endl;setcolor(7);	
		cout<<" Nama              : "<<data_pegawai[i].nama<<endl;
		cout<<" Alamat            : "<<data_pegawai[i].alamat<<endl;
		cout<<" Golongan          : "<<data_pegawai[i].golongan<<endl;
		cout<<" Jabatan           : "<<data_pegawai[i].jabatan<<endl;
		cout<<" Bulan Masuk Kerja : "<<data_pegawai[i].bulan_masuk<<endl;
		cout<<" Tahun Masuk Kerja : "<<data_pegawai[i].tahun_masuk<<endl;
		cout<<" Status            : "<<data_pegawai[i].status<<endl;
		cout<<" Jumlah Anak       : "<<data_pegawai[i].jml_anak<<endl;
		cout<<" Gaji Pokok        : "<<data_pegawai[i].gaji.g_pokok<<endl;
		cout<<" Tunjangan Anak    : "<<data_pegawai[i].gaji.t_anak<<endl;
		cout<<" Gaji Total        : "<<data_pegawai[i].gaji.total_gaji<<endl<<endl;
		cout<<"======================================="<<endl;	
		cout<<endl<<endl<<endl;
		cout<<" Tekan Enter untuk Kembali ke Menu Utama...";
	} else {
		cout<<endl<<" NIP tidak dtemukan!";
	}

}

void search_nama(s_pegawai data_pegawai[50],int n) {
	char datacari[31];
	int i;
	int banding;
	int j;
	//bool ketemu;
	int temp[10];
	j=-1;
	i=0;
	cout<<endl<<"Masukkan Nama Pegawai : ";fflush(stdin);cin.get(datacari,30);
	banding = strcmp(data_pegawai[i].nama,datacari);
	while(i<=n) {
		if (banding == 0) {
			j++;				
			temp[j] = i;
		}
		i++;
		banding = strcmp(data_pegawai[i].nama,datacari);
	}

	int k;
	int s = 0;
	if (j>=0) {
		cout<<endl<<endl<<j+1<<" Data dengan Nama ";setcolor(2);cout<<datacari;setcolor(7);cout<<" ditemukan";
		cout<<endl<<endl;
		cout<<"======================================="<<endl<<endl<<endl;
		for (k=0;k<=j;k++) {
			s = temp[k];
			cout<<" NIP               : "<<data_pegawai[s].nip<<endl;	
			cout<<" Nama              : ";setcolor(2);cout<<data_pegawai[s].nama<<endl;setcolor(7);
			cout<<" Alamat            : "<<data_pegawai[s].alamat<<endl;
			cout<<" Golongan          : "<<data_pegawai[s].golongan<<endl;
			cout<<" Jabatan           : "<<data_pegawai[s].jabatan<<endl;
			cout<<" Bulan Masuk Kerja : "<<data_pegawai[s].bulan_masuk<<endl;
			cout<<" Tahun Masuk Kerja : "<<data_pegawai[s].tahun_masuk<<endl;
			cout<<" Status            : "<<data_pegawai[s].status<<endl;
			cout<<" Jumlah Anak       : "<<data_pegawai[s].jml_anak<<endl;
			cout<<" Gaji Pokok        : "<<data_pegawai[s].gaji.g_pokok<<endl;
			cout<<" Tunjangan Anak    : "<<data_pegawai[s].gaji.t_anak<<endl;
			cout<<" Gaji Total        : "<<data_pegawai[s].gaji.total_gaji<<endl<<endl<<endl;
		}
		cout<<endl<<"======================================="<<endl;
		cout<<endl<<endl<<endl;
		cout<<" Tekan Enter untuk Kembali ke Menu Utama...";
	} else {
		cout<<endl<<" Nama tidak dtemukan!";
	}
}

//procedure statistik gaji pegawai
void stat_pegawai(s_pegawai data_pegawai[50], int n) {
	int i = 0;
	int j=0;
	int k=1;
	gotoxy(60,4);cout<<"STATISTIK GAJI PEGAWAI";
	gotoxy(57,5);cout<<"============================";
	setcolor(3);
	gotoxy(19,7);cout<<"+============================================================================================+";
	gotoxy(19,8);cout<<"|  NIP  |   NAMA                | B.Masuk   | T.Masuk |  GAJI / BULAN  |  GAJI A. KRJ.-SEK.  |";
	gotoxy(19,9);cout<<"+============================================================================================+";
	for (i=0;i<=n;i++) {
		data_pegawai[i].gaji.gaji_semua = data_pegawai[i].total_banyak_bulan * data_pegawai[i].gaji.total_gaji;
		gotoxy(19,10+i+j);cout<<"|       |                       |           |         |                |                     |";
		setcolor(7);
		gotoxy(21,10+i+j);cout<<data_pegawai[i].nip;	
		gotoxy(29,10+i+j);cout<<data_pegawai[i].nama;
		gotoxy(53,10+i+j);cout<<data_pegawai[i].bulan_masuk;
		gotoxy(66,10+i+j);cout<<data_pegawai[i].tahun_masuk;
		gotoxy(75,10+i+j);cout<<data_pegawai[i].gaji.g_pokok;
		gotoxy(92,10+i+j);cout<<data_pegawai[i].gaji.gaji_semua;
		setcolor(3);
		gotoxy(19,10+i+k);cout<<"+-------+-----------------------+-----------+---------+----------------+---------------------+";
		k++;
		j++;
	}
	gotoxy(19,10+i+j-1);cout<<"+============================================================================================+";
	cout<<endl<<endl;
	cout<<" Keterangan : "<<endl<<endl;
	cout<<"    B. Masuk         : Bulan pegawai masuk kerja"<<endl<<endl;
	cout<<"    T. Masuk         : Tahun pegawai masuk kerja"<<endl<<endl;
	cout<<"    GAJI A. KRJ-SEK  : Total gaji yang didapat dari awal bekerja sampai sekarang"<<endl<<endl;
	setcolor(7);

}

void sort_gaji_semua(int n,s_pegawai data_pegawai[50]) {
	int i,k;
	char temp[12];
	int temp1;
	for (i=0;i<n;i++) {
		for (k=n;k>=(i+1);k--) {
			if (data_pegawai[k].gaji.gaji_semua < data_pegawai[k-1].gaji.gaji_semua){

             	temp1 = data_pegawai[k].gaji.gaji_semua;
             	data_pegawai[k].gaji.gaji_semua = data_pegawai[k-1].gaji.gaji_semua;
             	data_pegawai[k-1].gaji.gaji_semua = temp1;
                 				             	
             	temp1 = data_pegawai[k].gaji.total_gaji;
             	data_pegawai[k].gaji.total_gaji = data_pegawai[k-1].gaji.total_gaji;
             	data_pegawai[k-1].gaji.total_gaji = temp1;
             	
				strcpy(temp,data_pegawai[k].nip);
             	strcpy(data_pegawai[k].nip,data_pegawai[k-1].nip);
             	strcpy(data_pegawai[k-1].nip,temp);
             	
             	strcpy(temp,data_pegawai[k].nama);
             	strcpy(data_pegawai[k].nama,data_pegawai[k-1].nama);
             	strcpy(data_pegawai[k-1].nama,temp);
             	
             	strcpy(temp,data_pegawai[k].alamat);
             	strcpy(data_pegawai[k].alamat,data_pegawai[k-1].alamat);
             	strcpy(data_pegawai[k-1].alamat,temp);
             	
             	strcpy(temp,data_pegawai[k].jabatan);
             	strcpy(data_pegawai[k].jabatan,data_pegawai[k-1].jabatan);
             	strcpy(data_pegawai[k-1].jabatan,temp);
			
				strcpy(temp,data_pegawai[k].golongan);
             	strcpy(data_pegawai[k].golongan,data_pegawai[k-1].golongan);
             	strcpy(data_pegawai[k-1].golongan,temp);
             	
             	strcpy(temp,data_pegawai[k].status);
             	strcpy(data_pegawai[k].status,data_pegawai[k-1].status);
             	strcpy(data_pegawai[k-1].status,temp);
             	
             	strcpy(temp,data_pegawai[k].bulan_masuk);
             	strcpy(data_pegawai[k].bulan_masuk,data_pegawai[k-1].bulan_masuk);
             	strcpy(data_pegawai[k-1].bulan_masuk,temp);
             	
				temp1 = data_pegawai[k].tahun_masuk;
             	data_pegawai[k].tahun_masuk = data_pegawai[k-1].tahun_masuk;
             	data_pegawai[k-1].tahun_masuk = temp1;
             	
            	temp1 = data_pegawai[k].total_banyak_bulan;
             	data_pegawai[k].total_banyak_bulan = data_pegawai[k-1].total_banyak_bulan;
             	data_pegawai[k-1].total_banyak_bulan = temp1;
             	
				temp1 = data_pegawai[k].jml_anak;
             	data_pegawai[k].jml_anak = data_pegawai[k-1].jml_anak;
             	data_pegawai[k-1].jml_anak = temp1;
             	
             	temp1 = data_pegawai[k].gaji.g_pokok;
             	data_pegawai[k].gaji.g_pokok = data_pegawai[k-1].gaji.g_pokok;
             	data_pegawai[k-1].gaji.g_pokok = temp1;
             	
             	temp1 = data_pegawai[k].gaji.t_anak;
             	data_pegawai[k].gaji.t_anak = data_pegawai[k-1].gaji.t_anak;
             	data_pegawai[k-1].gaji.t_anak = temp1;
			}
		}
	}     

}

void tabel_gaji_statistik(s_pegawai data_pegawai[50],int n) {
	int i;
	int j = 0;
	int temp =0;
	for (i=0;i<=n;i++) {
		temp = 10+j+i;
		j=j+1;
	}
	cout<<endl;
	temp=temp+17;
	sort_gaji_semua(n,data_pegawai);
	gotoxy(54,temp);cout<<"GAJI TERBESAR DAN TERKECIL"; 
    gotoxy(51,temp+1);cout<<"DARI AWAL BEKERJA SAMPAI SEKARANG";
	gotoxy(49,temp+2);cout<<"======================================";
	setcolor(3);
	
    gotoxy(12,temp+4);cout<<"+============================================================================================================+";
	gotoxy(12,temp+5);cout<<"|    DATA      |  NIP   |   NAMA                | B.Masuk   | T.Masuk |  GAJI / BULAN  |  GAJI A. KRJ.-SEK.  |";
	gotoxy(12,temp+6);cout<<"+============================================================================================================+";
	gotoxy(12,temp+7);cout<<"| G. Terbesar  |        |                       |           |         |                |                     |";
	gotoxy(12,temp+8);cout<<"+--------------+--------+-----------------------+-----------+---------+----------------+---------------------+";
	gotoxy(12,temp+9);cout<<"| G. Terkecil  |        |                       |           |         |                |                     |";
	gotoxy(12,temp+10);cout<<"+=====================================================================================+======================+";
	setcolor(7);
	
	gotoxy(30,temp+7);cout<<data_pegawai[n].nip;	
	gotoxy(38,temp+7);cout<<data_pegawai[n].nama;
	gotoxy(62,temp+7);cout<<data_pegawai[n].bulan_masuk;
	gotoxy(74,temp+7);cout<<data_pegawai[n].tahun_masuk;
	gotoxy(84,temp+7);cout<<data_pegawai[n].gaji.g_pokok;
	gotoxy(101,temp+7);cout<<data_pegawai[n].gaji.gaji_semua;
	
	gotoxy(30,temp+9);cout<<data_pegawai[0].nip;	
	gotoxy(38,temp+9);cout<<data_pegawai[0].nama;
	gotoxy(62,temp+9);cout<<data_pegawai[0].bulan_masuk;
	gotoxy(74,temp+9);cout<<data_pegawai[0].tahun_masuk;
	gotoxy(84,temp+9);cout<<data_pegawai[0].gaji.g_pokok;
	gotoxy(101,temp+9);cout<<data_pegawai[0].gaji.gaji_semua;
	
	cout<<endl<<endl<<endl;
	cout<<endl<<endl<<endl;
	cout<<endl<<endl<<endl;
	cout<<" Tekan Enter untuk Kembali ke Menu Utama...";
}


void jam() {
  	time_t rawtime;
  	struct tm *timeinfo;
 
  	time ( &rawtime );
  	timeinfo = localtime ( &rawtime );
	cout<<asctime (timeinfo);
}

int main(int argc, char *argv[]) {
	int menu_utama;
	int menu_sub_penggajian;
	int menu_data_gaji_p;
	int menu_search_pegawai;
	int b_user,b_pass;
	char username[20],password[32];
	s_pegawai data_pegawai[50];
	char jawab;
	int i;
	int b = 0;
	int kol = 0;
	int n=1;
	int count;
	int salah=0;
	inisialisasi(data_pegawai);
	do {
		menu_utama=1; //inisialisasi ketika melewati goto akhir;
		system("color 72");
		system("cls");
		gotoxy(62,10);cout<<"HALAMAN LOGIN"<<endl;
		gotoxy(59,12);cout<<"==================="<<endl;
		gotoxy(56,15);cout<<"USERNAME : ";cin>>username;
		gotoxy(56,18);cout<<"PASSWORD : "; 
		for (int i=0;i<32;i++)
    	{
      		password[i]=getch();
      		if (password[i]=='\r')
      		{
          		password[i]=NULL;
         		break;
      		}
       		if (password[i]=='\b')
      		{
         		if(i!=0)
		 		cout<<"\b \b"; 
		 		password[i]=NULL;
         		password[i-1]=NULL;
		 		i-=2;
         		if(i<-1)i=-1; 
         			continue;
      		}
      		cout<<"*";
    	}
		b_user = strcmp(user,username);
		b_pass = strcmp(pass,password);
		if ((b_user == 0) && (b_pass == 0)) {
			system("color 07");
			for (int i=0;i<3;i++) {
				system("cls");
				gotoxy(30,12);cout<<"                              ";
				delay(200);gotoxy(60,27);cout<<"W";
				delay(200);gotoxy(62,27);cout<<"E";
				delay(200);gotoxy(64,27);cout<<"L";
				delay(200);gotoxy(66,27);cout<<"C";
				delay(200);gotoxy(68,27);cout<<"O";
				delay(200);gotoxy(70,27);cout<<"M";
				delay(200);gotoxy(72,27);cout<<"E";
				delay(200);gotoxy(74,27);cout<<(char)1;
				delay(200);
			}
			delay(400);
			system("cls");
			gotoxy(53,27);jam();
			delay(1000);
			int i;
			int b = 0;
			int kol = 0;
			for (i=0;i<=26;i++) {

				gotoxy((53+kol),(27-b));jam();
				gotoxy((53+kol-2),(27-b+1));cout<<"                               ";
				delay(50);
				b= b+1;
				kol = kol+2;
			}
			delay(1000);
			do {
				salah = 2; //inisialisasi untuk melewati perulangan login.
				system("cls");
				gotoxy(105,1);
				jam();
				menu_u(&menu_utama);
				switch(menu_utama) {
					case 1 :
						do {
							system("cls");
							gotoxy(105,1);
							jam();
							n=n+1;
							data_pegawai[n] = i_pegawai();
							cout<<"Tambahkan data baru(y/t) : ";
							jawab = getche();
							
						}while(jawab!='t');
						//count untuk menentukan banyaknya data
						count = n;
						cout<<endl<<endl;
						cout<<"Data sudah berhasil diinputkan, tekan enter...";
						getch();
						break;
					case 2 :
						system("cls");
						gotoxy(105,1);
						jam();
						output_data_pegawai(data_pegawai,n);
						getch();
						break;
					case 3 :
						do {
							system("cls");
							gotoxy(105,1);
							jam();
							menu_penggajian(&menu_sub_penggajian);
							switch (menu_sub_penggajian) {
								case 1 :
									do {
										system("cls");
										gotoxy(105,1);
										jam();
										data_gaji_pegawai(&menu_data_gaji_p);
										switch(menu_data_gaji_p) {
											case 1 :
												system("cls");
												gotoxy(105,1);
												jam();
												sort_nip(n,data_pegawai); 
												output_sort(data_pegawai,n);
												tabel_gaji(data_pegawai,n);
												getch();
												break;
											case 2 :
												system("cls");
												gotoxy(105,1);
												jam();
												sort_gaji(n,data_pegawai);
												output_sort(data_pegawai,n);
												tabel_gaji(data_pegawai,n);
												getch();
												break;
											case 0 :
												break;
											default : cout<<endl<<"Menu yang anda inputkan tidak ada"<<endl;
						  						  cout<<"Tekan enter untuk Mengulang...!"<<endl;
						  						  getch();
										}
									} while (menu_data_gaji_p != 0);
									break;
								case 2 :
									do {
										system("cls");
										gotoxy(105,1);
										jam();
										search_pegawai(&menu_search_pegawai);
										switch(menu_search_pegawai) {
											case 1 :
												system("cls");
												gotoxy(105,1);
												jam();
												search_nip(data_pegawai,n);
												getch();
												break;
											case 2 :
												system("cls");
												gotoxy(105,1);
												jam();
												search_nama(data_pegawai,n);
												getch();
												break;
											case 0 :
												break;
											default : cout<<endl<<"Menu yang anda inputkan tidak ada"<<endl;
						  						  cout<<"Tekan enter untuk Mengulang...!"<<endl;
						  						  getch();
										}
									} while (menu_search_pegawai != 0);
									break;
								case 3 :
									system("cls");
									gotoxy(105,1);
									jam();
									stat_pegawai(data_pegawai,n);
									tabel_gaji_statistik(data_pegawai,n);
									getch();
									break; 
								case 0 :
									break;
								default : cout<<endl<<"Menu yang anda inputkan tidak ada"<<endl;
						  			  cout<<"Tekan enter untuk Mengulang...!"<<endl;
						  			  getch();
							}
						} while(menu_sub_penggajian != 0);
						break;
					case 0 :
						break;
					default : cout<<endl<<"Menu yang anda inputkan tidak ada"<<endl;
						  cout<<"Tekan enter untuk Mengulang...!"<<endl;
						  getch();
				}
			} while (menu_utama != 0);
		} else 
		{
			setcolor(3);
			gotoxy(44,23);cout<<"+----------------------------------------------------+";
			gotoxy(44,24);cout<<"| Invalid Username and Password, Please Try Again... |";
			gotoxy(44,25);cout<<"+----------------------------------------------------+";
			getch();
			setcolor(7);
		}
	
		salah++;
	}while(salah!=3);
	
	if(menu_utama == 0) {
		goto akhir;
	}
	setcolor(3);
	gotoxy(43,30);cout<<"+------------------------------------------------------+";
	gotoxy(43,31);cout<<"| Anda sudah 3x salah memasukkan username dan password |";
	gotoxy(43,32);cout<<"|                  Program akan keluar!!!              |";
	gotoxy(43,33);cout<<"+------------------------------------------------------+";
	setcolor(7);
	for (int i=0;i<134;i++) {
		delay(30);gotoxy(0+i,38);cout<<">";
		
	}
	goto finish;
	akhir:
	system("cls");
	gotoxy(105,1);;jam();
	delay(1000);
	for (i=0;i<=26;i++) {
		gotoxy((105-kol),(1+b));jam();
		gotoxy((105-kol+2),(1+b-1));cout<<"                               ";
		delay(50);
		b= b+1;
		kol = kol+2;
	}
	delay(1000);
	system("cls");
	
	delay(400);gotoxy(60,27);cout<<"B";
	delay(400);gotoxy(62,27);cout<<"Y";
	delay(400);gotoxy(64,27);cout<<"E";
	delay(400);gotoxy(66,27);cout<<".";
	delay(400);gotoxy(68,27);cout<<".";
	delay(400);gotoxy(70,27);cout<<".";
	delay(400);gotoxy(72,27);cout<<(char)1;
	delay(1000);
	finish:
	setcolor(7);
	return 0;
}
