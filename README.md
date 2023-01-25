# Esp32 Nvs

Para declarar el objeto
```c++
Preferences preferences;
```

Abre preferencias con el nombre app
```c++
preferences.begin("app", false);
```

Guarda el estado en la memoria con nombre variable
```c++
preferences.putBool("variable", true);
```

Para obtener la informacion de la memoria variable en caso de no existir por defecto sera falso
```c++
int pulsado = preferences.getBool("variable", false);
```

Para cerrar las preferencias
```c++
preferences.end();
```

### Codigo
```c++
#include <Preferences.h>

//Declara los puertos que usara el led y el boton
int led = 26;
int boton = 27;

//Crea una variable para saber el estado del boton
boolean pulsado = false;

//Declara el objeto preferencias
Preferences preferences;

void setup()
{
  //Configuracion como entradas y salidas
  pinMode(led, OUTPUT);
  pinMode(boton, INPUT);

  //Inicia el espacio de nombres y el segundo valor debe ser falso
  preferences.begin("app", false);
}

void loop()
{
  //Obtiene el valor en la memoria variable y si no existe es falso
  pulsado = preferences.getBool("variable", false);
 
  //Prende o apaga el led que dependera del estado de la memoria
  digitalWrite(led, pulsado);
  //delay(500);

  //Lee el estado del boton
  int estado = digitalRead(boton);

  //Realiza una comparacion para saber si el boton fue presionado
  if (estado == HIGH)
  {
    //Cambia el estado contrario
    pulsado = !pulsado;

    //Guarda en la memoria la variable el estado de pulsado
    preferences.putBool("variable", pulsado);
    
    //Termina las preferencias
    references.end();

    //Hace un retardo de un segundo importante ya que esta memoria tiene un limite de escritura
    delay(1000); 
  }
}
```

### Codigo para eliminar todos los espacio de nombre dentro del esp32

```c++
#include <nvs_flash.h>

void setup() {
  nvs_flash_erase(); // erase the NVS partition and...
  nvs_flash_init(); // initialize the NVS partition.
  while(true);
}

void loop() {
}
``` 


<html>

<body>

<h1>Listado de cursos</h1>

<table>
<tr>
  <td><strong>Curso</strong></td>
  <td><strong>Horas</strong></td>
  <td><strong>Horario</strong></td>
</tr>

<tr>
  <td>CSS</td>
  <td>20</td>
  <td>16:00 - 20:00</td>
</tr>

<tr>
  <td>HTML</td>
  <td>20</td>
  <td>16:00 - 20:00</td>
</tr>

<tr>
  <td>Dreamweaver</td>
  <td>60</td>
  <td>16:00 - 20:00</td>
</tr>
</table>

</body>
</html>

  </tr>

</table>
