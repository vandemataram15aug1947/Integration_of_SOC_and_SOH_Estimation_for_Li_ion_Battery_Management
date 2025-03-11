# 🔋 Integration of SOC and SOH Estimation for Li-ion Battery Management

## 📚 Contents

- [Introduction](#introduction)
- [What are SOC and SOH?](#what-are-soc-and-soh)
- [Motivation Behind the Work](#motivation-behind-the-work)
- [Objectives of Work](#objectives-of-work)
- [Hardware Setup](#hardware-setup)
- [Applications](#applications)
- [Conclusion](#conclusion)
- [Scope of Future Work](#scope-of-future-work)
- [References](#references)

## 🔍 **Introduction**

Battery Management Systems (BMS) play a crucial role in modern energy storage applications, ensuring the efficiency, safety, and longevity of batteries. Among various BMS functions, **State of Charge (SOC) and State of Health (SOH)** estimation are key parameters for optimizing battery performance and reliability.

This project focuses on the **Integration of SOC and SOH Estimation Methods for Li-ion Battery Management**, enabling enhanced performance monitoring and predictive maintenance.

---

# 🔋 State of Charge (SOC) of a Battery

The **State of Charge (SOC)** represents the remaining energy in a battery compared to its fully charged state. It is an essential parameter for estimating battery health and performance in various applications, such as electric vehicles, renewable energy storage, and battery management systems (BMS).

## 📌 SOC Calculation Formula

The SOC is mathematically expressed as:

```math
SoC(%) = 100 \times \frac{Q_0 + Q}{Q_{max}}
```

where:

- **`Q₀ (mAh)`** = Initial charge of the battery at a given time
- **`Q (mAh)`** = Charge supplied or delivered (*negative for discharge, positive for charge*)
- **`Qₘₐₓ (mAh)`** = Maximum charge capacity of the battery
- **`SoC₀ (%)`** = Initial SOC of the battery before any charging/discharging occurs

SOC is usually represented as a percentage (%) ranging from **0% (fully discharged)** to **100% (fully charged)**.

---

## 📌 Special Cases of SOC Calculation

### 1️⃣ For a Brand-New Battery

When the battery is new and has not undergone any degradation, the maximum charge capacity (`Qₘₐₓ`) is equal to the rated capacity (`Cᵜ`) as provided by the manufacturer. Additionally, the initial charge of a new battery is typically assumed to be **50%** of its full capacity.

```math
Q_{max} = C_r, \quad Q_0 = 0.5 \times Q_{max}
```

### 2️⃣ For a Fully Charged Battery

When the battery is completely charged, its initial charge is equal to its maximum charge capacity, and the SOC is **100%**.

```math
Q_0 = Q_{max}, \quad SoC_0 = 100\%
```

---

## 📌 SOC Representation

---

## 📌 Importance of SOC Estimation

✔️ **Battery Performance Monitoring:** Helps in tracking available energy.\
✔️ **Efficient Energy Management:** Essential for optimizing power usage in EVs and energy storage systems.\
✔️ **Battery Safety & Longevity:** Prevents overcharging and deep discharging, which can damage battery cells.\
✔️ **Smart Charging Control:** Enables precise charge/discharge cycles to maximize battery efficiency.

---

# 🏥 State of Health (SOH) of a Battery

The **State of Health (SOH)** measures the condition of a battery compared to a new one and considers aging effects. It is a crucial parameter in determining battery performance, degradation, and lifespan.

## 📌 SOH Calculation Formula

The SOH is mathematically expressed as:

```math
SoH(%) = 100 \times \frac{Q_{max}}{C_r}
```

where:

- **`Qₘₐₓ (mAh)`** = Maximum charge available in the battery
- **`Cᵜ`** = Rated capacity of the battery

SOH is usually represented as a percentage (%), where **100% represents a new battery**, and a lower SOH indicates degradation.

---

## 📌 SOH Representation

A battery with lower SOH will discharge more quickly due to degradation, affecting performance and lifespan.

The discharge profile of a secondary battery is affected by its state of health. The lower the SOH, the faster the battery discharges, as illustrated in **Figure 3** below:

---

## 📌 Importance of SOH Estimation

✔️ **Performance Optimization:** Accurate estimation of SOC, SOH, and Depth of Discharge (DOD) enables intelligent battery management systems to optimize charging and discharging strategies, enhancing overall battery performance.\
✔️ **Safety:** Understanding the current state of a battery is crucial for ensuring safe operation. Overcharging, over-discharging, and prolonged operation at extreme SOC levels can lead to safety hazards, including thermal runaway.\
✔️ **Energy Efficiency:** In applications such as renewable energy storage and electric vehicles, knowing the SOC and DOD helps in efficient utilization of stored energy, reducing waste and increasing overall energy efficiency.

---
## 🎯 Motivation Behind the Work

- **Performance Optimization**: Accurate estimation of SOC, SOH, and DOD is essential for developing **intelligent battery management systems**. These estimations help in optimizing charge and discharge cycles, ensuring maximum efficiency and prolonged battery life.
- **Safety**: Monitoring SOC and SOH is critical to **prevent dangerous battery conditions** such as overcharging and deep discharging. Ensuring batteries operate within safe limits reduces risks like **thermal runaway, overheating, and short circuits**.
- **Energy Efficiency**: SOC and DOD data enable **smart energy utilization**, reducing energy wastage and improving the efficiency of applications like **renewable energy storage, electric vehicles (EVs), and smart grids**.
- **Predictive Maintenance**: By continuously monitoring SOH, it is possible to **predict battery degradation trends** and replace failing batteries before they impact system performance.

---

## 🎯 **Objectives of Work**

- Develop a **robust method for estimating SOC, SOH, and DOD** to ensure real-time monitoring and control.
- Implement **efficient charge/discharge strategies** to improve the performance and lifespan of Li-ion batteries.
- Utilize **advanced algorithms** to enhance the accuracy of SOC and SOH measurements.
- Ensure **safety and reliability** in battery-powered applications by preventing overcharging and excessive discharge.
- Facilitate **predictive maintenance** through real-time monitoring and data analytics.

---

## 🛠 **Hardware Setup**

The hardware setup for this project includes:

- **Battery Pack**: Lithium-ion battery cells
- **BMS (Battery Management System)**: To monitor voltage, current, and temperature
- **Microcontroller or Any Kind of Arduino**: For real-time data processing
- **Sensors**: To measure charge/discharge cycles
- **Communication Interface**: For data logging and monitoring

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Integration_of_SOC_and_SOH_Estimation_for_Li_ion_Battery_Management/blob/7ed1b5c38707df8a6707ec54b2db44140c435477/Photos/Hardware%20Setup.jpg" width="400">
</p>  

<p align="center"><b>Figure 4:</b> Hardware Setup</p>  

---

# **Code Implementation**

### **Main Loop for SOC and SOH*
Below is the main loop implementation for  for SOC and SOH:

```c
// For IOT
#include "ThingSpeak.h"
#include <ESP8266WiFi.h>

// For Temprature Sensor
#include <OneWire.h>
#include <DallasTemperature.h>


// Board pin definition
const int analog_sensor = A0;

// Analog multiplexer pins
const int pin0 = D0;  // ---- C0 - Voltage Sensor
const int pin1 = D1;  // ----- C1 - Current Sensor
const int pin2 = D2;
const int pin3 = D3;

// Connected loads
const int pin4 = D6;  // Relay 1, Load 1
const int pin5 = D7;  // Relay 2, Load 2

// Buzzer
const int pin6 = D5;

// LED
const int pin7 = D4;

// Temperature Sensor
// Data wire is connected to the Arduino digital pin 4
const int ONE_WIRE_BUS = D8;

//ThingSpeak Patameter's
// Replace with your network credentials
const char *ssid = "Vande";
const char *password = "Password";

// Replace with your ThingSpeak channel details
const char *thingSpeakApiKey = "GJQ3JGALW07HE5S0";
const unsigned long channelNumber = 2388793;
int frame_interval = 0;

// ThingSpeak Connection clint
WiFiClient client;

// Delay times
unsigned long LED_DELAY_TIME = 2000;     // ms
unsigned long LED_BLINK_DELAY_TIME = 100;     // ms
unsigned long LED_NUMBER_OF_BLINK = 2;
unsigned long Buzz_DELAY_TIME = 1000;     // ms
unsigned long Buzz_BLINK_DELAY_TIME = 1000;     // ms
unsigned long Buzz_NUMBER_OF_Buzz = 1;
unsigned long LOAD1_DELAY_TIME = 1000;   // ms
unsigned long LOAD2_DELAY_TIME = 2000;   // ms
unsigned long FRAME_INTERVAL = 1000;    // ms  
unsigned long THINGSPEAK_FRAME_INTERVAL = 3000;    // ms  
unsigned long BATTERY_SOC_SOH_DELAY_TIME = 10;     // ms

// LED use blink count
static int blinkCount = 0;
static int BuzzCount = 0;

// Using millis to support time-based decision
// unsigned long previousMillis = 0;
unsigned long LED_previousMillis = 0;    // To animate blinking
unsigned long Buzzer_previousMillis = 0;  // To animate Buzzer
unsigned long Frame_previousMillis = 0;  // for processing some function, to avoid 0 at reset decleared static 
unsigned long Load1_previousMillis = 0; // for processing some function
unsigned long Load2_previousMillis = 0; // for processing some function
unsigned long battery_soc_soh_previousMillis = 0; // for processing battery function
unsigned long battery_soc_soh_previousMillis_for_cal = 0; // only used for real time capacity
unsigned long thingspeak_frame_previousMillis = 0; // only used for real time IOT data send

// master fault
bool isFault = false;
// Setup a oneWire instance to communicate with any OneWire devices
OneWire oneWire(ONE_WIRE_BUS);

// Pass our oneWire reference to Dallas Temperature sensor 
DallasTemperature sensors(&oneWire);

//All Battery parameters
// Battery Specification
const float BATTERY_MAX_VOLT    =   7.45;
const float BATTERY_MIN_VOLT    =   6.8;
const float BATTERY_CAPACITY    =   5000;
const float BATTERY_mAh_SOC_SOH_RECALLIBRATION = 0.01;

// Fault Confinguration fconfig
// Voltage Range 
const float BATTERY_FAULT_MAX_VOLT    =   8;
const float BATTERY_FAULT_MIN_VOLT    =   5.5;

// Temp Range
const float BATTERY_FAULT_MAX_TEMP    =   50;
const float BATTERY_FAULT_MIN_TEMP    =   15;

float BATTERY_SOC = 50;             
static float BATTERY_SOH = 50;            
float BATTERY_DOD = 50;            

float Voltage = 0;
float Current_DC = 0;
float Temprature_F = 0;
float Temprature_C = 0;
int Accumulated_Capacity = 0;

// for soc soh callibration
bool needBattCallibration = false;

// BATTERY_STATS BatteryStats;

//Resistor Constant for voltage measurement
const double VoltageConstant = ((30000.0 + 7500.0)/(1024.0 * 7500.0));           // R1 30000.0, R2 7500.0 multyplying outside refVolt 5.0
const double CurrentConstant = (5.0/1024.0);

// voltage and current max array
#define VOLTAGE_CURRENT_MAX_ARRAY 100
#define BATT_CURR_STATUS_MAX_ARRAY 101
// SOC cellVolt Capacity table  
static const int arr_soc[BATT_CURR_STATUS_MAX_ARRAY] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 
                                                        21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 
                                                        41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 
                                                        61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 
                                                        81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100};

static const float arr_cellVolt[BATT_CURR_STATUS_MAX_ARRAY] = {6.8, 6.806, 6.813, 6.819, 6.826, 6.832, 6.839, 6.845, 6.852, 6.858, 
                                                              6.865, 6.871, 6.878, 6.884, 6.891, 6.897, 6.904, 6.91, 6.917, 6.923, 
                                                              6.93, 6.936, 6.943, 6.949, 6.956, 6.962, 6.969, 6.975, 6.982, 6.988, 
                                                              6.995, 7.001, 7.008, 7.014, 7.021, 7.027, 7.034, 7.04, 7.047, 7.053, 
                                                              7.06, 7.066, 7.073, 7.079, 7.086, 7.092, 7.099, 7.105, 7.112, 7.118, 
                                                              7.125, 7.131, 7.138, 7.144, 7.151, 7.157, 7.164, 7.17, 7.177, 7.183, 
                                                              7.19, 7.196, 7.203, 7.209, 7.216, 7.222, 7.229, 7.235, 7.242, 7.248, 
                                                              7.255, 7.261, 7.268, 7.274, 7.281, 7.287, 7.294, 7.3, 7.307, 7.313, 
                                                              7.32, 7.326, 7.333, 7.339, 7.346, 7.352, 7.359, 7.365, 7.372, 7.378, 
                                                              7.385, 7.391, 7.398, 7.404, 7.411, 7.417, 7.424, 7.43, 7.437, 7.443, 7.45};

static const float arr_capacity[BATT_CURR_STATUS_MAX_ARRAY] = {0.0, 0.05, 0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45, 0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95, 1.0, 
                                                              1.05, 1.1, 1.15, 1.2, 1.25, 1.3, 1.35, 1.4, 1.45, 1.5, 1.55, 1.6, 1.65, 1.7, 1.75, 1.8, 1.85, 1.9, 1.95, 2.0, 
                                                              2.05, 2.1, 2.15, 2.2, 2.25, 2.3, 2.35, 2.4, 2.45, 2.5, 2.55, 2.6, 2.65, 2.7, 2.75, 2.8, 2.85, 2.9, 2.95, 3.0, 
                                                              3.05, 3.1, 3.15, 3.2, 3.25, 3.3, 3.35, 3.4, 3.45, 3.5, 3.55, 3.6, 3.65, 3.7, 3.75, 3.8, 3.85, 3.9, 3.95, 4.0, 
                                                              4.05, 4.1, 4.15, 4.2, 4.25, 4.3, 4.35, 4.4, 4.45, 4.5, 4.55, 4.6, 4.65, 4.7, 4.75, 4.8, 4.85, 4.9, 4.95, 5.0};

//System Enum
enum systemProcess {
  INIT_STATE = 0,
  PROCESS_START,
  PROCESS_STATE,
  FAULT_STATE,
  RESTART,
  DEEP_SLEEP
};

systemProcess systemCurStates = INIT_STATE;

// Analog read voltage, temp, current
enum AnalogSense {
  CURRENT = 0,
  VOLTAGE
  // TEMPERATURE
};

// Load enums
enum StartStop {
  STOP = 0,
  START
};

struct LoadStatus {
  StartStop LOAD1_STATUS;
  StartStop LOAD2_STATUS;
  StartStop LED;
  StartStop Buzzer;
};

LoadStatus loadStatus;

enum ConnectedLoad {
  LOAD1 = 0,
  LOAD2
};

void setCurrentBattState(){
  // Upper Cut
  int i;
  for(i = 0; i <= BATT_CURR_STATUS_MAX_ARRAY; i++){
    if(Voltage <= arr_cellVolt[i]){
      break;
    }
   }
  //lower cut
  int j;
  for(j = 0; j <= BATT_CURR_STATUS_MAX_ARRAY; j++){
    if(Voltage >= arr_cellVolt[j]){
      break;
    }
  }
  // setting avedrage soc and capacity to initiate battery status
  BATTERY_SOC = (arr_soc[i]+arr_soc[j])/2;
  BATTERY_DOD = 100 - BATTERY_SOC;
  Accumulated_Capacity = (int) ((arr_capacity[i]+arr_capacity[j])/2)*1000;
}

void setLED(StartStop status){
  // Setting LED 
  digitalWrite(pin7, status);
  loadStatus.LED = status;
}

void setBuzzer(StartStop status){
  // Setting Buzzer
  digitalWrite(pin6, status);
  loadStatus.Buzzer = status;
}

void setLoad(ConnectedLoad load, StartStop status) {
  switch (load) {
    case LOAD1:
      digitalWrite(pin4, !status);
      loadStatus.LOAD1_STATUS = status;
      break;
    case LOAD2:
      digitalWrite(pin5, !status);
      loadStatus.LOAD2_STATUS = status;
      break;
  }
}

// Sensor reading for user using analog mux
int readSensor(AnalogSense sensor) {
  int value = 0;
  switch (sensor) {
    case VOLTAGE:
      digitalWrite(pin0, LOW);
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, LOW);
      // applying delay according to response time
      delayMicroseconds(2);
      // Reading sensor value
      value = analogRead(analog_sensor);     // Converting read value to desired value
      delayMicroseconds(15);
      // Conversion code will be here
      break;
    case CURRENT:
      digitalWrite(pin0, LOW);
      digitalWrite(pin1, HIGH);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, LOW);
      // applying delay according to response time
      delayMicroseconds(2);
      // Reading sensor value
      value = analogRead(analog_sensor);
      // Conversion code will be here
      break;
    // case TEMPERATURE:
    //   digitalWrite(pin0, HIGH);
    //   digitalWrite(pin1, HIGH);
    //   digitalWrite(pin2, LOW);
    //   digitalWrite(pin3, LOW);
    //   // applying delay according to response time
    //   delayMicroseconds(2);
    //   // Reading sensor value
    //   value = analogRead(analog_sensor);
    //   // Conversion code will be here
    //   break;
  }
  digitalWrite(pin0, LOW);
  digitalWrite(pin1, LOW);
  digitalWrite(pin2, LOW);
  digitalWrite(pin3, LOW);
  return value;
}

void initSystem() {
  // Setting mux pin to low
  digitalWrite(pin0, LOW);
  digitalWrite(pin1, LOW);
  digitalWrite(pin2, LOW);
  digitalWrite(pin3, LOW);

  // Setting LED 
  digitalWrite(pin7, LOW);
  loadStatus.LED = STOP;

  // Setting Buzzer
  digitalWrite(pin6, LOW);
  loadStatus.Buzzer = STOP;

  // Setting load  pull up mode
  digitalWrite(pin4, !LOW);      // Load 1
  loadStatus.LOAD1_STATUS = STOP;
  digitalWrite(pin5, !LOW);      // Load 2
  loadStatus.LOAD2_STATUS = STOP;
}

void setup() {
  // Starting serial comm
  Serial.begin(115200);

  // Start up the library
  sensors.begin();          // for temprature sensor

  // Setting mux pins as output
  pinMode(pin0, OUTPUT);
  pinMode(pin1, OUTPUT);
  pinMode(pin2, OUTPUT);
  pinMode(pin3, OUTPUT);

  // Setting up load (relay) pins
  pinMode(pin4, OUTPUT);
  pinMode(pin5, OUTPUT);

  // Setting up LED pins
  pinMode(pin7, OUTPUT);

  // Setting up Buzzer pins
  pinMode(pin6, OUTPUT);

  //ThingSpeak connection setup
  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");

  ThingSpeak.begin(client);
}

// Voltage and Current Calculation
float CURRENT_CALCULATION(){return (2.5 - ((readSensor(CURRENT) * CurrentConstant)/0.66));}        
float VOLTAGE_CALCULATION(){return ((readSensor(VOLTAGE) * 5) * VoltageConstant);}

bool realStats(){
  bool valueChange = false;
  // previous values
  double preVoltage = Voltage;
  double preCurrent_DC = Current_DC;
  double preTemprature_C = Temprature_C;
  double preTemprature_F = Temprature_F;
  //Updateing Voltage
  for(int i = 0; i < VOLTAGE_CURRENT_MAX_ARRAY; i++) {
    Voltage = Voltage + VOLTAGE_CALCULATION()*0.6;
    delayMicroseconds(1);
  }
  Voltage = Voltage / VOLTAGE_CURRENT_MAX_ARRAY;

  // Updating current
  for(int i = 0; i < VOLTAGE_CURRENT_MAX_ARRAY; i++) {
    Current_DC =  Current_DC + CURRENT_CALCULATION();   
    delayMicroseconds(1);
  }
  Current_DC = Current_DC / VOLTAGE_CURRENT_MAX_ARRAY;
  // Updating temprature
  sensors.requestTemperatures(); // requresing sensor(DS18B20) to read the temprature data 
  Temprature_C = sensors.getTempCByIndex(0);  // reading temprature as celcius
  Temprature_F = sensors.getTempFByIndex(0); // reading temprature as farenheit 

  calculateSOC();
  BATTERY_SOH = calculateSOH(Accumulated_Capacity, BATTERY_CAPACITY);
  BATTERY_DOD = 100 - BATTERY_SOC;

  for(int i = 0; i <= BATT_CURR_STATUS_MAX_ARRAY; i++){
    if(Voltage <= arr_cellVolt[i]){
      if(BATTERY_SOC > arr_soc[i]){
        needBattCallibration = true;
      }
    }
    else{
      needBattCallibration = false;
    }
  }

  if (preVoltage != Voltage || preCurrent_DC != Current_DC || preTemprature_C != Temprature_C || preTemprature_F != Temprature_F){
    valueChange = true;
  }
  return valueChange;
}

bool isTimeOut(unsigned long interval, unsigned long &preMillis) {
  unsigned long currentMillis = millis();  // get the current time

  if (currentMillis - preMillis >= interval) {
    // save the last time the event was triggered
    preMillis = currentMillis;
    return true;
  }

  // check for millis() rollover
  if (currentMillis < preMillis) {
    // millis() has rolled over, reset the last trigger time
    preMillis = currentMillis;
  }

  return false;
}

void animateLED(int numBlinks, unsigned long blinkInterval) {
  unsigned long currentMillis = millis();

  if (currentMillis - LED_previousMillis >= blinkInterval) {
    LED_previousMillis = currentMillis;

    if (blinkCount < numBlinks * 2) {
      // Toggle the LED state
      setLED((blinkCount % 2 == 0) ? START : STOP);

      blinkCount++;

      if (blinkCount == numBlinks * 2) {
        blinkCount = 0; // Reset the blink count
      }
    }
  } else if (blinkCount > 0 && currentMillis < LED_previousMillis) {
    // Reset the blink count if millis() rolls over
    blinkCount = 0;
  }
}

void animateBuzzer(int numBuzz, unsigned long BuzzInterval) {
  unsigned long currentMillis = millis();

  if (currentMillis - LED_previousMillis >= BuzzInterval) {
    Buzzer_previousMillis = currentMillis;

    if (BuzzCount < numBuzz * 2) {
      // Toggle the LED state
      setLED((BuzzCount % 2 == 0) ? START : STOP);

      BuzzCount++;

      if (BuzzCount == numBuzz * 2) {
        BuzzCount = 0; // Reset the blink count
      }
    }
  } else if (BuzzCount > 0 && currentMillis < LED_previousMillis) {
    // Reset the blink count if millis() rolls over
    BuzzCount = 0;
  }
}

void processSystem(){
  switch (systemCurStates) {
  case INIT_STATE:
    Serial.println("Initializing the system!");
    //Changing State
    initSystem();
    setCurrentBattState();
    systemCurStates = PROCESS_START;
    break;
    case PROCESS_START:
      realStats();
      calculateSOC();
      BATTERY_SOH = calculateSOH(Accumulated_Capacity, BATTERY_CAPACITY);
      BATTERY_DOD = 100 - BATTERY_SOC;
      sendFrames();
      IotSendData();
      //Changing state
      systemCurStates = PROCESS_STATE;
    break;
    case PROCESS_STATE:
      // Serial.println("Processing the system!");
      // stopping buzzer while processing
      setBuzzer(STOP);
      // LED Animation parameter working on it led automatically setting on is fault vriable
      LED_DELAY_TIME = 1000;
      LED_NUMBER_OF_BLINK = 2;
      LED_BLINK_DELAY_TIME = 50;
      /*
      if(isTimeOut(LOAD1_DELAY_TIME, Load1_previousMillis)) {
        if (loadStatus.LOAD1_STATUS == STOP) {
          setLoad(LOAD1, START);
        } 
        else {
          setLoad(LOAD1, STOP);
        }
      }
      if(isTimeOut(LOAD2_DELAY_TIME, Load2_previousMillis)) {
        if (loadStatus.LOAD2_STATUS == STOP) {
          setLoad(LOAD2, START);
        } 
        else {
          setLoad(LOAD2, STOP);
        }
      }
*/
      if(isFault){
        systemCurStates = FAULT_STATE;
      }
      break;
      
  case FAULT_STATE:
    // Serial.println("Processing Fault State!");
    // will change state on condition
    // systemCurStates = **states 
    // stopping load when fault
    setLoad(LOAD1, START);
    setLoad(LOAD2, START);
    // setting led if default on
    setLED(STOP);
    // animate buzzer
    Buzz_DELAY_TIME = 1;
    Buzz_NUMBER_OF_Buzz = 2;
    Buzz_BLINK_DELAY_TIME = 200;

    // Monitor parameter to go bach into process state
    if(isFault){
      systemCurStates = FAULT_STATE;
    }
    else{
      systemCurStates = PROCESS_STATE;
    }
    break;
  case RESTART:
    // Serial.println("Going to Restart the board!");
    // will change state on condition
    // systemCurStates = **states 
    break;
  case DEEP_SLEEP:
    // Serial.println("Going for deep sleep!");
    // will change state on condition
    // systemCurStates = **states 
    break;
  }

}

void sendFrames(){
    Serial.print("Volatge = ");
    Serial.print(Voltage);
    Serial.println(" V");
    Serial.print("Current = ");
    Serial.print(Current_DC);
    Serial.println(" mA");
    Serial.print("Temprature = ");
    Serial.print(Temprature_C);
    Serial.println(" C");
    Serial.print("SOC = ");
    Serial.print(BATTERY_SOC);
    Serial.println(" %");
    Serial.print("SOH = ");
    Serial.print(BATTERY_SOH);
    Serial.println(" %");
    Serial.print("DOD = ");
    Serial.print(BATTERY_DOD);
    Serial.println(" %");
    Serial.print("Capacity = ");
    Serial.print(Accumulated_Capacity);
    Serial.println(" mAh");
    // Serial.print("Analog Voltage = ");
    // Serial.println(readSensor(VOLTAGE));
    // Serial.print("Analog Current = ");
    // Serial.println(readSensor(CURRENT));
}

void calculateSOC(){
  // Calculate SOC percentage    SoCt = (SoCt-1) + ((Ic(t) * △t)/Qn)
  BATTERY_SOC = ((BATTERY_SOC - 1)+((Accumulated_Capacity*3600)/BATTERY_CAPACITY));
  if(BATTERY_SOC < 0){
    BATTERY_SOC = 0;
  }
  else if(BATTERY_SOC > 100){
    BATTERY_SOC = 100;
  }
}

float calculateSOH(float actualCapacity, float designCapacity) {
  // Calculate SOH percentage
  return (actualCapacity / designCapacity) * 100.0;
}

float calculateBuildCapacity(unsigned long interval){
  return (Current_DC * interval) / 3600000.0;           // in mAh
}

void IotSendData(){
  // Send data to ThingSpeak
  switch(frame_interval){
    case 0:
      ThingSpeak.writeField(channelNumber, 1, Voltage, thingSpeakApiKey);
      frame_interval++;
      break;
    case 1:
      ThingSpeak.writeField(channelNumber, 2, Current_DC, thingSpeakApiKey);
      frame_interval++;
      break;
    case 2:
      ThingSpeak.writeField(channelNumber, 3, Temprature_C, thingSpeakApiKey);
      frame_interval++;
      break;
    case 3:
      ThingSpeak.writeField(channelNumber, 4, BATTERY_SOC, thingSpeakApiKey);
      frame_interval++;
      break;
    case 4:
      ThingSpeak.writeField(channelNumber, 5, BATTERY_SOH, thingSpeakApiKey);
      frame_interval++;
      break;
    case 5:
      ThingSpeak.writeField(channelNumber, 6, BATTERY_DOD, thingSpeakApiKey);
      frame_interval = 0;
      break;
  }

}

void loop() {
  // running loop
  // battery parameter 
  if(isTimeOut(BATTERY_SOC_SOH_DELAY_TIME, battery_soc_soh_previousMillis)){
    Accumulated_Capacity +=(int) (calculateBuildCapacity(millis() - battery_soc_soh_previousMillis_for_cal))*1000;  // Updating build capacity
    battery_soc_soh_previousMillis_for_cal = millis();
  }

  if(realStats()){
    if(isTimeOut(FRAME_INTERVAL, Frame_previousMillis)){
      sendFrames();
    }

    // continues monitoring parameter for processing
    if(Voltage > BATTERY_FAULT_MAX_VOLT || Voltage < BATTERY_FAULT_MIN_VOLT){
      isFault = true;
    }
    else if(Temprature_C > BATTERY_FAULT_MAX_TEMP || Temprature_C < BATTERY_FAULT_MIN_TEMP){
      isFault = true;
    }
    else{
      isFault = false;
    }

    // Executing process
    processSystem();

    // need battery callibration
    if(needBattCallibration){
      setCurrentBattState();
    }

    // Sending data to IOT
    if(isTimeOut(THINGSPEAK_FRAME_INTERVAL, thingspeak_frame_previousMillis)){
       IotSendData();// Send data to cloud
    }
    // LED Blinking Control
    if(!isTimeOut(LED_DELAY_TIME, LED_previousMillis) && !isFault){
       animateLED(LED_NUMBER_OF_BLINK, LED_BLINK_DELAY_TIME);        
    }
    // Buzzer Buzz Control
    if(!isTimeOut(Buzz_DELAY_TIME, Buzzer_previousMillis) && isFault){
       animateBuzzer(Buzz_NUMBER_OF_Buzz, Buzz_BLINK_DELAY_TIME);        
    }
    // Sending data to serial communication
    if(isTimeOut(FRAME_INTERVAL, Frame_previousMillis)){
      sendFrames();
    }
  }
}
```

---

# **Results and Discussion**

## **Overview**  
This repository contains real-time battery performance data collected using a ThingSpeak-based Battery Monitoring System. The analysis includes key battery parameters such as Voltage, Current, Temperature, State of Charge (SOC), State of Health (SOH), and Depth of Discharge (DOD). The results provide insights into battery stability, tracking performance, and operational health.

# 📊 Battery Monitoring System Data (Set 1)

This repository contains data analysis from a ThingSpeak-based battery monitoring system. Below is a detailed breakdown of the recorded battery parameters.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Integration_of_SOC_and_SOH_Estimation_for_Li_ion_Battery_Management/blob/6c996bfd7e319a762cda0fc1d7e9c2d328040b2e/Photos/Result1.png" width="500">
</p>

<p align="center"><b>Figure 5:</b> System Performance Analysis</p>  

## 🔋 Battery Status Charts

### **1️⃣ Battery Voltage**
- Initial voltage: **~5V**
- Gradual decrease with fluctuations between **0V and 3V**
- Sharp drop to nearly **0V**, followed by a sudden spike back to **~5V**

### **2️⃣ Battery Current**
- Variation between **2.2A and 2.4A**
- Initial fluctuations, followed by stabilization around **2.3A**
- Final decline to **2.2A**

### **3️⃣ Battery Temperature**
- Stable around **0°C**
- Sudden drop to **-100°C** (likely sensor error)
- Returns to **0°C** and remains stable

### **4️⃣ Battery State of Charge (SOC)**
- Remains steady at **100%**
- Minor deviation observed but returns to full charge

## 🔍 Observations & Insights
- **Voltage fluctuations** suggest unstable operation, charging cycles, or load changes.
- **Current variations** indicate varying load conditions.
- **Temperature anomaly (-100°C)** likely caused by a sensor error.
- **SOC stability at 100%** suggests minimal discharge or continuous charging.

# 📊 Battery Monitoring System Data (Set 2)

This repository contains real-time battery performance data, visualized using **ThingSpeak**. Below are the observations and key insights from the recorded data.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Integration_of_SOC_and_SOH_Estimation_for_Li_ion_Battery_Management/blob/6c996bfd7e319a762cda0fc1d7e9c2d328040b2e/Photos/Result2.png" width="500">
</p>

<p align="center"><b>Figure 6:</b> Stability and Tracking Performance</p>  

## 🔋 Battery Status Charts

### 1️⃣ Battery State of Health (SOH)
- The **Battery SOH** remains stable at **60%** over the observed period.
- No significant fluctuations detected, indicating consistent battery health.

### 2️⃣ Battery Depth of Discharge (DOD)
- The **DOD** remains at **0%**, suggesting no significant discharge events.
- The battery is maintaining charge effectively.

## 🔢 Real-Time Data Readings
- **Battery Voltage**: **6.53V** (Latest Reading)
- **Battery Current**: **2.19mA** (Latest Reading)

## 📌 Key Takeaways
✅ The battery **health (SOH)** remains steady at **60%**.  
✅ **DOD remains at 0%**, indicating no significant discharge.  
✅ The voltage is at **6.53V**, which is a healthy level.  
✅ The current is at **2.19mA**, aligning with expected behavior.  

---

# 📊 Battery Monitoring System Data (Set 3)

This dataset represents real-time battery performance parameters, visualized using ThingSpeak. Below are the observations and key insights from the recorded data.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Integration_of_SOC_and_SOH_Estimation_for_Li_ion_Battery_Management/blob/6c996bfd7e319a762cda0fc1d7e9c2d328040b2e/Photos/Result3.png" width="500">
</p>

<p align="center"><b>Figure 7:</b> Frequency Response and Performance Validation</p>  

## 🔋 Battery Status Charts

### 1️⃣ Battery Temperature (Batt_Temp)
- **Current Temperature:** 30.50°C  
- The temperature is within a normal operational range.

### 2️⃣ Battery State of Charge (Batt_SOC)
- The battery SOC is near **100%**, indicating a fully charged state.  
- No significant discharge events are detected.

### 3️⃣ Battery State of Health (Batt_SOH)
- The SOH remains stable at **60%**.  
- The battery is in a moderately healthy condition.

### 4️⃣ Battery Depth of Discharge (Batt_DOD)
- The DOD is currently **40%**, indicating moderate battery usage.  
- No extreme discharging trends are observed.

## 📌 Key Takeaways  
✅ The battery temperature is stable at **30.50°C**, which is within the normal range.  
✅ SOC is near **100%**, indicating a fully charged battery.  
✅ The SOH remains at **60%**, meaning the battery is still in good condition.  
✅ The DOD is at **40%**, suggesting moderate usage without deep discharge.  

---

# **Conclusion**
The results validate the effectiveness of the implemented control strategy. **[Summarize improvements, performance benchmarks, or any necessary optimizations]**. Future work may focus on **[possible refinements, optimizations, or next steps]**.  

---  

# **Applications**  
This project has applications in:

- **Electric Vehicles (EVs)** 🚗
- **Renewable Energy Storage** ☀️⚡
- **Uninterruptible Power Supplies (UPS)** 🔋
- **Smart Grids** 🏩
- **Portable Electronics** 📱

---

# **Final Thoughts**
Integrating SOC and SOH estimation into a battery management system significantly enhances performance, efficiency, and safety. This work provides a foundation for real-time battery monitoring and predictive maintenance, which is critical for sustainable energy solutions.  

---

# **Scope of Future Work**
- Implementing **Machine Learning (ML) models** for more accurate SOC and SOH prediction.
- Developing a **real-time monitoring dashboard** for battery status visualization.
- Extending the methodology to **multi-cell battery packs** for EV applications.
- Investigating alternative **non-invasive battery health estimation techniques**.

---

# **References**
- Research papers on SOC & SOH estimation methods
- Manufacturer datasheets for battery specifications
- IEEE standards for battery management systems

---

# **Contributing**
Contributions are welcome! Feel free to open an **issue** or submit a **pull request**.

---

# **License**
This project is licensed under the [MIT License](LICENSE).
---

📌 **Author**: [Vande]  
📌 **License**: GPL-3.0 lisence  
📌 **Contributions**: Open to suggestions and improvements! Feel free to submit PRs or open issues. 🚀
