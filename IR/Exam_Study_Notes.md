# Comprehensive Exam Study Notes - Enhanced

## 1. Sensors & Electronics

### Learning Objectives
- Understand the functionality, principles, and practical applications of common sensors in embedded systems
- Differentiate between digital and analog signal processing and their respective applications
- Apply fundamental electronics principles in circuit design, including proper GPIO usage and component selection
- Implement sensor fusion techniques for improved accuracy and reliability

### Key Concepts

#### Ultrasonic Sensors (HC-SR04)
Ultrasonic sensors operate on the principle of echolocation, similar to how bats navigate. They emit high-frequency sound waves (typically 40kHz) and measure the time taken for the echo to return.

**Operating Principle:**
- The sensor emits a short ultrasonic pulse (8 cycles at 40kHz)
- Sound waves travel through air at approximately 343 m/s (0.034 cm/μs at room temperature)
- When waves encounter an object, they reflect back to the sensor
- The microcontroller measures the time duration between transmission and reception

**Distance Calculation Formula:**
$$\text{Distance (cm)} = \frac{\text{Duration (μs)} \times \text{Speed of Sound (cm/μs)}}{2}$$

Where:
- Speed of Sound ≈ 0.034 cm/μs (at 20°C)
- Division by 2 accounts for round-trip travel

**Practical Considerations:**
- Effective range: 2cm to 400cm
- Accuracy: ±3mm
- Beam angle: ~15 degrees
- Temperature affects speed of sound: $v = 331.3 + 0.606T$ (where T is temperature in °C)

**Applications:**
- Obstacle avoidance in autonomous vehicles
- Level sensing in tanks and containers
- Proximity detection in security systems
- Parking assistance systems

**Arduino Implementation:**
```cpp
#define TRIG_PIN 9
#define ECHO_PIN 10

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  Serial.begin(9600);
}

void loop() {
  // Send trigger pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  
  // Measure echo duration
  long duration = pulseIn(ECHO_PIN, HIGH);
  
  // Calculate distance
  float distance = (duration * 0.034) / 2;
  
  // Display results
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  delay(500);
}
```

#### PIR (Passive Infrared) Sensors
PIR sensors detect motion by monitoring changes in infrared radiation emitted by warm objects (particularly humans and animals).

**Operating Principle:**
- Contains pyroelectric sensor that generates electrical charge when exposed to infrared radiation
- Fresnel lens focuses IR radiation onto the sensor
- Motion triggers differential changes in IR levels across sensor segments
- Built-in comparator converts analog signal to digital output

**Technical Specifications:**
- Detection range: 3-7 meters (depending on model)
- Detection angle: 100-120 degrees
- Delay time: Adjustable (0.3s to 18s)
- Sensitivity: Adjustable via potentiometer

**Output Characteristics:**
- Digital HIGH (3.3V or 5V): Motion detected
- Digital LOW (0V): No motion detected
- Retriggering: Can be configured for single or multiple triggers

**Applications:**
- Security and alarm systems
- Automatic lighting control
- Energy-saving applications
- Occupancy detection in smart buildings

**Arduino Implementation:**
```cpp
#define PIR_PIN 7
#define LED_PIN 13

void setup() {
  pinMode(PIR_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
  
  // Allow sensor to stabilize
  delay(20000);
  Serial.println("PIR sensor ready");
}

void loop() {
  int pirState = digitalRead(PIR_PIN);
  
  if (pirState == HIGH) {
    digitalWrite(LED_PIN, HIGH);
    Serial.println("Motion detected!");
  } else {
    digitalWrite(LED_PIN, LOW);
    Serial.println("No motion detected");
  }
  
  delay(1000);
}
```

#### IR (Infrared) Sensors
Infrared sensors use infrared light to detect objects, measure distances, or follow lines based on reflection characteristics.

**Types of IR Sensors:**
1. **Reflective IR Sensors:** Measure reflected IR light intensity
2. **Break-beam IR Sensors:** Detect interruption of IR beam
3. **Thermal IR Sensors:** Detect heat signatures

**Operating Principle:**
- IR LED emits infrared light (typically 940nm wavelength)
- Photodiode or phototransistor receives reflected/transmitted light
- Output varies based on object proximity, color, and surface properties

**Applications:**
- Line-following robots (detects contrast between line and surface)
- Proximity sensing and object detection
- Encoder systems for motor control
- Remote control receivers

**Limitations:**
- Sensitive to ambient light conditions
- Performance varies with object color and surface texture
- Requires calibration for consistent operation

#### Additional Sensors

**LDR (Light Dependent Resistor):**
- **Function:** Resistance decreases with increasing light intensity
- **Resistance Range:** 1MΩ (darkness) to 10kΩ (bright light)
- **Formula:** $R = R_0 \times \left(\frac{L_0}{L}\right)^{\gamma}$ where γ is the photoconductivity constant
- **Applications:** Automatic street lighting, camera exposure control

**DHT11/DHT22 Temperature and Humidity Sensors:**
- **DHT11:** ±2°C temperature, ±5% humidity accuracy
- **DHT22:** ±0.5°C temperature, ±2% humidity accuracy
- **Communication:** Single-wire digital protocol
- **Applications:** Weather monitoring, greenhouse control

**LM35 Temperature Sensor:**
- **Linear Output:** 10mV/°C
- **Formula:** $T(°C) = \frac{V_{out} \times 1000}{10}$ where $V_{out}$ is in volts
- **Range:** -55°C to +150°C
- **Applications:** Temperature monitoring, thermal protection

**MPU6050 (6-DOF IMU):**
- **Components:** 3-axis accelerometer + 3-axis gyroscope
- **Communication:** I2C protocol
- **Applications:** Orientation sensing, motion tracking, robotics

**Pulse Oximeter:**
- **Function:** Measures heart rate and blood oxygen saturation
- **Principle:** Light absorption differences between oxygenated and deoxygenated blood
- **Applications:** Health monitoring, fitness tracking

**IMU (Inertial Measurement Unit):**
- **Components:** Accelerometer, gyroscope, magnetometer
- **Applications:** Fall detection, navigation, stabilization systems

#### Sensor Fusion Techniques
Sensor fusion combines data from multiple sensors to overcome individual sensor limitations and improve overall system performance.

**Why Sensor Fusion?**
- Reduces noise and drift
- Increases accuracy and reliability
- Compensates for sensor failures
- Provides redundancy

**Common Fusion Algorithms:**

**1. Complementary Filter:**
Simple and computationally efficient for combining accelerometer and gyroscope data.

$$\theta_{fused} = \alpha \times (\theta_{previous} + \omega_{gyro} \times \Delta t) + (1-\alpha) \times \theta_{accel}$$

Where:
- α is the filter coefficient (typically 0.98)
- ω is the angular velocity from gyroscope
- Δt is the time step

**2. Kalman Filter:**
Optimal estimator for linear systems with Gaussian noise.

**Prediction Step:**
$$\hat{x}_{k|k-1} = F_k \hat{x}_{k-1|k-1} + B_k u_k$$
$$P_{k|k-1} = F_k P_{k-1|k-1} F_k^T + Q_k$$

**Update Step:**
$$K_k = P_{k|k-1} H_k^T (H_k P_{k|k-1} H_k^T + R_k)^{-1}$$
$$\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k (z_k - H_k \hat{x}_{k|k-1})$$
$$P_{k|k} = (I - K_k H_k) P_{k|k-1}$$

Where:
- $\hat{x}$ is the state estimate
- $P$ is the error covariance
- $K$ is the Kalman gain
- $F$ is the state transition model
- $H$ is the observation model
- $Q$ is process noise covariance
- $R$ is measurement noise covariance

**Arduino Sensor Fusion Example:**
```cpp
#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;
float fusedAngle = 0;
unsigned long lastTime = 0;

void setup() {
  Serial.begin(9600);
  Wire.begin();
  mpu.initialize();
}

void loop() {
  unsigned long currentTime = millis();
  float dt = (currentTime - lastTime) / 1000.0;
  
  // Read sensor data
  int16_t ax, ay, az, gx, gy, gz;
  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
  
  // Calculate angles
  float accelAngle = atan2(ay, az) * 180/PI;
  float gyroRate = gx / 131.0; // Convert to degrees/second
  
  // Complementary filter
  fusedAngle = 0.98 * (fusedAngle + gyroRate * dt) + 0.02 * accelAngle;
  
  Serial.print("Fused Angle: ");
  Serial.println(fusedAngle);
  
  lastTime = currentTime;
  delay(10);
}
```

#### Digital vs Analog Signal Processing

**Digital Pins:**
- **Voltage Levels:** HIGH (5V/3.3V) or LOW (0V)
- **Functions:** `digitalRead()`, `digitalWrite()`
- **Applications:** LEDs, switches, PIR sensors, relays
- **Advantages:** Noise immunity, simple processing
- **Disadvantages:** Limited information content

**Analog Pins:**
- **Voltage Range:** Continuous values (0-5V on Arduino UNO)
- **ADC Resolution:** 10-bit (0-1023) on Arduino UNO
- **Formula:** $V_{actual} = \frac{ADC_{reading}}{1023} \times V_{ref}$
- **Functions:** `analogRead()`, `analogWrite()` (PWM)
- **Applications:** Temperature sensors, light sensors, potentiometers
- **Advantages:** Rich information content, precise measurements
- **Disadvantages:** Susceptible to noise, requires calibration

**PWM (Pulse Width Modulation):**
- **Principle:** Varies duty cycle to control average voltage
- **Formula:** $V_{average} = V_{supply} \times \frac{t_{on}}{T}$
- **Applications:** Motor speed control, LED brightness, servo control

#### GPIO (General Purpose Input/Output) Pins
GPIO pins provide flexible digital interfaces for microcontrollers to interact with external components.

**Pin Configuration:**
- **Input:** High impedance, reads external signals
- **Output:** Can source or sink current
- **Pull-up/Pull-down:** Internal resistors for stable readings

**Arduino GPIO Example:**
```cpp
#define LED_PIN 13
#define BUTTON_PIN 2

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP); // Internal pull-up resistor
  Serial.begin(9600);
}

void loop() {
  int buttonState = digitalRead(BUTTON_PIN);
  
  if (buttonState == LOW) { // Button pressed (pull-up inverts logic)
    digitalWrite(LED_PIN, HIGH);
    Serial.println("Button pressed - LED ON");
  } else {
    digitalWrite(LED_PIN, LOW);
    Serial.println("Button released - LED OFF");
  }
  
  delay(100);
}
```

**Raspberry Pi GPIO Example:**
```python
import RPi.GPIO as GPIO
import time

LED_PIN = 18
BUTTON_PIN = 16

# Setup
GPIO.setmode(GPIO.BCM)
GPIO.setup(LED_PIN, GPIO.OUT)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)

try:
    while True:
        button_state = GPIO.input(BUTTON_PIN)
        
        if button_state == GPIO.LOW:  # Button pressed
            GPIO.output(LED_PIN, GPIO.HIGH)
            print("Button pressed - LED ON")
        else:
            GPIO.output(LED_PIN, GPIO.LOW)
            print("Button released - LED OFF")
        
        time.sleep(0.1)
        
except KeyboardInterrupt:
    print("Program interrupted")
    
finally:
    GPIO.cleanup()  # Reset all GPIO pins
```

#### Fundamental Electronics Principles

**Ohm's Law:**
$$V = I \times R$$
$$P = V \times I = I^2 \times R = \frac{V^2}{R}$$

**Kirchhoff's Laws:**
1. **Current Law (KCL):** $\sum I_{in} = \sum I_{out}$
2. **Voltage Law (KVL):** $\sum V_{loop} = 0$

**Resistors:**
- **Series:** $R_{total} = R_1 + R_2 + R_3 + ...$
- **Parallel:** $\frac{1}{R_{total}} = \frac{1}{R_1} + \frac{1}{R_2} + \frac{1}{R_3} + ...$
- **LED Current Limiting:** $R = \frac{V_{supply} - V_{LED}}{I_{LED}}$
- **Pull-up/Pull-down:** Typically 10kΩ for stable digital readings

**Capacitors:**
- **Capacitance:** $C = \frac{Q}{V}$
- **Energy Storage:** $E = \frac{1}{2}CV^2$
- **Time Constant:** $\tau = RC$
- **Applications:** Voltage smoothing, noise filtering, timing circuits

**Diodes:**
- **Forward Voltage:** ~0.7V for silicon diodes
- **Flyback Diode:** Protects against inductive kickback from motors/relays
- **Zener Diode:** Voltage regulation

**Transistors:**
- **NPN/PNP:** Switching and amplification
- **Base Current:** Controls collector current
- **Saturation:** Fully ON state for switching applications
- **Motor Control:** Use with flyback diode for protection

#### Signal Flow Architecture
The typical signal flow in embedded systems follows a sensor-to-actuator pathway through microcontroller processing.

**Signal Path:**
1. **Sensor → ADC → Microcontroller → Processing → Actuator**
2. **Noise Filtering → Signal Conditioning → Digital Processing → Output Generation**

**Example Implementation:**
```cpp
// Complete signal flow example
#define TEMP_SENSOR A0
#define FAN_PIN 9
#define LED_PIN 13

void setup() {
  pinMode(FAN_PIN, OUTPUT);
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // Read analog sensor
  int sensorValue = analogRead(TEMP_SENSOR);
  
  // Convert to temperature (LM35: 10mV/°C)
  float voltage = sensorValue * (5.0 / 1023.0);
  float temperature = voltage * 100.0;
  
  // Processing logic
  if (temperature > 30.0) {
    digitalWrite(LED_PIN, HIGH);        // Warning LED
    analogWrite(FAN_PIN, 255);          // Full speed fan
    Serial.println("High temperature detected!");
  } else if (temperature > 25.0) {
    digitalWrite(LED_PIN, LOW);
    analogWrite(FAN_PIN, 128);          // Half speed fan
  } else {
    digitalWrite(LED_PIN, LOW);
    analogWrite(FAN_PIN, 0);            // Fan off
  }
  
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println("°C");
  
  delay(1000);
}
```

### Summary Table - Sensors & Electronics
| Component | Type | Function | Key Formula | Applications |
|-----------|------|----------|-------------|-------------|
| Ultrasonic | Sensor | Distance measurement | $d = \frac{t \times v}{2}$ | Obstacle avoidance, level sensing |
| PIR | Sensor | Motion detection | Digital HIGH/LOW | Security, automatic lighting |
| LDR | Sensor | Light intensity | $R = R_0(\frac{L_0}{L})^{\gamma}$ | Auto lighting, camera control |
| GPIO | Interface | Digital I/O | 5V/0V logic levels | LED control, switch reading |
| Capacitor | Passive | Energy storage | $E = \frac{1}{2}CV^2$ | Voltage smoothing, timing |
| Transistor | Active | Switching/amplifying | $I_C = \beta \times I_B$ | Motor control, signal amplification |

## 2. Programming Logic

### Learning Objectives
- Master Python and Arduino programming fundamentals with advanced concepts
- Understand control structures, data types, and boolean logic operations
- Write, debug, and optimize programs for embedded systems and robotics
- Implement error handling and robust programming practices

### Key Concepts

#### Python Programming Fundamentals

**Print Statements and Debugging:**
Python's print function is essential for debugging and output formatting.

```python
# Basic printing
print("Hello, World!")

# Variable printing with formatting
x = 42
y = 3.14159
print(f"x = {x}, y = {y:.2f}")

# Debug printing
debug_mode = True
if debug_mode:
    print(f"Debug: x = {x}, type = {type(x)}")

# Boolean evaluation
print(3 == 3.0)    # True (value comparison)
print(3 is 3.0)    # False (identity comparison)
```

**Advanced Data Types:**
```python
# Lists and list comprehensions
numbers = [1, 2, 3, 4, 5]
squares = [x**2 for x in numbers if x % 2 == 0]
print(squares)  # [4, 16]

# Dictionaries
sensor_data = {
    'temperature': 25.5,
    'humidity': 60.2,
    'pressure': 1013.25
}

# Tuples and unpacking
coordinates = (10, 20)
x, y = coordinates
```

**Control Structures:**

**Conditional Statements:**
```python
temperature = 25.5
humidity = 60.0

# Basic if-else
if temperature > 30:
    print("Hot weather")
elif temperature > 20:
    print("Moderate weather")
else:
    print("Cold weather")

# Ternary operator
status = "Hot" if temperature > 30 else "Normal"

# Complex conditions
if temperature > 25 and humidity > 70:
    print("Hot and humid")
elif temperature < 10 or humidity > 90:
    print("Extreme conditions")
```

**Loop Structures:**
```python
# For loops with range
for i in range(5):          # 0, 1, 2, 3, 4
    print(f"Iteration {i}")

for i in range(2, 10, 2):   # 2, 4, 6, 8
    print(f"Even number: {i}")

# For loops with collections
sensors = ['temp', 'humidity', 'pressure']
for sensor in sensors:
    print(f"Reading {sensor} sensor")

# Enumerate for index access
for index, sensor in enumerate(sensors):
    print(f"Sensor {index}: {sensor}")

# While loops
count = 0
while count < 5:
    print(f"Count: {count}")
    count += 1

# Infinite loop with break
while True:
    user_input = input("Enter 'quit' to exit: ")
    if user_input.lower() == 'quit':
        break
    print(f"You entered: {user_input}")
```

**Advanced Function Concepts:**
```python
# Function with different parameter types
def advanced_function(a, b, /, c, d=10, *, e, f=20):
    """
    a, b: positional-only parameters
    c: can be positional or keyword
    d: keyword parameter with default
    e: keyword-only parameter (required)
    f: keyword-only parameter with default
    """
    return (a + b) * c + d + e + f

# Valid function calls
result1 = advanced_function(1, 2, 3, e=5)           # Uses defaults for d, f
result2 = advanced_function(1, 2, c=3, d=15, e=5, f=25)

# Lambda functions
square = lambda x: x**2
numbers = [1, 2, 3, 4, 5]
squared = list(map(square, numbers))

# Function as parameter
def apply_operation(func, data):
    return [func(x) for x in data]

result = apply_operation(lambda x: x * 2, [1, 2, 3, 4])
```

**Avoiding Mutable Default Arguments:**
```python
# Problematic approach
def bad_function(x, y=[]):  # Don't do this!
    y.append(x)
    return y

# Safe approach
def good_function(x, y=None):
    if y is None:
        y = []
    y.append(x)
    return y

# Even better approach
def better_function(x, y=None):
    y = y or []
    return y + [x]  # Returns new list
```

**Error Handling:**
```python
# Basic exception handling
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
except ValueError as e:
    print(f"Value error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
finally:
    print("This always executes")

# Specific sensor error handling
def read_sensor():
    try:
        # Simulate sensor reading
        import random
        if random.random() < 0.1:  # 10% chance of error
            raise ConnectionError("Sensor disconnected")
        return random.uniform(20, 30)
    except ConnectionError:
        print("Sensor error - using default value")
        return 25.0  # Default temperature
```

#### Arduino Programming Structure

**Basic Sketch Structure:**
```cpp
// Global declarations
#include <Wire.h>
#include <LiquidCrystal.h>

// Pin definitions
#define LED_PIN 13
#define SENSOR_PIN A0
#define BUTTON_PIN 2

// Global variables
int sensorValue = 0;
bool ledState = false;
unsigned long lastTime = 0;

// Setup function (runs once)
void setup() {
  // Initialize serial communication
  Serial.begin(9600);
  
  // Configure GPIO pins
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  
  // Initialize peripherals
  Wire.begin();
  
  Serial.println("Arduino initialized");
}

// Main loop (runs continuously)
void loop() {
  // Read sensors
  sensorValue = analogRead(SENSOR_PIN);
  
  // Process data
  float voltage = sensorValue * (5.0 / 1023.0);
  
  // Control outputs
  if (voltage > 2.5) {
    digitalWrite(LED_PIN, HIGH);
    ledState = true;
  } else {
    digitalWrite(LED_PIN, LOW);
    ledState = false;
  }
  
  // Serial output
  Serial.print("Sensor: ");
  Serial.print(sensorValue);
  Serial.print(", Voltage: ");
  Serial.println(voltage);
  
  delay(100);
}
```

**Advanced Arduino Functions:**
```cpp
// Interrupt service routine
volatile bool buttonPressed = false;

void buttonISR() {
  buttonPressed = true;
}

// Timer-based operations
unsigned long previousMillis = 0;
const long interval = 1000;

void setup() {
  attachInterrupt(digitalPinToInterrupt(2), buttonISR, FALLING);
}

void loop() {
  unsigned long currentMillis = millis();
  
  // Non-blocking delay
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    
    // Execute timed task
    Serial.println("Timer task executed");
  }
  
  // Handle interrupt
  if (buttonPressed) {
    Serial.println("Button was pressed!");
    buttonPressed = false;
  }
}
```

**Arduino Control Structures:**
```cpp
// Switch-case statement
void processCommand(char command) {
  switch (command) {
    case 'A':
      Serial.println("Action A");
      digitalWrite(LED_PIN, HIGH);
      break;
    case 'B':
      Serial.println("Action B");
      digitalWrite(LED_PIN, LOW);
      break;
    case 'C':
      Serial.println("Action C");
      // Toggle LED
      digitalWrite(LED_PIN, !digitalRead(LED_PIN));
      break;
    default:
      Serial.println("Unknown command");
      break;
  }
}

// Complex conditional logic
void obstacleAvoidance() {
  int frontDistance = measureDistance(FRONT_SENSOR);
  int leftDistance = measureDistance(LEFT_SENSOR);
  int rightDistance = measureDistance(RIGHT_SENSOR);
  
  if (frontDistance < 20) {
    if (leftDistance > rightDistance && leftDistance > 30) {
      turnLeft();
      Serial.println("Turning left");
    } else if (rightDistance > 30) {
      turnRight();
      Serial.println("Turning right");
    } else {
      moveBackward();
      Serial.println("Moving backward");
    }
  } else {
    moveForward();
    Serial.println("Moving forward");
  }
}
```

#### Boolean Logic and Operations

**Boolean Operators:**
- **AND (`&&` in C++, `and` in Python):** Returns true only if both operands are true
- **OR (`||` in C++, `or` in Python):** Returns true if at least one operand is true
- **NOT (`!` in C++, `not` in Python):** Inverts the boolean value
- **XOR (`^` in C++):** Returns true if operands are different

**Truth Tables:**

| A | B | A AND B | A OR B | NOT A | A XOR B |
|---|---|---------|--------|-------|---------|
| T | T |    T    |   T    |   F   |    F    |
| T | F |    F    |   T    |   F   |    T    |
| F | T |    F    |   T    |   T   |    T    |
| F | F |    F    |   F    |   T   |    F    |

**Practical Applications:**
```python
# Sensor fusion with boolean logic
def safety_check(temperature, pressure, humidity):
    temp_ok = 15 <= temperature <= 35
    pressure_ok = 950 <= pressure <= 1050
    humidity_ok = humidity <= 80
    
    # All conditions must be true
    system_safe = temp_ok and pressure_ok and humidity_ok
    
    # Any critical condition triggers alert
    critical_alert = temperature > 40 or pressure > 1100 or humidity > 95
    
    return system_safe and not critical_alert

# Robot navigation logic
def navigation_decision(front_clear, left_clear, right_clear):
    if front_clear and not (left_clear or right_clear):
        return "move_forward"
    elif not front_clear and left_clear:
        return "turn_left"
    elif not front_clear and right_clear:
        return "turn_right"
    elif not front_clear and not left_clear and not right_clear:
        return "reverse"
    else:
        return "explore"
```

#### Robot Operating System (ROS)

**ROS Architecture:**
ROS (Robot Operating System) is a flexible framework for writing robot software, providing tools and libraries for distributed computing in robotics.

**Key Components:**
1. **Nodes:** Independent processes that perform specific tasks
2. **Topics:** Named channels for asynchronous message passing
3. **Services:** Synchronous request-response communication
4. **Messages:** Data structures for communication
5. **Master:** Central registry for node discovery

**ROS Communication Patterns:**

**Publisher-Subscriber Pattern:**
```python
#!/usr/bin/env python3
import rospy
from std_msgs.msg import Float32, String
from sensor_msgs.msg import Temperature

class SensorPublisher:
    def __init__(self):
        # Initialize ROS node
        rospy.init_node('sensor_publisher', anonymous=True)
        
        # Create publishers
        self.temp_pub = rospy.Publisher('temperature', Float32, queue_size=10)
        self.status_pub = rospy.Publisher('sensor_status', String, queue_size=10)
        
        # Set publishing rate
        self.rate = rospy.Rate(10)  # 10 Hz
        
    def publish_sensor_data(self):
        while not rospy.is_shutdown():
            # Simulate sensor reading
            temperature = self.read_temperature_sensor()
            status = "OK" if 15 <= temperature <= 35 else "WARNING"
            
            # Publish messages
            self.temp_pub.publish(temperature)
            self.status_pub.publish(status)
            
            rospy.loginfo(f"Published temp: {temperature:.2f}°C, Status: {status}")
            
            self.rate.sleep()
    
    def read_temperature_sensor(self):
        # Simulate sensor reading
        import random
        return random.uniform(20, 30)

if __name__ == '__main__':
    try:
        publisher = SensorPublisher()
        publisher.publish_sensor_data()
    except rospy.ROSInterruptException:
        pass
```

**Subscriber Implementation:**
```python
#!/usr/bin/env python3
import rospy
from std_msgs.msg import Float32
from geometry_msgs.msg import Twist

class MotorController:
    def __init__(self):
        rospy.init_node('motor_controller', anonymous=True)
        
        # Subscribe to temperature topic
        rospy.Subscriber('temperature', Float32, self.temperature_callback)
        
        # Publisher for motor commands
        self.cmd_pub = rospy.Publisher('cmd_vel', Twist, queue_size=10)
        
        self.current_temp = 25.0
        
    def temperature_callback(self, msg):
        self.current_temp = msg.data
        rospy.loginfo(f"Received temperature: {self.current_temp:.2f}°C")
        
        # Control logic based on temperature
        if self.current_temp > 30:
            self.stop_motors()
        elif self.current_temp < 20:
            self.reduce_speed()
        else:
            self.normal_operation()
    
    def stop_motors(self):
        cmd = Twist()
        cmd.linear.x = 0.0
        cmd.angular.z = 0.0
        self.cmd_pub.publish(cmd)
        rospy.logwarn("Motors stopped due to high temperature")
    
    def reduce_speed(self):
        cmd = Twist()
        cmd.linear.x = 0.3  # Reduced speed
        cmd.angular.z = 0.0
        self.cmd_pub.publish(cmd)
        rospy.loginfo("Reduced speed due to low temperature")
    
    def normal_operation(self):
        cmd = Twist()
        cmd.linear.x = 0.5  # Normal speed
        cmd.angular.z = 0.0
        self.cmd_pub.publish(cmd)

if __name__ == '__main__':
    try:
        controller = MotorController()
        rospy.spin()  # Keep the node running
    except rospy.ROSInterruptException:
        pass
```

**Service Implementation:**
```python
#!/usr/bin/env python3
import rospy
from std_srvs.srv import SetBool, SetBoolResponse

class SystemController:
    def __init__(self):
        rospy.init_node('system_controller')
        
        # Create service
        self.service = rospy.Service('emergency_stop', SetBool, self.emergency_stop_callback)
        
        self.system_active = True
        rospy.loginfo("System controller ready")
    
    def emergency_stop_callback(self, req):
        if req.data:  # Emergency stop requested
            self.system_active = False
            rospy.logwarn("EMERGENCY STOP ACTIVATED")
            return SetBoolResponse(True, "Emergency stop activated")
        else:  # Resume operation
            self.system_active = True
            rospy.loginfo("System resumed")
            return SetBoolResponse(True, "System resumed")

if __name__ == '__main__':
    try:
        controller = SystemController()
        rospy.spin()
    except rospy.ROSInterruptException:
        pass
```

**ROS Launch File Example:**
```xml
<launch>
    <!-- Launch sensor publisher -->
    <node name="sensor_publisher" pkg="my_robot" type="sensor_publisher.py" output="screen"/>
    
    <!-- Launch motor controller -->
    <node name="motor_controller" pkg="my_robot" type="motor_controller.py" output="screen"/>
    
    <!-- Launch system controller -->
    <node name="system_controller" pkg="my_robot" type="system_controller.py" output="screen"/>
    
    <!-- Set parameters -->
    <param name="max_temperature" value="35.0"/>
    <param name="min_temperature" value="15.0"/>
</launch>
```

### Summary Table - Programming Logic
| Concept | Language | Description | Example |
|---------|----------|-------------|---------|
| Print/Debug | Python | Output and debugging | `print(f"Value: {x}")` |
| Control Flow | Both | Conditional execution | `if condition: action` |
| Loops | Both | Repeated execution | `for i in range(10):` |
| Functions | Python | Modular programming | `def func(a, b, /, *, c):` |
| ROS Nodes | Python/C++ | Distributed computing | Publisher/Subscriber pattern |
| Boolean Logic | Both | Logical operations | `and`, `or`, `not` operators |

## 3. Machine Learning Basics

### Learning Objectives
- Understand classification algorithms and their applications in robotics
- Master dataset handling, preprocessing, and train-test-validation splits
- Differentiate between model training and inference phases
- Calculate and interpret evaluation metrics with proper mathematical formulations
- Implement data preprocessing and model evaluation techniques

### Key Concepts

#### Classification and Machine Learning Fundamentals

**Classification Overview:**
Classification is a supervised learning task where the goal is to predict discrete categories or classes based on input features.

**Types of Classification:**
1. **Binary Classification:** Two classes (e.g., spam vs. not spam)
2. **Multi-class Classification:** Multiple classes (e.g., image recognition)
3. **Multi-label Classification:** Multiple labels per instance

**Common Classification Algorithms:**

**1. K-Nearest Neighbors (KNN):**
- **Principle:** Classify based on majority class of k nearest neighbors
- **Distance Metric:** Euclidean distance: $d = \sqrt{\sum_{i=1}^{n}(x_i - y_i)^2}$
- **Advantages:** Simple, no training required, works well with small datasets
- **Disadvantages:** Computationally expensive for large datasets, sensitive to irrelevant features

**2. Convolutional Neural Networks (CNN):**
- **Architecture:** Convolution layers → Pooling layers → Fully connected layers
- **Applications:** Image classification, object detection, computer vision
- **Key Operations:**
  - **Convolution:** $(f * g)(t) = \sum_{m} f(m) \cdot g(t-m)$
  - **Pooling:** Reduces spatial dimensions (max pooling, average pooling)

**3. Support Vector Machines (SVM):**
- **Principle:** Find optimal hyperplane that separates classes
- **Margin:** Distance between hyperplane and nearest data points
- **Kernel Functions:** RBF, polynomial, linear

#### Dataset Management and Preprocessing

**Dataset Splitting:**
Proper dataset splitting is crucial for unbiased model evaluation.

```python
from sklearn.model_selection import train_test_split
import pandas as pd
import numpy as np

# Load and prepare data
data = pd.read_csv('sensor_data.csv')
X = data[['temperature', 'humidity', 'pressure']]
y = data['classification']

# Split into train, validation, and test sets
X_temp, X_test, y_temp, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

X_train, X_val, y_train, y_val = train_test_split(
    X_temp, y_temp, test_size=0.25, random_state=42, stratify=y_temp
)

print(f"Training set: {len(X_train)} samples")
print(f"Validation set: {len(X_val)} samples") 
print(f"Test set: {len(X_test)} samples")
```

**Data Preprocessing Techniques:**

**1. Normalization/Standardization:**
```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Min-Max Normalization (0-1 scaling)
scaler_minmax = MinMaxScaler()
X_normalized = scaler_minmax.fit_transform(X_train)

# Formula: x' = (x - x_min) / (x_max - x_min)

# Z-score Standardization
scaler_standard = StandardScaler()
X_standardized = scaler_standard.fit_transform(X_train)

# Formula: x' = (x - μ) / σ
```

**2. Handling Missing Data:**
```python
from sklearn.impute import SimpleImputer

# Handle missing values
imputer = SimpleImputer(strategy='median')
X_imputed = imputer.fit_transform(X_train)

# Alternative strategies: 'mean', 'most_frequent', 'constant'
```

**3. Feature Engineering:**
```python
# Create new features
data['temperature_squared'] = data['temperature'] ** 2
data['temp_humidity_ratio'] = data['temperature'] / data['humidity']

# Polynomial features
from sklearn.preprocessing import PolynomialFeatures
poly = PolynomialFeatures(degree=2, include_bias=False)
X_poly = poly.fit_transform(X_train)
```

**Advanced Data Handling Example:**
```python
import pandas as pd
from datetime import datetime, timedelta
import numpy as np

# Comprehensive data processing example
def process_sensor_data(df):
    # Handle datetime
    df['timestamp'] = pd.to_datetime(df['timestamp'])
    df['hour'] = df['timestamp'].dt.hour
    df['day_of_week'] = df['timestamp'].dt.dayofweek
    
    # Calculate derived features
    current_year = datetime.now().year
    df['sensor_age'] = current_year - df['installation_year']
    
    # Handle categorical variables
    df_encoded = pd.get_dummies(df, columns=['sensor_type'], prefix='type')
    
    # Calculate rolling statistics
    df['temp_rolling_mean'] = df['temperature'].rolling(window=5).mean()
    df['temp_rolling_std'] = df['temperature'].rolling(window=5).std()
    
    # Remove outliers using IQR method
    Q1 = df['temperature'].quantile(0.25)
    Q3 = df['temperature'].quantile(0.75)
    IQR = Q3 - Q1
    df_clean = df[~((df['temperature'] < (Q1 - 1.5 * IQR)) | 
                    (df['temperature'] > (Q3 + 1.5 * IQR)))]
    
    return df_clean

# Example usage
sensor_data = pd.DataFrame({
    'timestamp': pd.date_range('2023-01-01', periods=100, freq='H'),
    'temperature': np.random.normal(25, 5, 100),
    'humidity': np.random.normal(60, 10, 100),
    'installation_year': np.random.choice([2020, 2021, 2022], 100),
    'sensor_type': np.random.choice(['A', 'B', 'C'], 100)
})

processed_data = process_sensor_data(sensor_data)
```

#### Model Training vs Inference

**Training Phase:**
During training, the model learns patterns from labeled data by adjusting its parameters to minimize the loss function.

**Key Characteristics:**
- Uses labeled training data
- Computationally intensive
- Requires multiple epochs/iterations
- Updates model weights/parameters

**Inference Phase:**
During inference, the trained model makes predictions on new, unseen data.

**Key Characteristics:**
- Uses trained model parameters
- No weight updates
- Faster execution
- Real-time capability

**Training Example:**
```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
import time

# Training phase
start_time = time.time()

# Initialize model
model = RandomForestClassifier(n_estimators=100, random_state=42)

# Train model
model.fit(X_train, y_train)

training_time = time.time() - start_time
print(f"Training completed in {training_time:.2f} seconds")

# Validation during training
val_predictions = model.predict(X_val)
val_accuracy = accuracy_score(y_val, val_predictions)
print(f"Validation accuracy: {val_accuracy:.3f}")
```

**Inference Example:**
```python
# Inference phase
def predict_sensor_status(temperature, humidity, pressure):
    start_time = time.time()
    
    # Prepare input data
    input_data = np.array([[temperature, humidity, pressure]])
    
    # Make prediction
    prediction = model.predict(input_data)
    probability = model.predict_proba(input_data)
    
    inference_time = time.time() - start_time
    
    return {
        'prediction': prediction[0],
        'confidence': np.max(probability),
        'inference_time': inference_time
    }

# Real-time inference example
result = predict_sensor_status(25.5, 65.2, 1013.25)
print(f"Prediction: {result['prediction']}")
print(f"Confidence: {result['confidence']:.3f}")
print(f"Inference time: {result['inference_time']:.6f} seconds")
```

#### Loss Functions and Optimization

**Loss Functions for Classification:**

**1. Cross-Entropy Loss (Log Loss):**
For binary classification:
$L_{CE} = -\frac{1}{N} \sum_{i=1}^{N} [y_i \log(\hat{y}_i) + (1-y_i) \log(1-\hat{y}_i)]$

For multi-class classification:
$L_{CE} = -\frac{1}{N} \sum_{i=1}^{N} \sum_{j=1}^{C} y_{ij} \log(\hat{y}_{ij})$

Where:
- $N$ = number of samples
- $C$ = number of classes
- $y_{ij}$ = true label (1 if sample i belongs to class j, 0 otherwise)
- $\hat{y}_{ij}$ = predicted probability

**2. Mean Squared Error (for regression):**
$MSE = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2$

**3. Hinge Loss (for SVM):**
$L_{hinge} = \max(0, 1 - y_i \cdot \hat{y}_i)$

#### Comprehensive Evaluation Metrics

**Confusion Matrix:**
A confusion matrix provides detailed breakdown of correct and incorrect predictions.

```python
from sklearn.metrics import confusion_matrix, classification_report
import seaborn as sns
import matplotlib.pyplot as plt

# Generate confusion matrix
y_true = ['P', 'P', 'P', 'N', 'N', 'P', 'N', 'P', 'N', 'P']
y_pred = ['P', 'P', 'N', 'P', 'N', 'P', 'N', 'N', 'N', 'P']

cm = confusion_matrix(y_true, y_pred, labels=['P', 'N'])
print("Confusion Matrix:")
print(cm)

# Visualize confusion matrix
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
            xticklabels=['Predicted P', 'Predicted N'],
            yticklabels=['Actual P', 'Actual N'])
plt.title('Confusion Matrix')
plt.show()
```

**Detailed Metric Calculations:**

From the confusion matrix:
- True Positives (TP) = 5
- False Positives (FP) = 1  
- True Negatives (TN) = 2
- False Negatives (FN) = 2

**1. Accuracy:**
$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} = \frac{5 + 2}{5 + 2 + 1 + 2} = \frac{7}{10} = 0.70$

**2. Precision:**
$\text{Precision} = \frac{TP}{TP + FP} = \frac{5}{5 + 1} = \frac{5}{6} \approx 0.833$

**3. Recall (Sensitivity):**
$\text{Recall} = \frac{TP}{TP + FN} = \frac{5}{5 + 2} = \frac{5}{7} \approx 0.714$

**4. Specificity:**
$\text{Specificity} = \frac{TN}{TN + FP} = \frac{2}{2 + 1} = \frac{2}{3} \approx 0.667$

**5. F1 Score:**
$F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} = 2 \times \frac{0.833 \times 0.714}{0.833 + 0.714} \approx 0.769$

**6. Matthews Correlation Coefficient (MCC):**
$MCC = \frac{TP \times TN - FP \times FN}{\sqrt{(TP + FP)(TP + FN)(TN + FP)(TN + FN)}}$

**Implementation Example:**
```python
from sklearn.metrics import (accuracy_score, precision_score, recall_score, 
                            f1_score, matthews_corrcoef, roc_auc_score)
import numpy as np

def comprehensive_evaluation(y_true, y_pred, y_proba=None):
    """
    Comprehensive model evaluation with all metrics
    """
    results = {}
    
    # Basic metrics
    results['accuracy'] = accuracy_score(y_true, y_pred)
    results['precision'] = precision_score(y_true, y_pred, pos_label='P')
    results['recall'] = recall_score(y_true, y_pred, pos_label='P')
    results['f1'] = f1_score(y_true, y_pred, pos_label='P')
    results['mcc'] = matthews_corrcoef(y_true, y_pred)
    
    # If probabilities are available
    if y_proba is not None:
        results['auc_roc'] = roc_auc_score(
            [1 if label == 'P' else 0 for label in y_true], y_proba
        )
    
    # Calculate confusion matrix components
    cm = confusion_matrix(y_true, y_pred, labels=['P', 'N'])
    TP, FN, FP, TN = cm[0,0], cm[0,1], cm[1,0], cm[1,1]
    
    results['specificity'] = TN / (TN + FP) if (TN + FP) > 0 else 0
    results['sensitivity'] = results['recall']  # Same as recall
    
    return results

# Example usage
y_true = ['P', 'P', 'P', 'N', 'N', 'P', 'N', 'P', 'N', 'P']
y_pred = ['P', 'P', 'N', 'P', 'N', 'P', 'N', 'N', 'N', 'P']
y_proba = [0.9, 0.8, 0.4, 0.7, 0.2, 0.85, 0.1, 0.3, 0.15, 0.95]

metrics = comprehensive_evaluation(y_true, y_pred, y_proba)

for metric, value in metrics.items():
    print(f"{metric.upper()}: {value:.3f}")
```

**ROC Curve and AUC:**
```python
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt

def plot_roc_curve(y_true, y_proba):
    # Convert labels to binary
    y_binary = [1 if label == 'P' else 0 for label in y_true]
    
    # Calculate ROC curve
    fpr, tpr, thresholds = roc_curve(y_binary, y_proba)
    roc_auc = auc(fpr, tpr)
    
    # Plot ROC curve
    plt.figure(figsize=(8, 6))
    plt.plot(fpr, tpr, color='darkorange', lw=2, 
             label=f'ROC curve (AUC = {roc_auc:.3f})')
    plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('Receiver Operating Characteristic (ROC) Curve')
    plt.legend(loc="lower right")
    plt.grid(True)
    plt.show()
    
    return roc_auc

# Example usage
auc_score = plot_roc_curve(y_true, y_proba)
```

#### Advanced Machine Learning Concepts

**Cross-Validation:**
```python
from sklearn.model_selection import cross_val_score, StratifiedKFold
from sklearn.ensemble import RandomForestClassifier

# K-fold cross-validation
model = RandomForestClassifier(n_estimators=100, random_state=42)
cv_scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-validation scores: {cv_scores}")
print(f"Mean CV accuracy: {cv_scores.mean():.3f} (+/- {cv_scores.std() * 2:.3f})")

# Stratified K-fold for imbalanced datasets
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
stratified_scores = cross_val_score(model, X, y, cv=skf, scoring='f1')
```

**Hyperparameter Tuning:**
```python
from sklearn.model_selection import GridSearchCV

# Define parameter grid
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [3, 5, 10, None],
    'min_samples_split': [2, 5, 10],
    'min_samples_leaf': [1, 2, 4]
}

# Grid search with cross-validation
grid_search = GridSearchCV(
    RandomForestClassifier(random_state=42),
    param_grid,
    cv=5,
    scoring='f1',
    n_jobs=-1
)

grid_search.fit(X_train, y_train)

print(f"Best parameters: {grid_search.best_params_}")
print(f"Best cross-validation score: {grid_search.best_score_:.3f}")
```

### Summary Table - Machine Learning Basics
| Concept | Description | Key Formula | Applications |
|---------|-------------|-------------|-------------|
| Classification | Predict categories | Various algorithms | Object detection, pattern recognition |
| Normalization | Scale features | $x' = \frac{x - x_{min}}{x_{max} - x_{min}}$ | Data preprocessing |
| Accuracy | Overall correctness | $\frac{TP + TN}{Total}$ | Model evaluation |
| Precision | Positive prediction accuracy | $\frac{TP}{TP + FP}$ | Quality of positive predictions |
| Recall | Positive detection rate | $\frac{TP}{TP + FN}$ | Completeness of positive detection |
| F1 Score | Harmonic mean of precision/recall | $2 \times \frac{P \times R}{P + R}$ | Balanced evaluation metric |

## 4. IoT & Data Flow

### Learning Objectives
- Understand MQTT protocol and WebSocket communication for IoT applications
- Design scalable, secure, and reliable IoT system architectures
- Implement real-time data exchange mechanisms
- Handle network protocols and data serialization formats
- Develop cloud integration strategies for IoT deployments

### Key Concepts

#### MQTT Protocol Deep Dive

**MQTT (Message Queuing Telemetry Transport):**
MQTT is a lightweight, publish-subscribe messaging protocol designed for constrained devices and low-bandwidth, high-latency networks.

**Key Features:**
- **Lightweight:** Minimal protocol overhead
- **Publish-Subscribe:** Decoupled communication model
- **Quality of Service (QoS):** Three levels of message delivery assurance
- **Retain Messages:** Last message stored and delivered to new subscribers
- **Will Messages:** Automatic notification when client disconnects unexpectedly

**QoS Levels:**
- **QoS 0:** At most once delivery (fire and forget)
- **QoS 1:** At least once delivery (acknowledged delivery)
- **QoS 2:** Exactly once delivery (assured delivery)

**Topic Structure:**
MQTT uses hierarchical topics separated by forward slashes:
```
home/livingroom/temperature
home/livingroom/humidity
home/bedroom/temperature
sensors/outdoor/weather/temperature
sensors/outdoor/weather/pressure
```

**Wildcards:**
- **Single-level wildcard (+):** `home/+/temperature`
- **Multi-level wildcard (#):** `home/livingroom/#`

**Advanced MQTT Implementation:**
```python
import paho.mqtt.client as mqtt
import json
import time
import threading
from datetime import datetime

class IoTDevice:
    def __init__(self, device_id, broker_host, broker_port=1883):
        self.device_id = device_id
        self.broker_host = broker_host
        self.broker_port = broker_port
        self.client = mqtt.Client(client_id=device_id)
        
        # Configure callbacks
        self.client.on_connect = self.on_connect
        self.client.on_message = self.on_message
        self.client.on_disconnect = self.on_disconnect
        
        # Configure will message
        will_topic = f"devices/{device_id}/status"
        will_message = json.dumps({
            "status": "offline",
            "timestamp": datetime.now().isoformat()
        })
        self.client.will_set(will_topic, will_message, qos=1, retain=True)
        
        self.is_connected = False
        self.sensor_data = {}
        
    def on_connect(self, client, userdata, flags, rc):
        if rc == 0:
            self.is_connected = True
            print(f"Device {self.device_id} connected successfully")
            
            # Publish online status
            status_topic = f"devices/{self.device_id}/status"
            status_message = json.dumps({
                "status": "online",
                "timestamp": datetime.now().isoformat()
            })
            client.publish(status_topic, status_message, qos=1, retain=True)
            
            # Subscribe to control topics
            control_topic = f"devices/{self.device_id}/control/+"
            client.subscribe(control_topic, qos=1)
            
        else:
            print(f"Connection failed with code {rc}")
    
    def on_message(self, client, userdata, msg):
        try:
            topic = msg.topic
            payload = json.loads(msg.payload.decode())
            
            print(f"Received message on {topic}: {payload}")
            
            # Handle control messages
            if "control" in topic:
                self.handle_control_message(topic, payload)
                
        except Exception as e:
            print(f"Error processing message: {e}")
    
    def on_disconnect(self, client, userdata, rc):
        self.is_connected = False
        print(f"Device {self.device_id} disconnected")
    
    def handle_control_message(self, topic, payload):
        command = topic.split('/')[-1]
        
        if command == "reset":
            print("Resetting device...")
            self.sensor_data = {}
            
        elif command == "config":
            print(f"Updating configuration: {payload}")
            
        elif command == "shutdown":
            print("Shutting down device...")
            self.disconnect()
    
    def connect(self):
        try:
            self.client.connect(self.broker_host, self.broker_port, 60)
            self.client.loop_start()
            
            # Wait for connection
            while not self.is_connected:
                time.sleep(0.1)
                
        except Exception as e:
            print(f"Connection error: {e}")
    
    def disconnect(self):
        if self.is_connected:
            self.client.loop_stop()
            self.client.disconnect()
    
    def publish_sensor_data(self, sensor_type, value, unit=None):
        if not self.is_connected:
            print("Device not connected")
            return False
        
        topic = f"sensors/{self.device_id}/{sensor_type}"
        
        message = {
            "device_id": self.device_id,
            "sensor_type": sensor_type,
            "value": value,
            "unit": unit,
            "timestamp": datetime.now().isoformat()
        }
        
        try:
            result = self.client.publish(topic, json.dumps(message), qos=1)
            
            if result.rc == mqtt.MQTT_ERR_SUCCESS:
                print(f"Published {sensor_type}: {value} {unit or ''}")
                return True
            else:
                print(f"Failed to publish {sensor_type} data")
                return False
                
        except Exception as e:
            print(f"Error publishing data: {e}")
            return False
    
    def start_sensor_monitoring(self, interval=5):
        """Simulate sensor data collection and publishing"""
        def monitor():
            import random
            
            while self.is_connected:
                # Simulate sensor readings
                temperature = random.uniform(20, 30)
                humidity = random.uniform(40, 80)
                pressure = random.uniform(1000, 1020)
                
                # Publish sensor data
                self.publish_sensor_data("temperature", temperature, "°C")
                self.publish_sensor_data("humidity", humidity, "%")
                self.publish_sensor_data("pressure", pressure, "hPa")
                
                time.sleep(interval)
        
        # Start monitoring in separate thread
        monitor_thread = threading.Thread(target=monitor)
        monitor_thread.daemon = True
        monitor_thread.start()

# Example usage
if __name__ == "__main__":
    # Create IoT device
    device = IoTDevice("sensor_001", "broker.hivemq.com")
    
    try:
        # Connect to broker
        device.connect()
        
        # Start sensor monitoring
        device.start_sensor_monitoring(interval=2)
        
        # Keep running
        while True:
            time.sleep(1)
            
    except KeyboardInterrupt:
        print("Shutting down...")
        device.disconnect()
```

#### WebSocket Communication

**WebSocket Protocol:**
WebSocket provides full-duplex communication channels over a single TCP connection, enabling real-time bidirectional data exchange.

**Key Features:**
- **Full-duplex:** Simultaneous bidirectional communication
- **Low latency:** Minimal protocol overhead
- **Real-time:** Instant data transmission
- **Persistent connection:** Maintains connection state
- Uses: Live sensor data streaming.
- Example:
  ```javascript
  const ws = new WebSocket("ws://example.com");
  ws.onopen = () => ws.send(JSON.stringify({ temp: 25 }));
  ws.onmessage = (event) => console.log(event.data);
  ```

#### IoT System Design
- Components:
  - Devices: ESP8266, Arduino.
  - Network: WiFi, MQTT, WebSockets.
  - Cloud: AWS IoT, Google Cloud for alerts.
- Principles:
  - Scalability: Support multiple devices.
  - Security: Encrypt data, authenticate devices.
  - Reliability: Handle network failures.
- Example: ESP8266 sends temperature data:
  ```python
  import network
  wlan = network.WLAN(network.STA_IF)
  wlan.active(True)
  wlan.connect("SSID", "PASSWORD")
  import urequests
  urequests.post("http://example.com/log", json={"temp": 25.5})
  ```

### Summary Table
| Protocol | Use Case | Example |
|----------|----------|---------|
| MQTT | Low-bandwidth IoT | Publish temp |
| WebSockets | Real-time streaming | Sensor data to web |
| WiFi | Connectivity | ESP8266 connection |

## Hardware Integration

### Objectives
- Control actuators using sensor data.
- Understand communication protocols (UART, I2C).
- Implement embedded logic for robotics applications.

### Key Concepts

#### Relay Control and UART
- Relay: Switches high-power devices using transistor and flyback diode.
  - Example:
    ```cpp
    #define RELAY_PIN 8
    void setup() {
      pinMode(RELAY_PIN, OUTPUT);
    }
    void loop() {
      digitalWrite(RELAY_PIN, HIGH); delay(1000);
      digitalWrite(RELAY_PIN, LOW); delay(1000);
    }
    ```
- UART: Asynchronous serial communication; baud rate typically 9600.
  - Pins: TX (transmit), RX (receive).
  - Example:
    ```cpp
    void setup() {
      Serial.begin(9600);
    }
    void loop() {
      if (Serial.available()) {
        Serial.print("Received: ");
        Serial.println(Serial.read());
      }
    }
    ```

#### Actuator Decisions from Sensors
- Logic: Sensors trigger actuators based on conditions.
- Example: Ultrasonic sensor controls LEDs:
  ```cpp
  if (distance <= 50) {
    digitalWrite(redLED, HIGH);  // Risk zone
    Serial.println("Risk zone!");
  } else {
    digitalWrite(greenLED, HIGH);
    Serial.println("Safe zone");
  }
  ```
- Robotics Example: Obstacle avoidance:
  ```cpp
  if (front < 10 && left < 10 && right < 10) {
    stopRobot();  // Stop or reverse
  } else if (front < 10 && left > 20) {
    turnLeft();
  }
  ```

#### Embedded Logic and Communication
- Embedded Logic: Microcontroller processes sensor data for decisions.
  - Example: Gesture recognition triggers motor.
- Communication Protocols:
  - UART: Asynchronous, simple.
  - I2C: Two-wire (SDA, SCL) for multiple devices.
  - SPI: High-speed, for displays, SD cards.
- Example (I2C):
  ```cpp
  #include <Wire.h>
  void setup() {
    Wire.begin();
    Wire.beginTransmission(0x27);
    Wire.write("Data");
    Wire.endTransmission();
  }
  ```

### Summary Table
| Component | Function | Example |
|-----------|----------|---------|
| Relay | Switch high-power devices | Control motor |
| UART | Serial communication | Send/receive data |
| Actuator | Signal to motion | Servo motor |
| Sensor Logic | Decision-making | Obstacle avoidance |
