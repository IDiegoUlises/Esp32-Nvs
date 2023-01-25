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

int led = 26;
int boton = 27;

boolean pulsado = false;

Preferences preferences;

void setup()
{
  pinMode(led, OUTPUT);
  pinMode(boton, INPUT);

  //Inicia el espacio de memoria y el segundo valor debe ser falso
  preferences.begin("my-app", false);
}

void loop()
{
  //Obtiene el valor en la memoria variable y si no existe es falso
  pulsado = preferences.getBool("variable", false);

  digitalWrite(led, pulsado);
  delay(500);

  //Lee el boton
  int estado = digitalRead(boton);

  if (estado == HIGH)
  {
    //Cambia el estado actual
    pulsado = !pulsado;
    
    //Guarda en la memoria la variable el estado de pulsado
    preferences.putBool("variable", pulsado);
    references.end();
    delay(1000); //Espera 1 segundo
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
