# Android_convert_money
### This is a project in Android studio using kotlin : using binding and the spinner

![image](https://github.com/juliaigz/Android_convert_money/assets/40221707/4bbd8fd4-a60d-4acf-803a-b1a888f27141)


´´´bash
class MainActivity : AppCompatActivity() {
    lateinit var convert:Button
    lateinit var  reset:Button
    lateinit var  total:TextView
    lateinit var eudol:String
    lateinit var monto:EditText
    lateinit var spinner:Spinner
    lateinit var  binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        convert = binding.convert
        reset= binding.reset
        total = binding.total
        monto = binding.saldo

        spinner = binding.spinner
        // Create an ArrayAdapter using the string array and a default spinner layout
        ArrayAdapter.createFromResource(this,R.array.divisa,
            android.R.layout.simple_spinner_item).also { adapter ->
            // Specify the layout to use when the list of choices appears
            adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)
            // Apply the adapter to the spinner
            spinner.adapter = adapter

            //controlamos por accion si es dolar o euro
            spinner.onItemSelectedListener = object : AdapterView.OnItemSelectedListener {
                override fun onItemSelected(parent: AdapterView<*>, view: View?, position: Int, id: Long) {
                    var selectedValue = parent.getItemAtPosition(position) as String
                    eudol = selectedValue
                }

                override fun onNothingSelected(parent: AdapterView<*>) {
                    // Acciones a realizar cuando no se ha seleccionado nada en el Spinner (opcional)
                }
            }

            //Accion para que imprima el total dolar o euro
            convert.setOnClickListener(View.OnClickListener { v: View ->
                if (monto.text.toString().isNotEmpty()) {
                    try {
                        if (eudol == "DOLAR") {
                            var montoNumerico = monto.text.toString().toDouble()
                            montoNumerico *= 800
                            total.text = "$montoNumerico pesos en Dolares"
                        }
                        if (eudol == "EURO") {
                            var montoNumerico = monto.text.toString().toDouble()
                            montoNumerico *= 900
                            total.text = "$montoNumerico pesos en Euros"
                        }
                    } catch (e: NumberFormatException) {
                        total.text = "Error de conversión"
                    }
                } else {
                    total.text = "Debe ingresar un valor"
                }
            })

            //limpiar campos
            reset.setOnClickListener(View.OnClickListener { v: View ->
                monto.setText("0")
                total.text = ""
                try {
                    val montoNumerico = monto.text.toString().toDouble()
                    total.text = montoNumerico.toString()
                } catch (e: NumberFormatException) {
                    total.text = "0"
                }
            })
        }
    }
}

´´´

xml

´´´bash

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/total"
        android:layout_width="131dp"
        android:layout_height="55dp"
        android:text="Bienvenido al convertidor"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.934" />

    <Spinner
        android:id="@+id/spinner"
        android:layout_width="198dp"
        android:layout_height="57dp"

        android:layout_marginEnd="3dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/saldo"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.566" />

    <EditText
        android:id="@+id/saldo"
        android:layout_width="213dp"
        android:layout_height="58dp"
        android:ems="10"
        android:inputType="number"
        android:text="0"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.565" />

    <Button
        android:id="@+id/convert"
        android:layout_width="114dp"
        android:layout_height="61dp"
        android:layout_marginTop="100dp"
        android:text="Convert"
        app:layout_constraintEnd_toStartOf="@+id/reset"
        app:layout_constraintHorizontal_bias="0.409"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/saldo" />

    <Button
        android:id="@+id/reset"
        android:layout_width="115dp"
        android:layout_height="59dp"
        android:layout_marginTop="96dp"
        android:layout_marginEnd="64dp"
        android:text="Reset"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="@+id/spinner" />

    <ImageView
        android:id="@+id/imageView2"
        android:layout_width="124dp"
        android:layout_height="123dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.515"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.287"
        app:srcCompat="@drawable/money"
        tools:srcCompat="@drawable/money" />

</androidx.constraintlayout.widget.ConstraintLayout>

´´´


