MODELO USUARIO
/**
* Modelo de datos que representa la entidad Usuario.
* Contiene atributos y métodos de acceso para encapsular la información del usuario.
*/
public class UsuarioModel {
   private String nombre;
   private int edad;
   private String correo;

   public UsuarioModel(String nombre, int edad, String correo) {
       this.nombre = nombre;
       this.edad = edad;
       this.correo = correo;
   }

   // Métodos de acceso
   public String getNombre() { return nombre; }
   public int getEdad() { return edad; }
   public String getCorreo() { return correo; }
}

<img width="755" height="498" alt="Captura de pantalla 2025-07-11 013400" src="https://github.com/user-attachments/assets/fd1426e4-8646-4c83-8105-97d48cf2653d" />

MODELO PUNTUACION
package com.example.r_n_e.model;

import android.content.Context;
import android.content.SharedPreferences;

/**
* Modelo encargado de gestionar las puntuaciones mediante SharedPreferences.
* Encapsula el acceso a almacenamiento local.
*/
public class PuntuacionModel {
   private SharedPreferences sharedPreferences;

   public PuntuacionModel(Context context) {
       this.sharedPreferences = context.getSharedPreferences("Puntuaciones", Context.MODE_PRIVATE);
   }

   // Devuelve la puntuación de una clave específica
   public int obtenerPuntuacion(String clave) {
       return sharedPreferences.getInt(clave, -1);
   }

   // Guarda la puntuación para una clave dada
   public void guardarPuntuacion(String clave, int valor) {
       SharedPreferences.Editor editor = sharedPreferences.edit();
       editor.putInt(clave, valor);
       editor.apply();
   }
}
<img width="756" height="649" alt="Captura de pantalla 2025-07-11 015451" src="https://github.com/user-attachments/assets/bf8f9648-f14f-4809-8128-559ab302b890" />
