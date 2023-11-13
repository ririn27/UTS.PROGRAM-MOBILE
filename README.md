## UTS PEMROGRAMAN MOBILE

NAMA         : Ririn Nofrima

NIM          : 312210025

KELAS        : TI.22.B1

MATA KULIAH  : PEMROGRAMAN MOBILE

Tugas        : Membuat tombol yang setiap diklik dapat bertambah angkanya, namun dengan urutan angka fibonacci, lalu lengkapi dengan fitur toast


#Berikut ini Source Code  :

* # activity_main.Xml :
  
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

    <LinearLayout
        android:id="@+id/numberLayout"
        android:layout_width="match_parent"
        android:layout_height="76dp"
        android:orientation="horizontal">

        <EditText
            android:id="@+id/maxNumber"
            android:layout_width="94dp"
            android:layout_height="55dp"
            android:layout_marginLeft="10dp"
            android:layout_marginTop="5dp"
            android:layout_marginRight="5dp"
            android:layout_marginBottom="5dp"
            android:ems="10"
            android:freezesText="false"
            android:inputType="numberDecimal"
            android:text="0" />

        <Button
            android:id="@+id/buttonMax"
            android:layout_width="143dp"
            android:layout_height="wrap_content"
            android:text="Set Maximum" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/linear"
        android:layout_width="match_parent"
        android:layout_height="414dp"
        android:layout_below="@id/numberLayout"
        android:background="#eeeeee"
        android:clipToPadding="false"
        android:gravity="center"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textNama"
            android:layout_width="200dp"
            android:layout_height="wrap_content"
            android:layout_gravity="clip_horizontal|center"
            android:layout_marginTop="-40dp"
            android:layout_marginBottom="30dp"
            android:text="Ririn Nofrima 312210025"
            android:textAlignment="center"
            android:textSize="24sp" />

        <TextView
            android:id="@+id/textCountFibo"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:layout_marginBottom="5dp"
            android:paddingTop="5dp"
            android:paddingBottom="5dp"
            android:text="0"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="150sp" />

        <TextView
            android:id="@+id/textCount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tombol Hitung diklik sebanyak : 0"
            android:textAlignment="center"
            android:textSize="20sp" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <TextView
                android:id="@+id/textView6"
                android:layout_width="wrap_content"
                android:layout_height="29dp"
                android:layout_weight="1"
                android:text="Maksimum Angka fibo : "
                android:textAlignment="textEnd"
                android:textSize="20sp" />

            <TextView
                android:id="@+id/textMaxFibo"
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:text="0"
                android:textSize="20sp" />
        </LinearLayout>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="165dp"
        android:layout_below="@id/linear"
        android:orientation="vertical">

        <Button
            android:id="@+id/buttonCount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginStart="1dp"
            android:layout_marginLeft="1dp"
            android:layout_marginTop="3dp"
            android:hapticFeedbackEnabled="false"
            android:text="HITUNG"
            android:textAlignment="center"
            android:textStyle="bold" />

        <Button
            android:id="@+id/buttonReset"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginStart="1dp"
            android:layout_marginLeft="1dp"
            android:layout_marginTop="3dp"
            android:text="RESET"
            android:textStyle="bold" />

        <Button
            android:id="@+id/buttonToast"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tampilkan Toast"
            android:textAlignment="center"
            android:textStyle="bold" />
    </LinearLayout>

</RelativeLayout>

#Penjelasan :

*kita isi relative layout dengan 3 linear layout

*linear layout 1 berisi editText dan button set maximum

*linear layout 2 diisi dengan 3 textview dan 1 linear layout horizontal:

      a.nama + nim
      
      b.jumlah klik pada tombol hitung
      
      c.angka fibonacci terakhir
      
      d.linear layout : TextView untuk menampilkan jumlah maksimal angka fibonacci
      
*linear layout 3 berisi :

      a.linear layout 1 :button hitung + button reset
      
      b.linear layout 2 : button toast

* # MainActivity.Java

package  id.co.androidbelajar;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

import android.text.Layout;

import android.view.View;

import android.widget.Button;

import android.widget.EditText;

import android.widget.LinearLayout;

import android.widget.TextView;

import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    public int count = 0;
    
    public int countFibo = 0;
    
    public int maxFibo = 0;
    
    public TextView showCount;
    
    public TextView showCountFibo;
    
    public TextView showMaxFibo;
    
    public EditText maxNumber;
    
    public Button buttonToast;
    
    public Button buttonCount;
    
    public Button buttonMax;
    
    public Button buttonReset;
    
    public Toast toastA;
    
    public int[] warna;
    
    public LinearLayout linear;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        buttonToast = (Button) findViewById(R.id.buttonToast);
        buttonCount = (Button) findViewById(R.id.buttonCount);
        buttonReset = (Button) findViewById(R.id.buttonReset);
        buttonMax = (Button) findViewById(R.id.buttonMax);
        showCount = (TextView) findViewById(R.id.textCount);
        showCountFibo = (TextView) findViewById(R.id.textCountFibo);
        showMaxFibo = (TextView) findViewById(R.id.textMaxFibo);
        maxNumber = (EditText) findViewById(R.id.maxNumber);
        warna = getResources().getIntArray(R.array.warna_background_fibo);
        linear = (LinearLayout) findViewById(R.id.linear);

        buttonToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Fibonacci : " + countFibo, Toast.LENGTH_SHORT);
                toastA.show();
            }
        });

        buttonCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calculate(view);
            }
        });

        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                reset(view);
            }
        });

        buttonMax.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String getNumber = maxNumber.getText().toString();
                maxFibo = Integer.parseInt(getNumber);
                showMaxFibo.setText(getNumber);
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Maksimum fibonacci diubah menjadi " + getNumber, Toast.LENGTH_SHORT);
                toastA.show();
            }

            ;
        });

    }

    protected void calculate(View view) {
        if (calculateFibo(count + 1) >= maxFibo) {
            if (toastA != null) toastA.cancel();
            toastA = Toast.makeText(getApplicationContext(), "Sudah Mencapai Maksimum !!", Toast.LENGTH_SHORT);
            toastA.show();
        } else {
            count++;
            linear.setBackgroundColor(warna[count % 3]);
            countFibo = calculateFibo(count);
            showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
            showCountFibo.setText(Integer.toString(countFibo));
            if (count % 5 == 0) {
                if (toastA != null) toastA.cancel();
                toastA = Toast.makeText(getApplicationContext(), "Tombol hitung diklik : " + count + " Kali", Toast.LENGTH_SHORT);
                toastA.show();
            }
        }
    }

    protected int calculateFibo(int n) {
        if (n <= 1) {
            linear.setBackgroundColor(warna[2]);
            return n;
        }
        int prev, current, next;
        prev = 0;
        current = 1;
        for (int i = 2; i <= n; i++) {
            next = prev + current;
            prev = current;
            current = next;
        }
        return current;
    }

    protected void reset(View view) {
        count = 0;
        countFibo = 0;
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
        linear.setBackgroundColor (getResources().getColor(android.R.color.white));
    }
}

# Penjelasan dari MainActivity.java :

public int count = 0;
    
    public int countFibo = 0;
    
    public int maxFibo = 0;
    
    public TextView showCount;
    
    public TextView showCountFibo;
    
    public TextView showMaxFibo;
    
    public EditText maxNumber;
    
    public Button buttonToast;
    
    public Button buttonCount;
    
    public Button buttonMax;
    
    public Button buttonReset;
    
    public Toast toastA;
    
    public int[] warna;
    
    public LinearLayout linear;

a. *kita deklarasikan properti atau atribut yang akan kita gunakan dalam aplikasi ini*

b. *untuk count, countFibo dan maxFibo langsung kita isi dengan nilai 0 (integer)*

c. *masing masing diberi sesuai tipe data dan kita set visibility nya public1*

 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        buttonToast = (Button) findViewById(R.id.buttonToast);
        buttonCount = (Button) findViewById(R.id.buttonCount);
        buttonReset = (Button) findViewById(R.id.buttonReset);
        buttonMax = (Button) findViewById(R.id.buttonMax);
        showCount = (TextView) findViewById(R.id.textCount);
        showCountFibo = (TextView) findViewById(R.id.textCountFibo);
        showMaxFibo = (TextView) findViewById(R.id.textMaxFibo);
        maxNumber = (EditText) findViewById(R.id.maxNumber);
        warna = getResources().getIntArray(R.array.warna_background_fibo);
        linear = (LinearLayout) findViewById(R.id.linear);

        buttonToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Fibonacci : " + countFibo, Toast.LENGTH_SHORT);
                toastA.show();
            }
        });

        buttonCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calculate(view);
            }
        });

        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                reset(view);
            }
        });

        buttonMax.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String getNumber = maxNumber.getText().toString();
                maxFibo = Integer.parseInt(getNumber);
                showMaxFibo.setText(getNumber);
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Maksimum fibonacci diubah menjadi " + getNumber, Toast.LENGTH_SHORT);
                toastA.show();
            }

            ;
        });

    }

a. *disini kita akan mengisi beberapa properti yang belum diisi sebelumnya sesuai dengan tipe data*

b. *lalu dihubungkan menggunakan tipe data dan juga id yang ada pada activity_main.xml*

c. *kemudian kita beri event atau aksi yang akan dilakukan ketika tombol tombol diklik*

d. *saat tombol hitung diklik maka akan menjalankan fungsi calculate*

e. *saat tombol reset diklik maka akan menjalankan fungsi reset8

f. *saat tombol setmaximum diklik maka akan mengisi nilai pada properti maxFibo dan menampilkan toast dengan informasi bahwa angka maksimm fibonacci telah diperbarui*

g. *saat tombol tampilkan toast diklik maka akan menampilkan toast dengan data angka fibonacci*

protected void calculate(View view) {
        if (calculateFibo(count + 1) >= maxFibo) {
            if (toastA != null) toastA.cancel();
            toastA = Toast.makeText(getApplicationContext(), "Sudah Mencapai Maksimum !!", Toast.LENGTH_SHORT);
            toastA.show();
        } else {
            count++;
            linear.setBackgroundColor(warna[count % 3]);
            countFibo = calculateFibo(count);
            showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
            showCountFibo.setText(Integer.toString(countFibo));
            if (count % 5 == 0) {
                if (toastA != null) toastA.cancel();
                toastA = Toast.makeText(getApplicationContext(), "Tombol hitung diklik : " + count + " Kali", Toast.LENGTH_SHORT);
                toastA.show();
            }
        }
    }
a. *saat fungsi dijalankan, akan dicek terlebih dahulu apakah nilai count + 1 itu sama dengan atau lebih dari jumlah maksimum fibo? jika iya maka akan ada toast yang menampilkan bahwa sudah mencapai maksimum, jika tidak maka nilai count akan ditambah 1 kemudian warna background akan diubah berdasarkan sisa bagi 3 dari count, dari sisa bagi 3 itu hasilnya akan digunakan sebagai index dalam memanggil array warna*

b. *Kemudian count yang sudah ditambah , maka akan dijadikan nilai dalam menjalankan fungsi calculateFibo lalu akan menerima data baru yang telah diolah di fungsi tersebut dan kemusian dimasukkan ke properti countFibo*

c. *Tampilkan jumlah klik tombol hitung dan juga angka fibonacci*

d. *Kita tampilkan toast setiap tombol count diklik sebanyak 5 kali*

e. *Untuk toastA.cancel() bermaksud agar toast yang sudah ada langsung dihentikan karena toast paling cepat akan hilang dalam dua detik, jika belum dua detik dan ada toast yang aktif maka toast yang baru akan masuk dalam antrian, dan akan dijalankan berurut setelah dua detik dengan cancel ini maka kita hentikan toast yang ada*

f. *Lalu jalankan toast.show() agar langsung kita tampilkan toast yang baru*

   
    protected int calculateFibo(int n){
        if(n <= 1) {
            linear.setBackgroundColor(warna[2]);
            return n;
        }
        int prev,current,next;
        prev = 0;
        current = 1;
        for (int i = 2; i <= n; i++) {
            next = prev + current;
            prev = current;
            current = next;
        }
        return current;
    }
a. *Jika angka yanng di kirim kurang dari sama dengan 1, maka akan kita ganti warna background menjadi index kedua, hal ini berguna ketika kita klik button hitung dua kali, meskipun count bertambah 1, namun fibonacci belum bertambah, maka dari itu angka fibonacci yang sama akan mendapat warna background yang sama*

b. *Namun jika tidak diberi fungsi ini maka, pemilihan warna background akan berganti berdasarkan isi dari properti count, alhasil angka fibonacci 1 yang muncul dua kali tidak mendapat background warna yang sama*

c. *Di fungsi calculateFibo angka count yang dikirimkan dari fungsi calculate akan diolah sehingga akan me return angka fibonacci*

    protected void reset(View view){
        count = 0;
        countFibo = 0;
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
        linear.setBackgroundColor(Color.WHITE);
    }
a. *Disini semua properti angka dan textview akan direset*

b. *kemudian warna background akan diganti menjadi warna putih seperti sedia kala*

    
* # Color

<?xml version="1.0" encoding="utf-8"?>

<resources>
  
    <color name="purple_200">#FFBB86FC</color>
  
    <color name="purple_500">#FF6200EE</color>
    
    <color name="purple_700">#FF3700B3</color>
    
    <color name="teal_200">#FF03DAC5</color>
    
    <color name="teal_700">#FF018786</color>
    
    <color name="yellow">#F2EF1C</color>
    
    <color name="green">#1CF234</color>
    
    <color name="red">#F50A0A</color>
    
    <color name="black">#FF000000</color>
    
    <color name="white">#FFFFFFFF</color>
    
    <integer-array name="warna_background_fibo">
    
        <item>@color/red</item>
        
        <item>@color/yellow</item>
        
        <item>@color/green</item>
        
    </integer-array>
    
</resources>

