<!-- 
<table>
<tr>
<th width=250>
CONTENT
</th>
</tr>
</table>
-->

<div style="display: flex; flex-direction: column; align-items: center; justify-content: center;"
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;">
<h1 align = center> Future Engineers 2025 </h1>
<h2 align = center> Team name: QYZYLORDA Flame </h2>
<h2 align = center> Team members: Sadu Yernur, Bizhanuly Aidar </h2>
<h2 align = center> email: qzo.flame.fe2024@gmail.com </h2>
<div style="display: flex; flex-direction: column; align-items: center; justify-content: center;"
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;">
<div align = center>
  <img src=https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/QZO_Logo12.png> 
  <img src="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/QZO_logoo.jpg">
</div>
</div>
</div>
<h2 align = center> Our team already participated in the last 2024 season and we won second place in FE category</h2>
<div align = center>
<img src="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/2024.jpeg"/>
</div>

# Contents 
* [**Mobility management**](#mobility-management)
  * [Chassis design](#chassis-design)
  * [Weight distribution](#weight-distribution)
  * [Camera position](#camera-position)
  * [Motor selection](#motor-selection)
* [**Power and sense management**](#Power-and-sense-management)
  * [Power management and choiсe of power source](#Power-management-and-choiсe-of-power-source)
  * [Sense management](#sense-management)
* [**Obstacle management**](#obstacle-management)
  * [Parking pasition](#parking-position)
  * [Kalman Filter](#kalman-filter)
  * [Ultrasonic rotation control](#ultrasonic-rotation-control)
* [**Pictures**](#pictures)
  * [Robot Photos](#robot-photos)
  * [Team Photos](#team-photos)
* [**Performance videos**](#performance-videos)
* [**Code explanation**](#code-explanation)
* [**Conclusion**](#conclusion)
  * [Limitations](#limitations)
  * [Sugestions for further development](#sugestions-for-further-development)
# <hr/>
<!-- 



-->
# Mobility Management

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalscheme.jpg)
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalpixyview.jpg)
<p>   Our robot is designed by lego, especially we used LEGO MINDSTORMS Education Core Set(Serial number 45544) and other LEGO EV3 sets: EV3 Expansion Set, EV3 Homeschool Combo Pack and others. You can view all of the LEGO EV3 sets by this link: <a href="https://www.bricklink.com/catalogList.asp?catType=S&catString=166.59.800">BrickLink[1]</a>. Robot's wheels are taken from LEGO SPIKE Prime set and its expansion set(serial numbers 45678-1 and  45680-1). </p> </br>
  
<p>   For better stability we used differential with two motors at the rear axle and steering control as required in the rules, our robot's size is 24.5cm (length); 14cm(width) and 29cm(height). We constructed the robot as small as possible, so its projection doesn't interfere during parking. </p>

<div align=center>
<table>
<tr>
<th width=250>
  
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/concepts/parallelparkingscheme.jpeg) </br>
</th>
</tr>
</table>
</div>

### Chassis design

The base of our chassis design comes from parallel steering model geometry. Wheels that are connected to the steering control always turn on the same angle. However, last year we used Pro-Akkerman steering model geometry. The difference is in the angle of the wheels. Pro-Akkerman makes inner wheel turn more than outer wheel, because distances that inner and outer wheels go are dissimilar(while turning).
<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/concepts/akkermanangles.jpg" alt="Ackermann Design">

<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/concepts/turndistance.jpg" width="500" height="350" alt="Ackermann Design">
With a parallel steering model, the inner wheel does not align with its natural turning radius and tends to scrub against to surface, causing potential danger for the stability. Akkerman system might look better and <B>it is</B>, but not for a small robot. You see, Akkerman steering model was created for a bigger and more massive things like cars, that weight tons and friction with the road is high and triggers scrubbing. Our small robot weights ~0,8 kilograms and friction with the surface is insignificant. If we gonna use Akkerman in order to solve this problem, it may have opposite effect and inner wheels will slip while turning.

<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalbalance.jpg" width="600">

Also, Akkerman is not efficient, when it comes to low speed in Lego robots. Our components are not professional and expensive like big companies use, so our components have gaps in linkages and connectors. At low speeds and small steering angles, these gaps can become comparable to intended turning angle itself. For example, if we are gonna give command to turn on 5 degrees, robot may not turn at all and it ruins microcontrolling
### Weight distribution
  As our robot is a self-driving car with steering mechanism and differential in rear axle we need to make our robot slight heavy, and distribute weight a bit behind the center of our robot to prevent the wheels from slipping. The slipping of the wheels in rear axle impacts our odometry and the programm.Also, we placed the EV3 P-Brick in the center of the robot to distribute the weight evenly, as the brick is a relatively heavy component(275g). Pixy camera is located quite behind the robot,that's why it don't maintain balance.
  
### Camera position
  Our camera places as much higher(28cm) and behind(7cm from center of the robot) as its possible for better view and obstacle control. It also inclined a bit down to view blocks that are close to robot and limit the view for better obstacle management.
</div>

### Gyro sensor PD regulator and turns, angular rotation
LEGO EV3 Gyro Sensor is used to measure the angular rotation of the robot, allowing precise detection of turns. This data is fed into a PD regulator (Proportional-Derivative regulator), which ensures smoother control during turns, such as achieving an exact 90-degree rotation.  Change in the PD coefficients with dependence to the steering and its PID regulator enhances the robot’s maneuverability. Additionally, the gyro sensor is a significant part in the robot’s odometry system, providing opportunities to track its orientation and improve overall navigation accuracy.

### Steering control
The PID regulator controls the steering mechanism by setting a specific variable called “aim”, which represents the target position or direction. The PID controller is used to set the steering motor encoder and compare its current position to the value of “aim.” Based on this comparison, the PID algorithm sets the motor’s movement to smoothly align the steering mechanism with the desired direction. This ensures precise and stable control over the robot’s steering, allowing it to maintain accurate and smooth maneuvers during operation.

### Bypassing obstacles
The Pixy camera is used to detect obstacles and it captures visual data like X and Y coordinates, signature and processes it to identify objects. Once an obstacle is detected, the camera's data used to manipulate robot’s steering system. By specific formula that uses 3 parameters(signature, X and Y coordinate) values are setted and then transmitted to PID regulator of steering mechanism by setting proportional, integral, and derivative values to smoothly navigate around the obstacles. This approach allows the robot to bypass obstacles in real-time, improving its mobility and efficiency in dynamically.

### Aligning robot to the center
Odometry is utilized to align the robot to the center by combining the Gyro sensor’s PD regulator and odometry coordinates. A new PD regulator ensures smooth and precise alignment. This process corrects the robot’s position and orientation relative to the centerline straightforward zones. Aligning to the center is crucial because it compensates for the Pixy camera’s limited view angle, ensuring that the camera accurately detects obstacles or paths ahead. This alignment improves the robot’s navigation accuracy and stability during operation and improves Pixy camera's view angle so it can always detect the objects and view it.

### Motor selection
  We have a choice between 2 types of LEGO motors: large motor and medium motor, the large motor is powerful but the speed is lower, the medium motor is not that powerful but have a great speed. The comparison can be viewed by this link: <a href="https://www.eurobricks.com/forum/index.php?/forums/topic/87670-ev3-large-and-medium-motors-comparison/">Comparison of technical specifications[2]/</a>. According to <a href="https://www.researchgate.net/publication/345182894_Dynamic_analysis_modeling_and_control_of_the_LEGO_EV3_modular_mobile_platform">research[3]</a> 

* Large servo motor (actuator) - maximum operating speed of 170 rpm, torque of 0.2 Nm and stopping torque of 0.4 Nm. It is positioned in the engine case an integrated encoder, a rotation meter, whose step is 1 degree of rotation and least sampling time 0.001 s.Also the power and speed is regulated by gear wheels and the size of the wheels. We choosed smaller wheels in steering mechanism because they do not move the robot, the only moves its trajectory.
* Medium-size servo motor - maximum speed of 250 rpm, running torque 0.08 Nm and stopping torque of 0.12 Nm, also with integrated encoder, identical to that of a large engine.

  
  <img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/medium%20motor.jpg> 
</br>
Also the wheels have low coefficient of friction to avoid loss of energy, but for wheels in the rear axles it will be better to choose wheels with a bit high cofficient of friction to avoid slipping of wheels. The rear wheels are bigger than wheels in front axle to have a better stability, movement control and the speed. It will be better to choose little smaller rear wheels than our. 
</br>
  The explanation of our construction design is on our youtube channel <a href="https://www.youtube.com/channel/UC0_5yZ2aPdJc0X5wtIw4ZcA">"QZO Flame"[4] (tag: @QZOFlame)</a>.
   
   * [Building Instructions and BOM](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Instructions/instruction.pdf)
   * [3D model of Pixy Camera_Case](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/3D_models/README.md) <br> (used application AutoCAD)
# <hr/>

# Power and sense management 

</br>

### Power management and choiсe of power source

The core of our robot is the <a href="https://pybricks.com/ev3-micropython/startbrick.html">EV3 Programmable Brick[5]</a> 
Its power comes from a **rechargeable 10V Lithium Battery**.  
We decided to use a rechargeable battery instead of 6 AA batteries.  

Despite AA batteries having a higher capacity, they can still be inconvenient and risky to use while rechargeable batteries can be charged in parallel so, one is in use while another is charging. Single use batteries have to be constantly replaced, which can cause big problems during the olympiad.  

Even rechargeable AA batteries (such as GP types) require additional adapters for charging, and usually only 2–3 cells can be charged at a time, whereas the robot requires all 6.  

The EV3 P-Brick has **4 ports for motors** and **4 ports for sensors**.  
Power consumption details for motors and sensors can be found here:  
<a href="https://www.dexterindustries.com/ev3-current-consumption-measurement/">EV3 Current Consumption Measurement[6]</a>

<table>
<tr>
<td align="center">
<img src="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/EV3_P-Brick_demonstration.jpg" width="500">
</td>
</tr>
<tr>
<td align="center">
  <img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/batteries.jpg" width="300">
  <img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/battery%20slot.png" width="300">
  
</td>
</tr>
</table>


  * [Electroschemes/wiring diagrams](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/schemes/README.md)

    ## Why did we choose EV3 P-Brick?
    <ul>
    <li font size="10">EASY TO USE</li> <br>
    The EV3 comes with graphical programming environment (LEGO Mindstorms EV3 software), and it makes it much easier. This visual approach is more accessible than writing code in languages like C++ (Arduino) or Python (Raspberry Pi).Moreover, EV3 can be programmed very quickly thanks to its drag and drop graphical environment. This allows teams to make fast adjustments like surprises or fix errors during competitions, saving valuable time.<br> <br><br>
    <li>INTEGRATED HARDWARE</li> <br>
    EV3 comes with specialized LEGO motors and sensors (like color, infrared, and gyro), which are easy to connect and calibrate. Third-party developers can integrate their own devices thanks to the EV3 Firmware Developer Kit(With this Firmware Developer Kit you get the information you need if you want to understand the firmware architecture of the LEGO MINDSTORMS EV3 Programmable brick).For example we use "Pixy camera Lego Mindstorms EV3" edition with no need to download or edit firmware by ourselves.<br> <br><br>
    <li>PORTABILITY</li>
    <br>
    EV3 is more portable and compact,because it is designed for easy handling, and its components are built with the purpose of being assembled and taken apart for quick project changes.LEGO MINDSTORMS EV3 Brick weighs approximately 215 grams. We can put all our kit in one box. <br> <br><br>
    <li>ROBOT DESIGNING</li>
    <br>
Our robot was almost built only by LEGO details except camera and we can change its construction very quick, while Arduino or Raspberry Pi may face problem, that they can't change design because it was made by 3D-printer and etc  <br> <br><br>
 
  ### EV3 P-Brick Energy distribution
  EV3 P-Brick have 4 ports for sensors and motors and all of them distributes and contributes most of the energy resources. While LEGO sensors contribute as much energy as they need by built-in control systems and framework abilities, varying between number of iteration per second, energy consumption and framework and IDE's abilities to proceed amount of data. Then the motors energy distribution is often regulated by control algorythms and values given in the programm, consequentlyleading to smart energy distribution to provide enough power and maintain accuratte readings without overloading.
  
  ### Monitoring features and flexibilty
  The LEGO EV3 power management system improves flexibility and efficiency through its convenient monitoring features and adaptable power options. The system supports multiple configurations, such as rechargeable lithium-ion batteries or standard AA batteries, providing a choice between them, also it is easier to change between batteries in LEGO because of real-time battery monitoring system that enables active energy management, providing alerts for low power and ensuring uninterrupted operation. This flexibility is further enhanced by integration with external power sources for extended runtime, while the monitoring features ensure optimal performance and safe components during tasks.
  
  ### Comparison with other popular controllers
  
  <table>
    <tr>
      <th width=33%>
        
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/EV3_P-Brick.png)
  
  EV3 P-Brick </th>
      <th width=33%>
        
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/Arduino_UNO.jpeg)
        
  Arduino UNO 
      </th>
      <th width=33%> 
      
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/Raspberry_Pi_4B.png)
       
  Raspberry Pi </th>
    </tr> 
    <tr>
    <td colspan=3 align=center> processor </td>
    </tr>
    <tr>
      <td align=center> 300 MHz, 1 core </td>
      <td align=center> 16MHz </td>
      <td align=center> 1.5 GHz, 4 cores </td>
    </tr>
     <tr>
    <td colspan=3 align=center> ports </td>
    </tr>
    <tr>
      <td align=center> 4 ports for sensors, 4 ports for motors </td>
      <td align=center> 14 digital, 6 analog pins </td>
      <td align=center> 40 GPIO pins </td>
    </tr>
    <tr>
    <td colspan=3 align=center> programming </td>
    </tr>
    <tr>
      <td align=center> LEGO Mindstorms, limited Python and C++ </td>
      <td align=center> Arduino IDE (C, C++ based) </td>
      <td align=center> Multiple languages (Python, C++, Java, etc.) </td>
    </tr>
  </table>
  </br>
  </br>
  
## Sense management 

</br>
 UART sensors of LEGO EDUCATION MINDSTORMS EV3 Core Set such as color, ultrasonic and gyro sensors are used for sense management of our robot. Gyro sensor saves initial robot position in degrees and counts the displacement from it and it allows us to find drifts in turns or long movements and compensate them in real time. Ultrasonic sensor measures the distance from the robot to a wall and robot can recognize his direction in the start, because of differences of measurements and it is also used for obstacle detection, if the distance changes surprisingly compared to the predicted one. Lines, crossing and markers can be detected by a single color sensor. Encoders in medium motors know the distance robot moved with high accuracy, cause they count rotation of each motor in degrees, which can be converted by circular formulas into wheel rotations and finally into the distance what robot travelled. Our program uses a combination of these sencors to create the odometry of our robot. By using encoders, gyro sensor and pythagoras theorem we find the displacement that robot moves from starting position and convert it into x and y coordinates. In the beginnig of the round while standing in the parking zone robot can understand his direction, because ultrasonic is always pointed to the right, so if the direction is clockwise-ultrasonics measurements wil show a big value and opposite. The center of the every straightforward section is the center of odometry where x and y coordinates are zero. Odometry is constantly corrected to avoid drift errors that appear because of wheel slip, inaccurate sensor values or mechanical imperfections. Ultrasonic sensor and gyro sensor are used to fix odometry also by pythagoras theorem and exceptions for the situations when ultrasonic sensor view blocks or gives suspicious results. This combination of sensors makes a stable navigation system where errors from one sensor can be compensated by comparision with others. For example, when encoders accumulate a small error in long straight lines and it becomes bigger and bigger, gyro sensor starts correcting the direction; when gyro slightly drifts, encoders and ultrasonic give stable feedback;when odometry shifts, color sensor is used as reference for field parts. The detailed info is given by links related to each sensor's purpose.
  
  * [color sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/color_sensor.md)
  * [ultrasonic sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/ultrasonic_sensor.md)
  * [gyro sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/gyro_sensor.md)
  * [encoders from motors](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/encoders_from_motors.md)
  * [odometry](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/odometry.md)
# <hr/>
<!-- 

























-->
# Obstacle management
  For the obstacle detection we used Pixy2 camera and PixyMon v2 application to configure it. To use it in LEGO MINDSTORMS application you need to install special library, because it is third-party device. All of the downloads are able in official site of Pixy2 <a href="https://pixycam.com/downloads-pixy2/">Pixy[7]</a>.We get x y coordinates on the field from the Pixy camera by placing the robot on two points along the correct trajectory of robot (If the pillar is red, it should go around on the right, if it is green, on the left).From the obtained value of pillars and robot(x,y coordinates) we calculate a linear function by two points (you can calculate it by the link:) <a href="https://planetcalc.com/8110/?language_select=en&ysclid=m0a3s77i4p794636345">linear function by two points[8].</a> This function is approximate scheme or way of how our robot should move in order to bypass pillars. Every straightforward section has its own coordinate center and 6  possible locations of pillars. Robot changes its odometry coordinate when he passes second line(blue or orange, depends on a direction). Corner sections do not include odometry system, because it doesn't have obstacles there.
  </br> </br>
<table>
<tr>
<th width=500>
  
  ![obstacle detection](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/obstacle_detection.png)
</th>
  <th width=500>
    
  ![obstacle detection](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/Obstacle_detection1.png)
  </th>
  <tr>
    <th width=500>
      
  ![linear function](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/linear_function_convert.png)
</th>
  <th width=500>
    
  ![linear function](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/linear_function.png)
</table>

</br>
<div align = center style="display: flex; flex-direction: column; align-items: center; justify-content: center; color: gray">

<table>
<tr>
<th width=250>
  
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_Management/ICON%20PIxyMon%20v2.png)
<p> 
PixyMon v2 application
</p>
</th>
</tr>
</table>

<table>
<tr>
<th width=400>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_Management/Pixy_Block.png)
<p>
Pixy block for LEGO MINDSTORMS
</p>
</th>
</tr>
</table>


Pixy2 camera is a universal tool as it can work with EV3, arduino and raspberry. </br>
<table>
<tr>
<th width=250>
  
![Pixy camera](https://github.com/user-attachments/assets/f9f93471-1b46-469d-9ef1-d752f6181133)
<p> 
Pixy camera
</p>
</th>
</tr>
</table>
</div>


For the work in LEGO MINDSTORMS application you need to install "pixy block".<br>
This block outputs: </br>
<ol>
<li>Signature id with the highest value of y coordinate </li>
<li>camera's relative x coordinate of the object </li>
<li>camera's relative y coordinate of the object </li>
<li>relative width of the object</li>
<li>relative height of the object </li>
<li>angle of the object to camera </li>
<table>
<tr>
<th width=400>
  
![Pixy2 block](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/Pixy2block.png)
</th>
</tr>
</table>

## Automatic control
The robot's trajectory is determined by two main situations: <br>
<ul>
  <li>
    when pixy camera sees a road sign
  </li>
  <li>
    when pixy camera does not see road sign
  </li>
</ul> <br>

### Bypassing obstacles (when pixy camera sees a road sign)
We use steering mechanism and pixy2 coordinates and connect them with linear function. Y value from pixy2 gives how far the robot should be from the object, using a linear function. Using the obtained value and the real value X from pixy2, we can find an error between robot and pillar and give this error to the steering mechanism. So if the pillar is close to robot linear function gives high values to steering mechanism's motor in order to avoid crush. <br>

https://github.com/user-attachments/assets/eb8f1eea-5bec-42ee-9bcd-57115f89046b
### Align center (when pixy camera does not see road sign)
Our robot aligns itself with the center of the road when it doesn't see an object, so as not to crash into parking spaces or miss a road sign. To center the robot, it uses odometry. The module x coordinate of the center of the road is equal to 25 (x is 25 or -25) because the robot uses segmented odometry (the center coordinate (0;0) is the center of the every straightforward section) <br>
<table>
<tr>
<th width=250>
  
<img src="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/Playfieldodometry_page-0001.jpg?raw=true" width="400">
<p> 
Segmented odometry
</p>
</th>
</tr>
</table>
</div>
It determines the error between the coordinate of the robot and the center of the road and is given to the steering mechanism so that it aligns itself to the center thanks to the constant formula.

## Parking position

We use ultrasonic sensor for precise parking and we already know where parking zone is, because it is located in the section where we started, but since we only have one ultrasonic and in the clockwise run ultrasonic will be pointed to the inner wall, we will have to make turn. Robot will drive till it sees orange line and will turn and align near to the outer walls, so the parking process consists of 3 steps:
<ul>
  <li>drive till the orange</li>
  <li>turning back and aligning </li>
  <li> finding the exact location of the parking</li>
  <li>parallel parking</li>
</ul>
<br>

### Make a turn 
our robot makes a turn if the robot moves clockwise so that the ultrasonic looks at the outer border

### Search for a parking zone
Our robot should move parallel and close to the outer side until it sees the parking zone. To be close to parking is we also use pixy2 relative coordinates and odometry to know the parking zone's position. Counter clockwise run includes backward movement and it stops and moves forward at orange line. Pixy allows robot to not go too far from parking section. Clockwise run includes forward movement and 180 degrees turn when it sees orange.

### park in the zone
To park accurately, an ultrasonic sensor is used, when this sensor notices a parking wall, the robot stops and uses cycle of turning steering wheel right,left and moving back, forward on a short distance. 
<br>
<br>
*Most tasks are performed using a pixy camera, here you can see how to set up this camera*
 * [Pixy2 camera's configuration](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/README.md)


### Kalman filter
Kalman Filter - an algorithm that uses a series of measurements observed over time, including statistical noise and other inaccuracies, to produce estimates of unknown variables that tend to be more accurate than those based on a single measurement, by estimating a joint probability distribution over the variables for each time-step. In other words, whole round lasts for a few minutes and our obstacle management works only thanks for odometry, but in the long term driving, uncertainty rises gradually and in the end it can be crucial to robots movements, that is why we need Kalman Filter, that can compensate error of odometry.

<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Uncertaintity.jpg">
In this graph you can see how error of odometry slowly rises by one minute compared to ultrasonics values. Y coordinate shows the distance between robot and outer wall. 
<div class="section">
  <h3>Kalman Filter Usage</h3>
  <p>
    How we use Kalman Filter? It compares 2 values from odometry and ultrasonic. In case difference is negligible, special coefficient <b>Trust</b> will rise. Normally it is close to 1, so robot will move and trust to Ultrasonics values, but if difference between values are too big or it changes too fast, trust will sharply decline. For example, Ultrasonic can detect the obstacle and its value will decrease, so with trusts downfall, robot will rely on Odometry system.
  </p>
  
## Ultrasonic rotation control
  In most of cases, 3 motors are enough for FE category, but we decided to use last one too in order to improve flexibility of our robot to a hard conditions, that is why last motor rotates Ultrasonic sensor by 180 
  degrees horizontally, increasing view range. How it works? When robot drives toward red pillar, he has to bypass it from right, but if driving direction is clock wise, ultrasonic will be pointed to the left, which means it will detect pillar and potentially it can be dangerous. That is why whenever Ultrasonic can detect pillar, our 4th motor will turn it to the opposite side, inner wall until he bypasses pilar. This system has similarities with LIDAR system.
  <img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelsonic.jpeg" width="600"> 
 <table>
  <tr>
    <th width=33%>Pros / Cons</th>
    <th width=33%>Stationary Ultrasonic</th>
    <th width=33%>Ultrasonic rotation control</th>
  </tr>

  <tr>
    <td><b>Pros</b></td>
    <td align=center>
      It is stable and easier to implement, because of less possible situations
    </td>
    <td align=center>
      Way more accurate and gives a better performance, if you can program it
    </td>
  </tr>

  <tr>
    <td><b>Cons</b></td>
    <td align=center>
      It is not flexible and Ultrasonic might give wrong values because of pillars
    </td>
    <td align=center>
      Possible problems with controlling motor and gear-axle system has a slight backlash
    </td>
  </tr>

</table>

</div>

# <hr/>

# Pictures
### Robot photos

<table>
<tr>
  <th width=50%>

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelfront.jpeg)
  </th>
  <th width=50%>

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelleft.jpeg)
  </th>
</tr>
<tr>
  <td width=50%>
    
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelright.jpeg)
  </td>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelback.jpeg)
  </td>
</tr>
<tr>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelbottom.jpeg)
  </td>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodeltop.jpeg)
  </td>
</tr>
<tr>
  <td width=50%>
  
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEmodelstyle.jpeg)
  </td>
  <td width=50%>
    <td width=50%>
  
</td>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalstyle2.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalfront.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalleft.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalback.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalright.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinaltop.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalbottom.jpeg)
    
  </td>
</tr>
</table>







## Team Photos
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/official-photos/team.jpg)
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Team_photos/workingproccess1.jpeg)
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Team_photos/workingproccess2.jpeg)
</br>
</br>
# <hr/>

<!-- 










-->
# Performance videos
### Open Challenge: https://www.youtube.com/watch?v=7BwItxD5PFI&ab_channel=QZOFlame </br>
### Obstacle Challenge: https://www.youtube.com/watch?v=Dp4Yk0vj5d8&ab_channel=QZOFlame </br>
### Robot parts discussion: https://www.youtube.com/watch?v=wA9YH8HjfyY&ab_channel=QZOFlame</br>
# <hr/>



# Code explanation
The code is written in LEGO MINDSTORMS block programming language and you can download and check it 
<a href="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Instructions/FECHALLENGE2025YA.ev3">here</a>. </br> </br>

First of all we align the steering wheels to the center, so the robot moves straightforward. Then in configuration we set app all of the variables with specific values and using the bug of LEGO MINDSTORMS we reset the values of gyro sensor. Then our programm splits into 3 streams, first for robot control, 2nd for taking the values of Pixy2 camera into variables for obstacle management and the 3rd is for taking the values of UART sensors that are LEGO sensors and using the logic to determine the line color and round direction, activating the logic flag for turn, also the PID regulator of steering control is managed. Dividing the code into 3 streams is necessary for LEGO platform because it improves data processing and optimization of the programm logic and programm operating speed and improving precisesness of data. All of the key principles are in the 1st stream. This stream used for robot control and is responsible for the aligning to the center and to detour the obstacles. After that the main stream ends a loop for 3 laps and starts the parking.


# Conclusion
## Limitations

<table>
  <tr>
    <th align = center> Mobility Management </th>
    <td> 
    <ul>
      <li> LEGO motors, sensors and P-Brick are large in comparison with other electrical components and it makes it hard to create a compact robot </li>
      <li> LEGO EV3 set have limited opportunities in terms of customizing robot itself  </li>
      <li> creating construction only by LEGO diminish </li>
    </ul>
    </td>
  </tr> 
    
  <tr>
    <th> Power and Sense Management </th>
    <td> <ul> 
      <li> 1 core CPU deprives multithreaded data processing and accuracy of sensor records. </li>
      <li> Only 4 ports for sensors and 4 ports for motors can be used. </li>
      <li> The Operating System of EV3 P-Brick is limited in functionality and flexibility. </li>
      <li> EV3 P-Brick has limited abilities in comparison with Raspberry Pi 4B that is a small computer. </li>
      <li> EV3 P-Brick is limited in source of motors and sensors since special firmware is needed for sensors and motors to interact with EV3 P-Brick. </li>
      <li> EV3 P-Brick depends on a battery too much and even slight difference potentially can trigger problems. </li>
      <li> EV3 system has stopped in updates, and have some bugs like active bluetooth mode that sometimes interferes the operation of sensors </li> 
      <li> LEGO sensors are less accurate in comparison with other available sensors </li>
    </td>
  </tr>
      
  <tr>
    <th align = center> Obstacle Management </th>
    <td> <ul>
      <li> Pixy2 camera's quality is low (1.3 megapixels) </li>
      <li> Uses I2C that limits the sensor recordings to 60 times per second and lower </li>
      <li> Outputs only specified values </li>
      <li> Strong dependence on the lighting level </li>
      <li> Unstability of run </li>
    </td>
  </tr>
</table>

## Sugestions for further development
<!-- 
Since LEGO platform have numerous limitations it would be better to switch on Raspberry Pi's newest model. Raspberry Pi is a single board computer that affords the abilities to work with electronics. The main advantages by switching on Raspberry Pi would be the ability to use AI for detecting objects, using numerous and various sensors for better power and sense and obstacle managements. For the construction making it would be better to built own construction including the aspects of mechanical engineering, especially Ackermann Steering Geometry for smooth turns. Also it would be possible to make construction smaller and aerodynamic for better control and to fit into parking lot vertically as it is easier. Wheel selection is also an important factor, as better rubber on wheels prevents their slipping making the encoder values more accurate and improves traction. The smaller wheels for steering mechanism reduces the turn radius, and big wheels on rear axle improves the speed. Gears system regulates the torque and speed. For obstacle management choosing camera with greater resolution, better resistence to light changes and using AI technologies would improve the obtacle avoidance. Using more accurate sensors with more iterations per second would improve the sense management. Motors with more torque, RPM and damage resistance would improve the power and sense management. 
-->

<table>
  <tr>
    <th align = center> Switch control-board to Raspberry Pi </th>
    <td> 
      Since LEGO platform have numerous limitations it would be better to switch on Raspberry Pi's newest models. Moreover Raspberry Pi platform is considered as single board computer that includes all of the features of personal computers such as programming flexibility, better peripherals and ability to use AI
    </td>
  </tr> 

  <tr>
    <th>
      Mobility Management
    </th>
    <td>
      Switch on own designed details and improving aerodynamics, diminishing the size. Switching the wheels such as smaller the wheels of steering mechanism the smoother are the turns and smaller the turn radius. Bigger wheels on rear axle improves the speed but reduces the torque, as well as gears mechanism the greater the speed, the smaller the torque. Also selection of wheels with better rubber will improve the traction and diminish slipping which is important for odometry base and sense management based on encoders. Also LEGO motors are fragile and can be easily damaged, so more strong motors with greater index of load condition will improve the stability of the robot.
    </td>
  </tr>
    
  <tr>
    <th> Power and Sense Management </th>
    <td> 
      Using more advanced sensors with greater accuracy level and greater number of iterations per second will improve the sense management and trajectory control. The same is for motor selection, greater speed, traction, torque and accuracy of encoder values are closely related to the motor.
    </td>
  </tr>
      
  <tr>
    <th align = center> Obstacle Management </th>
    <td> 
      Choosing camera with greater resolution, better resistence to light changes and using AI technologies would improve the obtacle detection and avoidance. 
    </td>
  </tr>
</table>

<h1>Used links</h1>

<a href="https://www.bricklink.com/catalogList.asp?catType=S&catString=166.59.800">BrickLink[1]</a> <br>
<a href="https://www.eurobricks.com/forum/index.php?/forums/topic/87670-ev3-large-and-medium-motors-comparison/">Comparison of technical specifications[2]/</a> <br>
<a href="https://www.researchgate.net/publication/345182894_Dynamic_analysis_modeling_and_control_of_the_LEGO_EV3_modular_mobile_platform">research[3]</a> <br>
<a href="https://www.youtube.com/channel/UC0_5yZ2aPdJc0X5wtIw4ZcA">"QZO Flame"[4] (tag: @QZOFlame)</a> <br>
<a href="https://pybricks.com/ev3-micropython/startbrick.html">EV3 Programmable Brick[5]</a> <br>
<a href="https://www.dexterindustries.com/ev3-current-consumption-measurement/">EV3 Current Consumption Measurement[6]</a> <br>
<a href="https://pixycam.com/downloads-pixy2/">Pixy[7]</a> <br>
<a href="https://planetcalc.com/8110/?language_select=en&ysclid=m0a3s77i4p794636345">linear function by two points[8].</a> <br>
<!-- 



# Programm Logic
First of all we align the steering wheels to the center, so the robot moves straightforward. Then in configuration we set app all of the variables with specific values and using the bug of LEGO MINDSTORMS we reset the values of gyro sensor. Then our programm splits into 3 streams, first for robot control, 2nd for taking the values of Pixy2 camera into variables for obstacle management and the 3rd is for taking the values of UART sensors that are LEGO sensors and using the logic to determine the line color and round direction, activating the logic flag for turn, also the PID regulator of steering control is managed. Dividing the code into 3 streams is necessary for LEGO platform because ..... All of the key principles are in the 1st stream. This stream used for robot control and is responsible for the aligning to the center and to detour the obstacles. After that the main stream ends a loop for 3 laps and starts the parking.

## Programm analysis


-->
<!-- # Engineering Factor
### Construction making
  For our construction we used LEGO MINDSTORMS Education Set and wheels from LEGO SPIKE Prime Set as it conducts simple platform LEGO MINDSTORMS application for code, logic and powerful UART sensors as Gyro, Ultrasonic and Colorsensor for sense management and EV3 programmable brick as a main controller. </br>

  Pixy2 camera is a powerful tool with I2C communication protocol. It is used to distinguish colors of red, green blocks and parking in obstacle challenge, their position by relative coordinates and their relative sizes. It also has its own programm <u>PixyMon v2</u> for configuration of Pixy2 camera, with interactive interface including various settings. </br>
### Programming
  For the programming we used <a href="">LEGO MINDSTORMS</a> application. 
# <hr/>
