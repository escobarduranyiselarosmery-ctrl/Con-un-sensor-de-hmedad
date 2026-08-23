# Indicador de Temperatura con Sensor TMP y LEDs – Arduino UNO

## 📖 Descripción
Proyecto que utiliza un sensor de temperatura TMP conectado al Arduino UNO para medir la temperatura ambiente y mostrar el resultado mediante tres LEDs (verde, amarillo y rojo).  
Cada LED indica un rango de temperatura: baja, media o alta.

## 🧰 Materiales
- Arduino UNO R3  
- Sensor de temperatura TMP36 o TMP37  
- 3 LEDs (verde, amarillo, rojo)  
- 3 resistencias de 220 Ω  
- Protoboard  
- Cables jumper  

## 🔌 Conexiones
- TMP → A0 (pin de señal)  
- TMP → 5 V y GND  
- LED verde → D2  
- LED amarillo → D3  
- LED rojo → D4  
- Todos los cátodos de los LEDs → GND (con resistencias)

## 💻 Código
```cpp
int sensorPin = A0;
int ledVerde = 2;
int ledAmarillo = 3;
int ledRojo = 4;
float temperatura;

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarillo, OUTPUT);
  pinMode(ledRojo, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int valor = analogRead(sensorPin);
  temperatura = (valor * 5.0 / 1023.0 - 0.5) * 100.0; // Conversión TMP36

  Serial.print("Temperatura: ");
  Serial.print(temperatura);
  Serial.println(" °C");

  if (temperatura < 25) {
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledAmarillo, LOW);
    digitalWrite(ledRojo, LOW);
  } else if (temperatura >= 25 && temperatura < 30) {
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarillo, HIGH);
    digitalWrite(ledRojo, LOW);
  } else {
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarillo, LOW);
    digitalWrite(ledRojo, HIGH);
  }

  delay(500);
}
