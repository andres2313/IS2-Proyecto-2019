# IS2-Proyecto-2019
Proyecto de Ingenieria de Software II con NodeMCU y Raspberry Pi mediante MQTT

Leer el ejemplo de envio de informacion antes de subir el codigo

#include <Wire.h>
#include <ESP8266WiFi.h>
#include "Adafruit_MQTT.h"
#include "Adafruit_MQTT_Client.h"

ADC_MODE(ADC_VCC);

#define WLAN_SSID       "CWC-9307524"
#define WLAN_PASS       "mffksgMG57rwbhjkheshjkdekh"

#define HOST        "192.168.0.32"
#define PORT        1883
#define USERNAME    "username"
#define PASSWORD    "12345678" 

const int intervall = 10000;
int pin_mq = 4;

WiFiClient client;
Adafruit_MQTT_Client mqtt(&client, HOST, PORT, USERNAME, PASSWORD);


Adafruit_MQTT_Publish gas = Adafruit_MQTT_Publish(&mqtt, "gas");
Adafruit_MQTT_Publish fecha = Adafruit_MQTT_Publish(&mqtt, "fecha");
void MQTT_connect();


void setup() {
  WiFi.forceSleepWake();
  WiFi.mode(WIFI_STA);
  Serial.begin(115200);
  Serial.print("Connecting to ");
  Serial.println(WLAN_SSID);

  WiFi.begin(WLAN_SSID, WLAN_PASS);
  while (WiFi.status() != WL_CONNECTED) 
  {
    delay(500);
    Serial.print(".");
  }
  
  Serial.println();
  Serial.println("WiFi connected");
  Serial.println("IP address: "); Serial.println(WiFi.localIP());
  MQTT_connect();
}

void loop() 
{
 boolean mq_estado = digitalRead(pin_mq); //Leemos el sensor
 if(mq_estado){
    gas.publish("Sin presencia de gas");
  } 
  else {
    gas.publish("Gas Dectectado");

    fecha.publish("fdsfsdfsd")
  }
  delay(5000);
}

