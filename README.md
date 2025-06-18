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
  * [Chassis design and differential](#chassis-design-and-differential)
  * [Weight distribution](#weight-distribution)
  * [Camera position](#camera-position)
  * [Motor selection](#motor-selection)
* [**Power and sense management**](#power-and-sense-management)
  * [Power management](#power-management)
  * [Sense management](#sense-management)
* [**Obstacle management**](#obstacle-management)
  * [Change of the driving direction](#change-of-the-driving-direction)
  * [Parking pasition](#parking-position)
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

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudiostyleelements.jpg)
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudioview.jpg)
<p>   Our robot is designed by lego, especially we used LEGO MINDSTORMS Education Core Set(Serial number 45544) and other LEGO EV3 sets: EV3 Expansion Set, EV3 Homeschool Combo Pack and others. You can view all of the LEGO EV3 sets by this link: <a href="https://www.bricklink.com/catalogList.asp?catType=S&catString=166.59.800">https://www.bricklink.com/catalogList.asp?catType=S&catString=166.59.800</a>. Robot's wheels are taken from LEGO SPIKE Prime set and its expansion set(serial numbers 45678-1 and  45680-1). </p> </br>
  
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

### Chassis design and differential
The base of our chassis design comes from Ackerman steering model geometry. It improves maintainabiity of the robot as it controls the smoothness of the turns because of the maximum degrees of the steering can move
We have a differential in driving rear axle of our robot to make turns smoother. If robot turns one wheel will move slower than second and it reduces radius of the turn so our robot turn is controlled by 2 mechanisms: steering mechanism and differential.
<img src="https://raw.githubusercontent.com/QZOFlameFE/FE2024_1st_repo_ByFlame/main/concepts/Ackermann_simple_design.png" width="300" height="400" alt="Ackermann Design">
### Weight distribution
  As our robot is a self-driving car with steering mechanism and differential in rear axle we need to make our robot slight heavy, and distribute weight a bit behind the center of our robot to prevent the wheels from slipping. The slipping of the wheels in rear axle impacts our odometry and the programm.Also, we placed the EV3 P-Brick in the center of the robot to distribute the weight evenly, as the brick is a relatively heavy component(275g). Pixy camera is located quite behind the robot,that's why it don't maintain balance. To maintain balance, we used metal balls(you can see from instruction of our robot) from the Lego set and placed them in front of the robot. This way, we avoid the robot from wobbling.
  
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
  We have a choice between 2 types of LEGO motors: large motor and medium motor, the large motor is powerful but the speed is lower, the medium motor is not that powerful but have a great speed. The comparison can be viewed by this link: <a href="https://www.eurobricks.com/forum/index.php?/forums/topic/87670-ev3-large-and-medium-motors-comparison/">https://www.eurobricks.com/forum/index.php?/forums/topic/87670-ev3-large-and-medium-motors-comparison/</a>. According to <a href="https://www.researchgate.net/publication/345182894_Dynamic_analysis_modeling_and_control_of_the_LEGO_EV3_modular_mobile_platform">research:</a> 

* Large servo motor (actuator) - maximum operating speed of 170 rpm, torque of 0.2 Nm and stopping torque of 0.4 Nm. It is positioned in the engine case an integrated encoder, a rotation meter, whose step is 1 degree of rotation and least sampling time 0.001 s.Also the power and speed is regulated by gear wheels and the size of the wheels. We choosed smaller wheels in steering mechanism because they do not move the robot, the only moves its trajectory.
* Medium-size servo motor - maximum speed of 250 rpm, running torque 0.08 Nm and stopping torque of 0.12 Nm, also with integrated encoder, identical to that of a large engine.
</br>
Also the wheels have low coefficient of friction to avoid loss of energy, but for wheels in the rear axles it will be better to choose wheels with a bit high cofficient of friction to avoid slipping of wheels. The rear wheels are bigger than wheels in front axle to have a better stability, movement control and the speed. It will be better to choose little smaller rear wheels than our. 
</br>
  The explanation of our construction design is on our youtube channel <a href="https://www.youtube.com/channel/UC0_5yZ2aPdJc0X5wtIw4ZcA">"QZO Flame" (tag: @QZOFlame)</a>.
   
   * [Building Instructions and BOM](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Builiding_Instructions/README.md)
   * [3D model of Pixy Camera_Case](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/3D_models/README.md) <br> (used application AutoCAD)
# <hr/>

# Power and sense management 

</br>

## Power management

</br>

  The core of our robot is <a href="https://pybricks.com/ev3-micropython/startbrick.html">EV3 Programmable Brick</a>, the power comes from a rechargable 10V Lithium Battery. EV3 P-Brick have 4 ports for motors and 4 ports for sensors.  Power consumption of motors and sensors: <a href="https://www.dexterindustries.com/ev3-current-consumption-measurement/">https://www.dexterindustries.com/ev3-current-consumption-measurement/</a>.
  <table>
<tr>
<th width=400>
  
  ![EV3 with ports for sensors and motors](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/EV3_P-Brick_demonstration.jpg)
</th>
</tr>
</table>

  * [Electroschemes/wiring diagrams](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/schemes/README.md)

    ## Why did we choose EV3 P-Brick?
    <ul>
    <li font size="10">EASY TO USE</li> <br>
    The EV3 comes with graphical programming environment (LEGO Mindstorms EV3 software), and it makes it much easier. This visual approach is more accessible than writing code in languages like C++ (Arduino) or Python (Raspberry Pi).<br> <br><br>
    <li>INTEGRATED HARDWARE</li> <br>
    EV3 comes with specialized LEGO motors and sensors (like color, infrared, and gyro), which are easy to connect and calibrate.<br> <br><br>
    <li>PORTABILITY</li>
    <br>
    EV3 is more portable and compact,because it is designed for easy handling, and its components are built with the purpose of being assembled and taken apart for quick project changes. <br> <br><br>
 
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
  UART sensors of LEGO EDUCATION MINDSTORMS EV3 Core Set such as color, ultrasonic and gyro sensors are used for sense management of our robot. </br>
  Gyro sensor is used to save initial robot position in degrees and count the deviation from it. Ultrasonic sensor measures the distance from robot to wall. Color sensor is used to know the driving direction of the round. Encoders in medium motors are used to know the distance that robot moved. Our programm uses mix of this sensors to create the odometry of our robot, by the usage of encoders, gyro sensor and Pythagoras theorem we calculate the displacement that robot moves from initial positions and convert it to x and y coordinates. Before the first line in first lap the odometry is relative to the robot's initial position and after the color sensor views the line it recognizes robot direction and by specific math formulas it converts relative odometry to full odometry of the map, the center of the map is the center of odometry where x and y coordinates are equal to zero. Ultrasonic sensor and Gyro sensor in combine used to fix odometry also by Pythagoras theorem and exceptions for the situations when ultrasonic sensor view blocks. The detailed info is given by this links related to each sensor's purpose.
  
  * [color sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/color_sensor.md)
  * [ultrasonic sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/ultrasonic_sensor.md)
  * [gyro sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/gyro_sensor.md)
  * [encoders from motors](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/encoders_from_motors.md)
  * [odometry](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/odometry.md)
# <hr/>
<!-- 

























-->
# Obstacle management
  For the obstacle detection we used Pixy2 camera and PixyMon v2 application to configure it. To use it in LEGO MINDSTORMS application you need to install special library. All of the downloads are able in official site of Pixy2 <a href="https://pixycam.com/downloads-pixy2/">https://pixycam.com/downloads-pixy2/</a>.We get x y coordinates from the Pixy camera by placing the robot on two points along the correct trajectory of robot (If the pillar is red, it should go around on the right, if it is green, on the left).From the obtained value (x,y coordinates) we calculate a quadratic function by two points (you can calculate it by the link:) <a href="https://planetcalc.com/8110/?language_select=en&ysclid=m0a3s77i4p794636345">linear function by two points. Every straightforward section has its own coordinate center and 6  possible locations of pillars. Robot changes its odometry coordinate when he passes second line(blue or orange, depends on a direction). Corner sections do not include odometry system.</a>
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
We use steering mechanism and pixy2 coordinates and connect them with linear function. Y value from pixy2 gives how far the robot should be from the object, using a quadtratic function. Using the obtained value and the real value X from pixy2, we can find an error between robot and pillar and give this error to the steering mechanism. So if the pillar is close to robot linear function gives high values to steering mechanism's motor in order to avoid crush. <br>

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

# <hr/>

# Pictures
### Robot photos

<table>
<tr>
  <th width=50%>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudiofront.jpeg)
  </th>
  <th width=50%>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudioleft.jpeg)
  </th>
</tr>
<tr>
  <td width=50%>
    
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudioright.jpeg)
  </td>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudioback.jpeg)
  </td>
</tr>
<tr>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudiobottom.jpeg)
  </td>
  <td width=50%>

![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudiotop.jpeg)
  </td>
</tr>
<tr>
  <td width=50%>
  
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/FEstudiostyle.jpeg)
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlamestyle.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlamefront.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlameleft.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlameback.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlameright.jpeg)
    
  </td>
</tr>
<tr>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlametop.jpeg)
    
  </td>
  <td width=50%>
    
  ![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Vehicle_photos/QZOFlamebottom.jpeg)
    
  </td>
</tr>
</table>







## Team Photos
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/official-photos/team.jpg)
</br>
</br>
# <hr/>

<!-- 










-->
# Performance videos
### Open Challenge: https://youtu.be/7BwItxD5PFI?si=vPpkhWuJryeI7OkL </br>
### Obstacle Challenge: https://youtu.be/Dp4Yk0vj5d8?si=MA80an7itmxMNDKA </br>
### Robot parts discussion: https://youtu.be/wA9YH8HjfyY?si=rLYR0J1qxFrNzICX </br>
# <hr/>



# Code explanation
The code is written in LEGO MINDSTORMS block programming language and you can download and check it 
<a href="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/programms/Second%20version%20of%20programm.ev3">here</a>. </br> </br>

First of all we align the steering wheels to the center, so the robot moves straightforward. Then in configuration we set app all of the variables with specific values and using the bug of LEGO MINDSTORMS we reset the values of gyro sensor. Then our programm splits into 3 streams, first for robot control, 2nd for taking the values of Pixy2 camera into variables for obstacle management and the 3rd is for taking the values of UART sensors that are LEGO sensors and using the logic to determine the line color and round direction, activating the logic flag for turn, also the PID regulator of steering control is managed. Dividing the code into 3 streams is necessary for LEGO platform because it improves data processing and optimization of the programm logic and programm operating speed and improving precisesness of data. All of the key principles are in the 1st stream. This stream used for robot control and is responsible for the aligning to the center and to detour the obstacles. After that the main stream ends a loop for 3 laps and starts the parking.


# Conclusion
## Limitations

<table>
  <tr>
    <th align = center> Mobility Management </th>
    <td> 
    <ul>
      <li> LEGO motors, sensors and P-Brick are large in comparison with other electrical components </li>
      <li> LEGO EV3 set have limited opportunities like it is impossible to make Ackermann steering control geometry </li>
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
      <li> EV3 P-Brick have limited abilities in comparison with Raspberry Pi 4B that is a small computer. </li>
      <li> EV3 P-Brick is limited in source of motors and sensors since special firmware is needed for sensors and motors to interact with EV3 P-Brick. </li>
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
      Switch on own designed details and improving aerodynamics, diminishing the size, creating great  Ackermann Steering Geometry for smooth turns. Switching the wheels such as smaller the wheels of steering mechanism the smoother are the turns and smaller the turn radius. Bigger wheels on rear axle improves the speed but reduces the torque, as well as gears mechanism the greater the speed, the smaller the torque. Also selection of wheels with better rubber will improve the traction and diminish slipping which is important for odometry base and sense management based on encoders. Also LEGO motors are fragile and can be easily damaged, so more strong motors with greater index of load condition will improve the stability of the robot.
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
