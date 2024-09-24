# Tempreture_and_Humidity_sensore
# this is the code of sensore

const int analogIn = A0;  // Temperature sensor connected to A0
const int humiditySensorPin = A1;  // Humidity sensor connected to A1

// Defining Variables
int rawValue = 0;
double voltage = 0;
double tempC = 0;
double tempF = 0;
int humiditySensorOutput = 0;

void setup() {
  Serial.begin(9600);
  pinMode(analogIn, INPUT);  // Corrected A1 to analogIn
  pinMode(humiditySensorPin, INPUT);  // Set humidity sensor pin as input
}

void loop() {
  // Read temperature
  rawValue = analogRead(analogIn);
  voltage = (rawValue / 1023.0) * 5000;  // Convert to millivolts
  tempC = (voltage - 500) * 0.1;  // Convert to Celsius (500 is the offset)
  tempF = (tempC * 1.8) + 32;  // Convert to Fahrenheit

  // Print temperature values
  Serial.print("Raw Value = ");
  Serial.print(rawValue);
  Serial.print("\t Temperature in C = ");
  Serial.print(tempC, 1);
  Serial.print("\t Temperature in F = ");
  Serial.println(tempF, 1);

  // Read humidity
  humiditySensorOutput = analogRead(humiditySensorPin);
  int humidityPercentage = map(humiditySensorOutput, 0, 1023, 0, 100);  // Map the raw value to a percentage

  // Print humidity value
  Serial.print("Humidity = ");
  Serial.print(humidityPercentage);
  Serial.print("%");
  
  // Delay before the next reading
  delay(5000);
}
