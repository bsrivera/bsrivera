VISTA (PERFIL USUARIO)
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".Perfil">

   <!-- ScrollView para contenido desplazable -->
   <ScrollView
       android:layout_width="match_parent"
       android:layout_height="0dp"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintEnd_toEndOf="parent">

       <LinearLayout
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:orientation="vertical"
           android:padding="16dp">

           <!-- Contenedor para el botón de retroceso y el logo en una sola línea -->
           <androidx.constraintlayout.widget.ConstraintLayout
               android:layout_width="match_parent"
               android:layout_height="wrap_content">

               <!-- Botón de retroceso a MainActivity -->
               <ImageButton
                   android:id="@+id/btnBack"
                   android:layout_width="wrap_content"
                   android:layout_height="wrap_content"
                   android:layout_margin="16dp"
                   android:contentDescription="Botón de retroceso"
                   android:src="@drawable/back"
                   android:backgroundTint="@color/white"
                   app:layout_constraintStart_toStartOf="parent"
                   app:layout_constraintTop_toTopOf="parent"
                   tools:ignore="HardcodedText,TouchTargetSizeCheck" />

               <!-- Logo NASA -->
               <ImageView
                   android:id="@+id/logo_nasa"
                   android:layout_width="100dp"
                   android:layout_height="57dp"
                   android:contentDescription="NASA Logo"
                   android:src="@drawable/logo_nasa"
                   android:layout_marginTop="15dp"
                   app:layout_constraintStart_toEndOf="@id/btnBack"
                   app:layout_constraintTop_toTopOf="parent"
                   app:layout_constraintBottom_toBottomOf="parent"
                   android:layout_marginStart="66dp"
                   tools:ignore="HardcodedText" />

           </androidx.constraintlayout.widget.ConstraintLayout>

           <!-- Mostrar datos de usuario con estilo -->
           <LinearLayout
               android:orientation="vertical"
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:layout_marginTop="20dp"
               android:layout_gravity="start"
               android:padding="10dp">

               <!-- Nombre -->
               <TextView
                   android:id="@+id/txtNombre"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:text="Nombre: "
                   android:textSize="18sp"
                   android:textColor="@android:color/black"
                   android:layout_marginBottom="8dp"
                   android:background="@drawable/rounded_border"
                   android:padding="10dp" />

               <!-- Edad -->
               <TextView
                   android:id="@+id/txtEdad"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:text="Edad: "
                   android:textSize="18sp"
                   android:textColor="@android:color/black"
                   android:layout_marginBottom="8dp"
                   android:background="@drawable/rounded_border"
                   android:padding="10dp" />

               <!-- Correo -->
               <TextView
                   android:id="@+id/txtCorreo"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:text="Correo: "
                   android:textSize="18sp"
                   android:textColor="@android:color/black"
                   android:layout_marginBottom="20dp"
                   android:background="@drawable/rounded_border"
                   android:padding="10dp" />

           </LinearLayout>

           <!-- Título -->
           <TextView
               android:id="@+id/txtPuntuacionModulo"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_marginTop="40dp"
               android:text="Selecciona un módulo para ver su puntuación"
               android:textSize="16sp"
               android:textAlignment="center"
               android:layout_gravity="center"
               tools:ignore="HardcodedText" />

           <!-- Layout para mostrar las puntuaciones -->
           <LinearLayout
               android:id="@+id/layoutPuntuaciones"
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:orientation="vertical"
               android:layout_marginTop="16dp" />

           <!-- Botón para volver a la lista de módulos -->
           <Button
               android:id="@+id/btnVolver"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_marginTop="16dp"
               android:layout_gravity="center"
               android:text="Volver a la lista de módulos"
               tools:ignore="HardcodedText,TextContrastCheck" />

       </LinearLayout>
   </ScrollView>
</androidx.constraintlayout.widget.ConstraintLayout>
<img width="529" height="760" alt="Captura de pantalla 2025-07-11 015748" src="https://github.com/user-attachments/assets/7cf6f7d2-9240-46e1-9cd6-859128a3138d" />
<img width="529" height="761" alt="image" src="https://github.com/user-attachments/assets/50c64951-e7e5-4f71-9795-0cbdb2344a35" />
<img width="528" height="518" alt="image" src="https://github.com/user-attachments/assets/99c6c7f8-8d54-406d-8ec4-a6da03787bd9" />

