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

<h1>Tipos de preferencias</h1>

<table>
<tr>
  <td><strong>Tipo de preferencias</strong></td>
  <td><strong>Tipo de dato</strong></td>
  <td><strong>Tamaño(bytes)</strong></td>
</tr>

<tr>
  <td>Bool</td>
  <td>bool</td>
  <td>1</td>
</tr>

<tr>
  <td>Char</td>
  <td>int8_t</td>
  <td>1</td>
</tr>

<tr>
  <td>UChar</td>
  <td>uint8_t</td>
  <td>1</td>
</tr>
  
  <tr>
  <td>Short</td>
  <td>int16_t</td>
  <td>2</td>
</tr>
  <tr>
  <td>UShort</td>
  <td>uint16_t</td>
  <td>2</td>
</tr>
  <tr>
  <td>Int</td>
  <td>int32_t</td>
  <td>4</td>
</tr>
  <tr>
  <td>UInt</td>
  <td>uint32_t</td>
  <td>4</td>
</tr>
  <tr>
  <td>Long</td>
  <td>int32_t</td>
  <td>4</td>
</tr>
  <tr>
  <td>ULong</td>
  <td>uint32_t</td>
  <td>4</td>
</tr>
  <tr>
  <td>Long64</td>
  <td>int64_t</td>
  <td>8</td>
</tr>
  <tr>
  <td>ULong64</td>
  <td>uint64_t</td>
  <td>8</td>
</tr>
  <tr>
  <td>Float</td>
  <td>float_t</td>
  <td>8</td>
</tr>
  <tr>
  <td>Double</td>
  <td>double_t</td>
  <td>8</td>
</tr>
  <tr>
  <td>String</td>
  <td>String</td>
  <td>Variable</td>
</tr>
  <tr>
  <td>Bytes</td>
  <td>uint8_t</td>
  <td>Variable</td>
</tr>
</table>

</body>
</html>

  </tr>

</table>
