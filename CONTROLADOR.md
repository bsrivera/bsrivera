CONTROLADOR
package com.example.r_n_e.controller;

import android.annotation.SuppressLint;
import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.text.InputType;
import android.widget.*;
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import com.example.r_n_e.MainActivity;
import com.example.r_n_e.R;
import com.example.r_n_e.model.UsuarioModel;
import com.example.r_n_e.model.PuntuacionModel;
import com.example.r_n_e.DatabaseHelper2;
import com.example.r_n_e.DatabaseHelper;

/**
* Controlador encargado de gestionar la vista de perfil y orquestar
* la interacción entre usuario, modelo y vista.
*/
public class PerfilActivity extends AppCompatActivity {

   private TextView txtNombre, txtEdad, txtCorreo, txtPuntuacionModulo;
   private LinearLayout layoutPuntuaciones;

   private SharedPreferences preferences;
   private PuntuacionModel puntuacionModel;
   private DatabaseHelper2 dbHelper;
   private DatabaseHelper databaseHelper;

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.perfil);

       // Inicialización de componentes y modelo
       preferences = getSharedPreferences("AppPrefs", MODE_PRIVATE);
       puntuacionModel = new PuntuacionModel(this);
       dbHelper = new DatabaseHelper2(this);
       databaseHelper = new DatabaseHelper(this);

       // Referencias a vistas
       txtNombre = findViewById(R.id.txtNombre);
       txtEdad = findViewById(R.id.txtEdad);
       txtCorreo = findViewById(R.id.txtCorreo);
       txtPuntuacionModulo = findViewById(R.id.txtPuntuacionModulo);
       layoutPuntuaciones = findViewById(R.id.layoutPuntuaciones);

       // Registro de usuario si es necesario
       if (!preferences.getBoolean("usuario_registrado", false)) {
           solicitarDatosUsuario();
       } else {
           cargarDatosUsuario();
       }

       findViewById(R.id.btnBack).setOnClickListener(v -> volverInicio());
       findViewById(R.id.btnVolver).setOnClickListener(v -> mostrarListaModulos());

       mostrarListaModulos();
   }

   // Carga los datos almacenados del usuario en pantalla
   private void cargarDatosUsuario() {
       UsuarioModel usuario = new UsuarioModel(
               preferences.getString("usuario_nombre", "Usuario"),
               preferences.getInt("usuario_edad", 0),
               preferences.getString("usuario_correo", "correo")
       );
       txtNombre.setText("Nombre: " + usuario.getNombre());
       txtEdad.setText("Edad: " + usuario.getEdad());
       txtCorreo.setText("Correo: " + usuario.getCorreo());
   }

   // Genera botones para cada módulo
   @SuppressLint("SetTextI18n")
   private void mostrarListaModulos() {
       layoutPuntuaciones.removeAllViews();
       txtPuntuacionModulo.setText("Selecciona un módulo para ver su puntuación");

       for (int i = 1; i <= 10; i++) {
           Button boton = new Button(this);
           boton.setText("Módulo " + i);
           int finalI = i;
           boton.setOnClickListener(v -> mostrarPuntuacion(finalI));
           layoutPuntuaciones.addView(boton);
       }
   }

   // Muestra las puntuaciones por sección y total
   @SuppressLint("SetTextI18n")
   private void mostrarPuntuacion(int moduloId) {
       layoutPuntuaciones.removeAllViews();
       txtPuntuacionModulo.setText("Puntuaciones del Módulo " + moduloId);
       int total = 0;

       for (int i = 1; i <= 10; i++) {
           String key = "Modulo" + moduloId + "_Seccion" + i;
           int puntuacion = puntuacionModel.obtenerPuntuacion(key);
           if (puntuacion != -1) {
               if (!dbHelper.scoreExists(moduloId, i)) dbHelper.insertScore(moduloId, i, puntuacion);
               else dbHelper.updateScore(moduloId, i, puntuacion);

               total += puntuacion;

               TextView txt = new TextView(this);
               txt.setText("Sección " + i + ": " + puntuacion);
               layoutPuntuaciones.addView(txt);
           }
       }

       TextView resumen = new TextView(this);
       resumen.setText("Puntuación total del Módulo " + moduloId + ": " + total);
       resumen.setTypeface(null, android.graphics.Typeface.BOLD);
       layoutPuntuaciones.addView(resumen);
   }

   // Muestra el formulario de registro si no hay usuario guardado
   private void solicitarDatosUsuario() {
       AlertDialog.Builder builder = new AlertDialog.Builder(this);
       builder.setTitle("Registro de Usuario");

       LinearLayout layout = new LinearLayout(this);
       layout.setOrientation(LinearLayout.VERTICAL);
       layout.setPadding(50, 30, 50, 30);

       EditText inputCorreo = new EditText(this);
       EditText inputNombre = new EditText(this);
       EditText inputEdad = new EditText(this);

       inputCorreo.setHint("Correo");
       inputNombre.setHint("Nombre");
       inputEdad.setHint("Edad");
       inputEdad.setInputType(InputType.TYPE_CLASS_NUMBER);

       layout.addView(inputCorreo);
       layout.addView(inputNombre);
       layout.addView(inputEdad);

       builder.setView(layout);
       builder.setPositiveButton("Guardar", (dialog, which) -> {
           String correo = inputCorreo.getText().toString().trim();
           String nombre = inputNombre.getText().toString().trim();
           String edadStr = inputEdad.getText().toString().trim();

           if (!correo.isEmpty() && !nombre.isEmpty() && !edadStr.isEmpty()) {
               int edad = Integer.parseInt(edadStr);
               dbHelper.insertUser(correo, nombre, edad);
               SharedPreferences.Editor editor = preferences.edit();
               editor.putBoolean("usuario_registrado", true);
               editor.putString("usuario_correo", correo);
               editor.putString("usuario_nombre", nombre);
               editor.putInt("usuario_edad", edad);
               editor.apply();
               cargarDatosUsuario();
           } else {
               Toast.makeText(this, "Todos los campos son obligatorios", Toast.LENGTH_SHORT).show();
           }
       });

       builder.setNegativeButton("Cancelar", (dialog, which) -> dialog.dismiss());
       builder.setCancelable(false);
       builder.show();
   }

   private void volverInicio() {
       Intent intent = new Intent(this, MainActivity.class);
       intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP | Intent.FLAG_ACTIVITY_NEW_TASK);
       startActivity(intent);
       finish();
   }
}
<img width="525" height="807" alt="image" src="https://github.com/user-attachments/assets/0532de49-4c29-4e58-aedb-3668264327da" />
<img width="530" height="805" alt="image" src="https://github.com/user-attachments/assets/a721db2f-6e1f-440d-b8a5-8407a877d5dc" />
<img width="529" height="804" alt="image" src="https://github.com/user-attachments/assets/7737c16d-4a99-4191-a64c-af2e46abb70d" />
<img width="531" height="333" alt="image" src="https://github.com/user-attachments/assets/e14ec543-3714-4ca4-861e-a33029ff6ebb" />


