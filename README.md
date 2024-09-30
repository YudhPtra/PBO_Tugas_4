# PBO_Tugas_4

 * Kelas NumberDisplay merepresentasikan tampilan angka digital yang dapat menyimpan nilai dari nol hingga batas yang diberikan. Batas tersebut dapat 
 * ditentukan saat membuat tampilan. Nilai berkisar dari nol (inklusif) hingga batas-1. Jika digunakan, misalnya, untuk detik pada jam digital, batasnya 
 * adalah 60, sehingga menghasilkan nilai tampilan dari 0 hingga 59. Ketika ditambah, tampilan otomatis kembali ke nol saat mencapai batas.

`````
public class NumberDisplay{
    private int batas;
    private int nilai;

    /* Konstruktor untuk menetapkan batas di mana tampilan akan kembali ke nol.*/
    public NumberDisplay(int batasKembali){
        batas = batasKembali;
        nilai = 0;
    }

    /* Mengembalikan nilai saat ini*/
    public int getNilai(){
        return nilai;
    }

    /* Mengembalikan nilai tampilan (yaitu, nilai saat ini sebagai String dua digit. Jika nilainya kurang dari sepuluh, akan ditambahkan angka nol di depan).*/
    public String getNilaiTampilan(){
        if(nilai < 10){
            return "0" + nilai;
        } else {
            return "" + nilai;
        }
    }

    /* Menetapkan nilai tampilan ke nilai baru yang ditentukan. Jika nilai baru kurang dari nol atau melebihi batas, tidak melakukan apa-apa.*/
    public void setNilai(int nilaiBaru){
        if((nilaiBaru >= 0) && (nilaiBaru < batas)){
            nilai = nilaiBaru;
        }
    }

    /* Menambah nilai tampilan sebanyak satu, kembali ke nol jika batas tercapai.*/
    public void increment(){
        nilai = (nilai + 1) % batas;
    }
}
`````

 * Jam ini menampilkan jam dan menit. Rentang waktunya adalah 00:00 (tengah malam) hingga 23:59 (satu menit sebelum tengah malam).
 * Tampilan jam menerima "tanda detik" (melalui metode timeTick) setiap menit
 * dan bereaksi dengan menambah tampilan. Ini dilakukan dengan cara jam biasa:
 * jam bertambah ketika menit kembali ke nol.

`````
public class ClockDisplay {
    private NumberDisplay jam;
    private NumberDisplay menit;
    private String stringTampilan;    // mensimulasikan tampilan yang sebenarnya
    
    /* Konstruktor ini membuat jam baru diatur pada 00:00.*/
    public ClockDisplay(){
        jam = new NumberDisplay(24);
        menit = new NumberDisplay(60);
        perbaruiTampilan();
    }

    /* Konstruktor ini membuat jam baru diatur pada waktu yang ditentukan oleh parameter.*/
    public ClockDisplay(int jam, int menit){
        this.jam = new NumberDisplay(24);
        this.menit = new NumberDisplay(60);
        aturWaktu(jam, menit);
    }

    /* Metode ini dipanggil setiap satu menit - ini membuat tampilan jam maju satu menit.*/
    public void detikWaktu(){
        menit.increment();
        if(menit.getNilai() == 0){  // baru saja kembali ke nol
            jam.increment();
        }
        perbaruiTampilan();
    }

    /* Mengatur waktu tampilan ke jam dan menit yang ditentukan. */
    public void aturWaktu(int jam, int menit){
        this.jam.setNilai(jam);
        this.menit.setNilai(menit);
        perbaruiTampilan();
    }

    /* Mengembalikan waktu saat ini dari tampilan ini dalam format HH:MM. */
    public String ambilWaktu(){
        return stringTampilan;
    }
    
    /*Memperbarui string internal yang mewakili tampilan.*/
    private void perbaruiTampilan(){
        stringTampilan = jam.getNilaiTampilan() + ":" + menit.getNilaiTampilan();
    }
}
`````
