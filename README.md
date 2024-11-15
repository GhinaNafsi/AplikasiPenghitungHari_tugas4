# AplikasiPenghitungHari_tugas4
 GhinaNafsi-2210010324

# 1. Deskripsi Program
Aplikasi ini menghitung jumlah hari dalam bulan tertentu pada tahun tertentu yang dipilih oleh pengguna.

- Input: Pengguna memilih bulan dari JComboBox , memilih tanggal dan memasukkan tahun menggunakan JSpinner .
- Penggunaan JCalendar: Untuk mempermudah pengguna memilih tanggal, bulan dan tahun.
- Output: Setelah tombol ditekan, aplikasi menampilkan jumlah hari dalam bulan yang dipilih dan menyebutkan dari hari awal dan hari terkhir pada calender pengguna pilih.
  
# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JComboBox, JSpinner, JButton, JCalendar
- JPanel: Untuk menampung komponen lain.
- JLabel: Berfungsi sebagai label untuk elemen input dan output.
- JComboBox: Untuk memilih bulan.
- JSpinner: Untuk memasukkan tahun.
- JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun secara visual.
- JButton: Tombol untuk menghitung jumlah hari, menghitung selisih hari, hapus dan keluar

- Button Hitung

private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    btnHitung.addActionListener((ActionEvent e) -> {
        kalkulatorhari();
    });
    }  

- Button Hitung Selisih Hari

private void bSelisihHariActionPerformed(java.awt.event.ActionEvent evt) {                                             

        bSelisihHari.addActionListener((ActionEvent e) -> {
            MenghitungSelisihTanggal(); //button untuk menghitung selisih hari 
        });
   }     

- Button Hapus

 private void bDeleteActionPerformed(java.awt.event.ActionEvent evt) {                                        
       
        // Event listener untuk tombol "Hapus"
        bDelete.addActionListener((ActionEvent e) -> {
            hapusinputan(); 
     });
   }    

Metode hapusinputan() di panggil

// Metode untuk menghapus atau mereset pilihan
    
    private void hapusinputan() {
        // Reset bulan ke Januari
        comboBULAN.setSelectedIndex(0);
        // Reset tahun ke tahun default (misalnya 2023)
        sTahun.setValue(2023);
        // Reset JCalendar ke tanggal hari ini
        calenderBT.setCalendar(Calendar.getInstance());
        // Kosongkan hasil pada JLabel
        labelHasil.setText("Jumlah hari: ");
    }

- Button Keluar

    private void bExitActionPerformed(java.awt.event.ActionEvent evt) {
~~~
  System.exit(0);
~~~
    }    

# 3. Logika Program: 
Penggunaan API tanggal (LocalDate), Perhitungan hari dalam bulan, Perhitungan tahun kabisat

# 4. Events:
* ActionListener untuk tombol Hitung

 private void buttonHitungActionPerformed(java.awt.event.ActionEvent evt) {                                             
        
        buttonHitung.addActionListener((ActionEvent e) -> {
        menghitunghari(); //agar button hitung berjalan
    });
   }   

Penjelasan Kode :
ActionListener pada buttonHitung Saat tombol ditekan, metode kalkulatorhari() akan dipanggil.

private void menghitunghari() {
       
        //Mengambil nilai bulan dari JComboBox
        int month = comboBULAN.getSelectedIndex() + 1; // ComboBox menggunakan indeks dari 0, jadi ditambah 1
        // Mengambil nilai tahun dari JSpinner
        int year = (int) sTahun.getValue();

        // Juga mengatur tanggal JCalendar sesuai dengan bulan dan tahun yang dipilih
        Calendar selectedDate = calenderBT.getCalendar();
        selectedDate.set(Calendar.MONTH, month - 1); // Calendar.MONTH menggunakan indeks dari 0
        selectedDate.set(Calendar.YEAR, year);
        calenderBT.setCalendar(selectedDate); // Menampilkan bulan dan tahun yang dipilih di JCalendar

        // Membuat objek YearMonth berdasarkan bulan dan tahun yang dipilih
        YearMonth yearMonth = YearMonth.of(year, month);

        // Menghitung jumlah hari dalam bulan tersebut
        int daysInMonth = yearMonth.lengthOfMonth();

        // Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();

        // Menampilkan hasil jumlah hari, hari pertama, dan hari terakhir pada JLabel
        labelHasil.setText(String.format(
            "Jumlah hari: %d, Hari pertama: %s, Hari terakhir: %s", 
            daysInMonth, firstDay.getDayOfWeek(), lastDay.getDayOfWeek()
        ));
   }


Metode hitungHari():
- comboBoxBulan.getSelectedIndex() mendapatkan indeks bulan yang dipilih (dengan Januari sebagai indeks 0), lalu menambahkan 1 agar sesuai dengan bulan kalender (Januari = 1).
- spinnerTahun.getValue() mengambil nilai tahun yang dipilih.
- Menghitung jumlah hari: YearMonth.of(tahun, bulan) membuat objek YearMonth untuk bulan dan tahun yang dipilih. Metode lengthOfMonth() kemudian digunakan untuk mendapatkan jumlah hari pada bulan tersebut.
- Hasil jumlah hari ditampilkan di labelHasil.
  
* ChangeListener pada JSpinner untuk input tahun

private void sTahunStateChanged(javax.swing.event.ChangeEvent evt) {                                    
        
         // input tanggal seperti formulir pendaftaran atau kalender dengan cepat
        sTahun.addChangeListener((ChangeEvent e) -> {
        updateCalender();
    });
   } 

Listener untuk mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah

private void comboBULANItemStateChanged(java.awt.event.ItemEvent evt) {                                            
    
     //untuk memilih dan mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah
        comboBULAN.addItemListener((ItemEvent e) -> {
            updateCalender();
        });
   }      

Metode pembaruankalender() akan di panggil

// Metode untuk memperbarui JCalendar sesuai pilihan bulan dan tahun
    private void updateCalender() {
       
        int month = comboBULAN.getSelectedIndex(); // Indeks bulan ComboBox mulai dari 0
        int year = (int) sTahun.getValue();

        // Mengatur JCalendar untuk bulan dan tahun yang dipilih
        Calendar selectedDate = Calendar.getInstance();
        selectedDate.set(Calendar.YEAR, year);
        selectedDate.set(Calendar.MONTH, month); // Calendar.MONTH juga mulai dari 0
        selectedDate.set(Calendar.DAY_OF_MONTH, 1);
        calenderBT.setCalendar(selectedDate); // Memperbarui tampilan JCalendar
   }

# 5. Variasi:
* Tampilkan informasi tambahan seperti hari pertama dan terakhir dalam bulan tersebut

// Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
       
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();

* Integrasikan fitur untuk menghitung selisih hari antara dua tanggal

 private void calculateDifferenceButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                          
    // Event listener untuk tombol "Hitung Selisih Hari"
       
       bSelisihHari.addActionListener((ActionEvent e) -> {
            MenghitungSelisihTanggal(); //button untuk menghitung selisih hari 
        });
        

Metode calculateDateDifference() akan di panggil

// Metode untuk menghitung selisih hari antara dua tanggal
     private void MenghitungSelisihTanggal() {
        
        // Mendapatkan tanggal awal dan akhir dari JCalendar
        Calendar startCal = calenderSH1.getCalendar();
        Calendar endCal = calenderSH2.getCalendar();

        // Konversi Calendar ke LocalDate
        LocalDate startDate = startCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        LocalDate endDate = endCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();

        // Menghitung selisih hari menggunakan ChronoUnit.DAYS
        long daysBetween = ChronoUnit.DAYS.between(startDate, endDate);

        // Menampilkan hasil selisih hari pada JLabel yang dibuat
        labelHasil2.setText("Selisih hari antara dua tanggal: " + daysBetween + " hari");
   }

# Hasil Gambar Project Ketika di Run
<img width="929" alt="MenghitungHari" src="https://github.com/user-attachments/assets/62a05e6d-6d44-4b75-be3e-4ee2f80499d2">


## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    10    |
|  2  | Logika Program   |    20    |
|  3  | Event            |    20    |
|  4  | Kesesuaian UI    |    20    |
|  5  | Memenuhi Variasi |    40    |
|     | TOTAL        | 100 |

## Pembuat

NAMA : GHINA NAFSI
NPM : 2210010324
KELAS : 5A TI REG PAGI BJM
