# Example Autonomous (Far Side)
Far side auton is pretty easy to do in VEX Over Under.  

All you have to do is:  
- Keep preload on the back of robot.
- At the start of auton, drive full speed backwards into the goal.
- Wait there for a few seconds.
- Drive forwards (away from goal).

This can be achieved through direct control of the motors of the drivetrain.  
Instead of using distance movements (like drive for 5 inches) you would use voltage movements (like drive backwards at 12 volts for 3 seconds).  

Here is how you do this in common IDEs:

VEXcode V5  

<img width="296" alt="Screen Shot 2023-11-19 at 12 40 54 PM" src="https://github.com/zayndamji/example-auton/assets/86502397/9fbb8b3b-c3ab-41bf-bda9-5a4f962729ad">
  
VEXcode Pro V5
```c++
motor LeftMotor1 = motor(PORT6, ratio6_1, true);
motor LeftMotor2 = motor(PORT7, ratio6_1, false);
motor LeftMotor3 = motor(PORT8, ratio6_1, true);

motor RightMotor1 = motor(PORT16, ratio6_1, false);
motor RightMotor2 = motor(PORT17, ratio6_1, false);
motor RightMotor3 = motor(PORT18, ratio6_1, true);

motor_group LeftDrive = motor_group(LeftMotor1, LeftMotor2, LeftMotor3);
motor_group RightDrive = motor_group(RightMotor1, RightMotor2, RightMotor3);

drivetrain Drivetrain(LeftDrive, RightDrive);

void autonomous(void) {
  // drive backwards at full speed for 5 seconds
  LeftDrive.spin(directionType::rev, 12, volt);
  RightDrive.spin(directionType::rev, 12, volt);
  wait(5, seconds);

  // drive away from goal (forwards)
  Drivetrain.driveFor(12, distanceUnits::in);
}
```

JAR Template (VEXcode Pro V5)
```c++
void autonomous(void) {
  // drive backwards at full speed for 5 seconds
  chassis.drive_with_voltage(-12, -12);
  wait(5, seconds);

  // drive away from goal (forwards)
  chassis.drive_distance(12);
}
```
