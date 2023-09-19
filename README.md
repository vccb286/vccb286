#define BLYNK_TEMPLATE_ID "TMPL6r4VyMRQH"
#define BLYNK_TEMPLATE_NAME "Quickstart Template"
#define BLYNK_AUTH_TOKEN "SZIxdWMHaMJ_m5eN19GFWTPJC8Pvgw7W"

#define BLYNK_PRINT Serial

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

#define PIN_RELAY  D4

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "Phisit";
char pass[] = "00000000";

int soil_PIN = A0;
int val;

void setup()
{
  pinMode (PIN_RELAY, OUTPUT);
  pinMode(soil_PIN, INPUT);
  Serial.begin(9600);
  Blynk.begin(auth, ssid, pass);
}

void loop()
{
  Blynk.run();

  val = analogRead(soil_PIN);
  Serial.print("val = ");
  Serial.println(val);
  Blynk.virtualWrite(V0, val);

  if (val > 700)
  {
    digitalWrite(PIN_RELAY, LOW);
  }
  else
  {
    digitalWrite(PIN_RELAY, HIGH);
  }  

  delay(100);
}
