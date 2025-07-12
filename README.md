Task: Simulate 6 Servo Motors with Sweep and Hold Function
For this task, I was asked to simulate 6 servo motors using Arduino code that would make all the motors sweep back and forth for 2 seconds, and then hold them all at a 90° angle. The entire task was done virtually using Tinkercad’s Circuits Simulator.

Tools & Components I Used:
- Tinkercad (Circuits Simulator) – Used to build the virtual circuit and run the Arduino code without needing any physical hardware.
- Arduino UNO – The microcontroller board that controlled all 6 servos.
- 6 Servo Motors – Each one controlled using its own signal pin.
- Breadboard – Helped distribute power (5V and GND) to all the motors.
- Wiring:
  - Red wire (VCC) – From Arduino 5V pin → breadboard power rail → all servos.
  - Black/Brown wire (GND) – From Arduino GND pin → ground rail → all servos.
  - Yellow/Orange wire (Signal) – From Arduino digital pins 2 to 7 → each servo’s signal pin.

What I Built:
 1. Servo Setup
I connected six servo motors to digital pins 2 through 7 on the Arduino. Power and ground were shared through the breadboard to all motors.

 2. Arduino Code
I used the built-in Servo library and created 6 servo objects. The program did the following:
For the first 2 seconds, all 6 servos swept back and forth using a sine function for smooth motion.
After 2 seconds passed, all servos were set to and held at exactly 90 degrees.
The sweeping used the sin() function to create a fluid 0° → 180° → 0° motion over 2 seconds.

 3. Simulation
Ran the simulation in Tinkercad and verified that:
The motors moved back and forth smoothly for the first 2 seconds.
All motors then locked into 90° and stayed still afterward.

Reflection:
This task helped me understand how to control multiple servo motors simultaneously using Arduino. I also learned how to use timing and mathematical functions (sin) to create smooth motion patterns. The simulation made it easier to visualize and test the behavior of all six servos without needing any physical parts.



Code:
#include <Servo.h>

// Create Servo objects for pins 2–7
Servo servo1, servo2, servo3, servo4, servo5, servo6;

unsigned long startTime;

void setup() {
  // Attach each servo to its pin
  servo1.attach(2);
  servo2.attach(3);
  servo3.attach(4);
  servo4.attach(5);
  servo5.attach(6);
  servo6.attach(7);

  startTime = millis();      // remember when we started
}

void loop() {
  unsigned long t = millis() - startTime;

  if (t <= 2000) {
    // For first 2000 ms, sweep each servo 0→180 and back
    int angle = (int)(90 + 90 * sin(PI * t / 1000.0)); 
    // sin(π * t/1000) goes 0→1→0 over 2 s
    servo1.write(angle);
    servo2.write(angle);
    servo3.write(angle);
    servo4.write(angle);
    servo5.write(angle);
    servo6.write(angle);
  } else {
    // After 2 s, hold all at 90°
    servo1.write(90);
    servo2.write(90);
    servo3.write(90);
    servo4.write(90);
    servo5.write(90);
    servo6.write(90);
  }
}
