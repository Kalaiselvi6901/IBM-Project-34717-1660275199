# IBM-Project-34717-1660275199
# Ardiuno code for temperature sensor(tmp36),buzzer ,led,pir sensor
#define sensorPin A3
int Buzz= 8; // Define Bizzer pin
int LED= 13; // Define LED pin
int PIR= 4; // Define PIR pin
int val= 0; // Initializing the value as zero at the beginning
  
void setup() {
pinMode(sensorPin,INPUT);
pinMode(Buzz, OUTPUT);
pinMode(LED, OUTPUT);
pinMode(PIR, INPUT);
Serial.begin(9600);
}

void loop() {
  // Get a reading from the temperature sensor:
  int reading = analogRead(sensorPin);

  // Convert the reading into voltage:
  float voltage = reading * (5000 / 1024.0);

  // Convert the voltage into the temperature in Celsius:
  float temperature = (voltage - 500) / 10;

  // Print the temperature in the Serial Monitor:
  Serial.print(temperature);
  Serial.print(" \xC2\xB0"); // shows degree symbol
  Serial.println("C");

  delay(1000); // wait a second between readings
  if(temperature>40)
  {
  digitalWrite(LED, HIGH); // Turn LED ON
  digitalWrite(Buzz, HIGH); // Turn Buzzer ON
  Serial.println("Temperature is High"); // Print this text in Serial Monitor
}
if(temperature<40 && temperature>30)
{
  digitalWrite(LED, LOW);
  digitalWrite(Buzz, LOW);
  Serial.println("Temperature is normal");
}

else 
{
  digitalWrite(LED, LOW);
  digitalWrite(Buzz, LOW);
  Serial.println("Temperature is low");
}

val = digitalRead(PIR); // The value read from PIR pin 4 will be assigned to 'val'
if(val == HIGH){
  digitalWrite(LED, HIGH); // Turn LED ON
  digitalWrite(Buzz, HIGH); // Turn Buzzer ON
  Serial.println("Movement Detected"); // Print this text in Serial Monitor
}
else 
{
  digitalWrite(LED, LOW);
  digitalWrite(Buzz, LOW);
  Serial.println("Movement not Detected");
}
}
