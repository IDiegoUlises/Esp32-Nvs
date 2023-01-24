# Esp32-Nvs

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

  digitalWrite(led, save);

  //Lee el boton
  int estado = digitalRead(boton);

  if (estado == HIGH)
  {
    //Cambia el estado actual
    pulsado = !pulsado;
    
    //Guarda en la memoria la variable el estado de pulsado
    preferences.putBool("variable", pulsado);
    delay(1000); //Espera 1 segundo
  }
}
