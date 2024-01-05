
6 7 1415


```cpp
  

#include "vex.h"

  

using namespace vex;

  

bool calibrated = false;

bool turned = false;

  

void calibrateInertial() {

if (!calibrated) {

I9.calibrate();

wait(3000, msec);

calibrated = true;

}

}

  

void turnAround() {

if (!turned) {

int targetHeading = I9.heading() + 90;

  

// Turn until the target heading is reached

while (abs(targetHeading - I9.heading()) > 2.0) {

L1.spin(forward, 66, percent);

L2.spin(forward, 66, percent);

R1.spin(forward, -66, percent);

R2.spin(forward, -66, percent);

wait(10, msec);

L1.setStopping(

}

  

// Stop the motors

L1.stop(hold);

L2.stop(hold);

R1.stop(hold);

R2.stop(hold);

  

turned = true;

  

// Add a delay after turning to prevent continuous turning

wait(500, msec);

}

}

  

void move(int l, int r, int q = 100) {

L1.setMaxTorque(q, percent);

L1.spin(forward);

L1.setVelocity(l, percent);

  

L2.setMaxTorque(q, percent);

L2.spin(forward);

L2.setVelocity(l, percent);

  

R1.setMaxTorque(q, percent);

R1.spin(forward);

R1.setVelocity(r, percent);

  

R2.setMaxTorque(q, percent);

R2.spin(forward);

R2.setVelocity(r, percent);

}

  

int main() {

calibrateInertial();

  

while (true) {

if (Distance10.objectDistance(mm) < 1000) {

turnAround();

} else {

if (turned) {

turned = false;

move(66, 66);

}

}

wait(100, msec);

}
wait ()111

}
```