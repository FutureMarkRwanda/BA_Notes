# 5-Day Robotics & Embedded Systems Camp Plan
## Building a Self-Balancing Robot

**Target Audience**: Ages 12–16, Beginners with Basic Computer Skills  
**Created**: July 23, 2025  
**Contact**: [Your Name], [Your Email]

---

## Camp Objective
The camp guides participants to build a working **self-balancing robot** by Day 5, introducing foundational concepts in robotics, electronics, and embedded systems. Designed for beginners aged 12–16, it emphasizes hands-on learning, teamwork, and creativity.

---

## Safety Guidelines
- **Hot Glue Guns**: Use under adult supervision. Wear gloves and avoid hot surfaces.  
- **Batteries**: Check polarity before connecting to prevent short circuits. Use insulated holders.  
- **Tools**: Handle screwdrivers and scissors carefully. Store safely when not in use.  
- **Electronics**: Power off circuits before modifying wiring to avoid damage or shocks.

---

## Daily Structure (4 Hours with 15-Min Break)
- **Intro (25 min, 10%)**: Recap previous day and set expectations.  
- **Theory & Demo (75 min, 30%)**: Teach concepts with examples or diagrams.  
- **Hands-On Practice (125 min, 50%)**: Build parts of the final project.  
- **Wrap-Up (25 min, 10%)**: Reflect on learnings and set next session’s goals.

---

## 5-Day Program Overview

### Day 1: Introduction to Robotics and Basic Electronics
**Topics Covered**:  
- What is a robot? Examples (e.g., robotic arms, drones).  
- Core components: sensors, microcontroller, actuators.  
- Basics of electricity: voltage, current, polarity.  
- Components: LEDs, resistors, motors.  

**Activities (125 min)**:  
- Icebreaker (20 min): Draw a dream robot and share its purpose. Ensure all team members contribute.  
- Discuss real-world robot applications (15 min).  
- Build a simple circuit with a battery, LED, and resistor (45 min).  
- Explore current flow using a multimeter (45 min).  

**Assessment**: 5-question quiz on circuit components (10 min).

---

### Day 2: Arduino, Motors, and Motor Drivers
**Topics Covered**:  
- Arduino UNO/Nano as a microcontroller.  
- Digital outputs and PWM (explained as a dimmer switch).  
- L298N motor driver: function and wiring.  

**Activities (125 min)**:  
- Blink an LED using Arduino (30 min).  
- Spin a DC motor via L298N (45 min).  
- Code to change motor direction and speed (30 min).  
- Mount motors and wheels to chassis (20 min).  

**Assessment**: Demonstrate motor speed control (5 min per team).

---

### Day 3: Sensors and Control – The MPU6050
**Topics Covered**:  
- Sensors: role in robotics (e.g., detecting tilt).  
- MPU6050: accelerometer and gyroscope basics.  
- I2C communication (explained as a two-way conversation).  
- Feedback systems for balance.  

**Activities (125 min)**:  
- Wire MPU6050 to Arduino and display tilt data (45 min).  
- Code LED to light up based on tilt (30 min).  
- Group exercise: Balance on one leg to simulate robot balance (15 min).  
- Discuss center of gravity (30 min).  

**Assessment**: Show correct MPU6050 data on Serial Monitor (5 min).

---

### Day 4: Self-Balancing Robot Assembly and Wiring
**Topics Covered**:  
- Sensor-motor control loop.  
- Wiring: Arduino, MPU6050, L298N, motors.  
- Center of mass and structural symmetry.  
- Battery safety and power considerations.  

**Activities (125 min)**:  
- Mount motors to chassis (20 min).  
- Connect MPU6050 and L298N to Arduino (30 min).  
- Secure battery and check polarity (15 min).  
- Upload base balancing code and test motor response (wheels off, 60 min).  

**Assessment**: Verify wiring and motor response to tilt (5 min).

---

### Day 5: Tuning, Testing, and Demonstration
**Topics Covered**:  
- Finalizing robot structure.  
- PID control (simplified as adjusting balance sensitivity).  
- Troubleshooting: oscillation, sensor noise.  
- Performance optimization.  

**Activities (125 min)**:  
- Attach wheels and upload final code (30 min).  
- Tune PID values using pre-set sliders (45 min).  
- Test robot on flat surface (30 min).  
- Demo robots and present team names (20 min).  

**Assessment**: Rate robot balance stability (1–5 scale, 5 min).

---

## Materials Checklist (Per Team of 3–4)
- Arduino UNO or Nano  
- L298N motor driver  
- 2 geared DC motors with wheels  
- MPU6050 sensor  
- 7.4V battery + holder  
- Breadboard, jumper wires  
- USB cable for Arduino  
- Cardboard/plastic chassis  
- Hot glue gun, glue sticks  
- Screwdrivers, tape, scissors  
- Laptop with Arduino IDE  

**Alternatives**: Use ADXL345 if MPU6050 unavailable; recycled cardboard for chassis.

---

## Optional Add-ons (Day 5, Time-Permitting)
- **Ultrasonic Sensor (30 min)**: Add HC-SR04 for obstacle avoidance. Requires wiring and code.  
- **Bluetooth Control (40 min)**: Use HC-05 for app-based control. Needs serial setup.  
- **Video Documentation**: Record team demos (15 min).

---

## Engagement and Delivery Tips
- Use mini-quizzes to recap topics (e.g., 5 questions on Day 3).  
- Assign team roles: coder, wirer, assembler.  
- Encourage creativity with team names or chassis decorations.  
- Support diverse learners: Provide wiring diagrams for visual learners, simplified code for beginners.  
- Scale for group size: 3–4 per team; add stations for larger groups.  
- Backup tasks: If ahead, experiment with LED patterns; if behind, test motors individually.  
- Award certificates for teamwork, creativity, or perseverance.

---

## Feedback and Assessment
- **Daily**: Use quizzes or demos to check understanding (see daily assessments).  
- **Post-Camp**: Distribute feedback form (rate difficulty, fun, clarity on 1–5 scale).  
- **Progress Tracking**: Use checklist: “Circuit built,” “Code uploaded,” “Robot balances for 5 seconds.”