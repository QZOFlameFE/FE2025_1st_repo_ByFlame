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
<h1 align = center> Future Engineers 2026 </h1>
<h2 align = center> Team name: QYZYLORDA Flame </h2>
<h2 align = center> Team members: Sadu Yernur, Sadu Ayanur </h2>
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
<h2 align = center>Our team already participated in the 2024 and 2025 seasons, and we won second place in the FE category in 2024.</h2>
<div align = center>
<img src="https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Team_photos/2024.jpeg"/>
</div>

# Contents 
* [**Mobility and mechanical design**](#mobility-and-mechanical-design)
  * [Technical specifications and footprint constraints](#technical-specifications-and-footprint-constraints)
  * [Motor selection and actuator architecture](#motor-selection-and-actuator-architecture)
  * [Drivetrain evolution and gear ratio optimization](#drivetrain-evolution-and-gear-ratio-optimization)
  * [Steering geometry and mechanical backlash mitigation](#steering-geometry-and-mechanical-backlash-mitigation)
  * [Wheel selection and odometry accuracy](#wheel-selection-and-odometry-accuracy)
  * [Center of mass and weight distribution](#center-of-mass-and-weight-distribution)
  
* [**Power and sensor architecture**](#power-and-sensor-architecture)
  * [Power architecture and source selection](#power-architecture-and-source-selection)
  * [Power distribution architecture](#power-distribution-architecture)
  * [Sensor placement and reasoning](#sensor-placement-and-reasoning)
  * [Calibration methods](#calibration-methods)
  * [Failure cases and mitigation](#failure-cases-and-mitigation)
  * [Iteration and improvements](#iteration-and-improvements)
* [**Software Architecture and Obstacle Strategy**](#software-architecture-and-obstacle-strategy)
  * [Finite State Machine](#finite-state-machine)
  * [Kalman filter](#kalman-filter)
  * [Ultrasonic rotation control](#ultrasonic-rotation-control)
* [**Systems Thinking and Engineering Decisions**](#systems-thinking-and-engineering-decisions)
  * [System-level design constraints](#system-level-design-constraints)
  * [Trade-offs in sensor and system design](#trade-offs-in-sensor-and-system-design)
  * [Risk identification and mitigation](#risk-identification-and-mitigation)
  * [System integration rationale](system-integration-rationale)
  * [Summary of final engineering decisions](#summary-of-final-engineering-decisions)
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
# Mobility and mechanical design

![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalscheme.jpg)
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalpixyview.jpg)
<p>   Our robot is designed by lego, especially we used LEGO MINDSTORMS Education Core Set(Serial number 45544) and other LEGO EV3 sets: EV3 Expansion Set, EV3 Homeschool Combo Pack and others. You can view all of the LEGO EV3 sets by this link: <a href="https://www.bricklink.com/catalogList.asp?catType=S&catString=166.59.800">BrickLink[1]</a>. Robot's wheels are taken from LEGO SPIKE Prime set and its expansion set(serial numbers 45678-1 and  45680-1). </p> </br>

### Technical specifications and footprint constraints
<p>   The mechanical design of the robot is governed by the WRO 2026 Future Engineers guidelines, which state that the robot must first complete three laps around the course, while avoiding red and green obstacles, and then perform parallel parking. </p>  <br>

<p> In order to provide maximum mobility and avoid collisions with traffic objects, the robot was made to have the smallest possible footprint. The final dimensions are:</p>
<ul>
  <li>
    Length: 24.5 cm
  </li>
  <li>
    Width: 14.0 cm
  </li>
  <li>
    Height: 29.0 cm
  </li>
  <li>
   Total Weight: ~0.8 kg
  </li>
</ul> <br>
<p> With this structural volume kept to a minimum, there is a considerably larger clearance margin for the robot while performing a turn between two tightly-spaced pillars and successfully parking itself.</p>
<div align=center>
<table>
<tr>
<th width=250>
  
![alt text](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/concepts/parallelparkingscheme.jpeg) </br>
</th>
</tr>
</table>
</div>

### Motor selection and actuator architecture
  We have a choice between 2 types of LEGO motors: large motor and medium motor. The comparison can be viewed by this link: <a href="https://www.eurobricks.com/forum/index.php?/forums/topic/87670-ev3-large-and-medium-motors-comparison/">Comparison of technical specifications[2]/</a>. According to <a href="https://www.researchgate.net/publication/345182894_Dynamic_analysis_modeling_and_control_of_the_LEGO_EV3_modular_mobile_platform">research[3]</a> 
 
 <img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/medium%20motor.jpg width="40%">   <img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Large%20motor.jpg width="48%">
  

<p> The choice of actuators was guided by an assessment of the LEGO motor specification and performance targets defined by the research team. They needed to select between two main actuator types, namely the Large Motor and the Medium Motor.</p>

In terms of technical performance parameters, the fundamental properties of these actuators are as follows:
<table>
  <thead>
    <tr>
      <th>Technical Specification</th>
      <th>LARGE Motor (Actuator)</th>
      <th>MEDIUM-Size Motor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Maximum Operating Speed</b></td>
      <td>170 rpm</td>
      <td><b>250 rpm</b> (Higher peak velocity)</td>
    </tr>
    <tr>
      <td><b>Running Torque</b></td>
      <td>0.20 Nm</td>
      <td><b>0.08 Nm</b> (Lower baseline)</td>
    </tr>
    <tr>
      <td><b>Stall (Stopping) Torque</b></td>
      <td>0.40 Nm</td>
      <td><b>0.12 Nm</b> (Lower baseline)</td>
    </tr>
    <tr>
      <td><b>Integrated Encoder</b></td>
      <td>Yes (1° resolution, 0.001s sampling)</td>
      <td>Yes (1° resolution, 0.001s sampling)</td>
    </tr>
    <tr>
      <td><b>Form Factor / Volume</b></td>
      <td>Large, bulky housing</td>
      <td><b>Compact, space-saving design</b></td>
    </tr>
  </tbody>
</table>

#### Engineering analysis & final Selection
<p> Although the Large Motor offers better torque performance (0.20 Nm compared to 0.08 Nm), it is worth noting that the Medium Motor was used in building the whole robot because of two critical reasons identified from our study:</p>
<ul>
   <li> <b> Efficiency of Space and Collision Prevention:</b> <br> The large motor has a large casing, adding to the robot’s size. Due to the restrictions that prohibit collision with traffic pillars, which are painted red and green in the WRO 2026 contest, making the robot as small as possible was essential. The small size of the medium motor ensured that the robot would have a small footprint.</li>
   <li> <b>Speed Performance:</b> <br> The medium motor ensures 47% higher top speed operation than the large one (250 rpm vs. 170 rpm). It is crucial for winning time in the easy zones of the race track.</li>
</ul>

#### Mitigating the torque deficit via dual-motor coupling
<p>The primary risk of using the Medium Motor for the drivetrain was its low stall torque (0.12 Nm), which previously caused single-motor configurations to stall during startup.

To resolve this without reverting to the bulky Large Motor, the team engineered a **mechanically coupled dual-motor rear axle**. By synchronizing two Medium Motors into a single drive gear system, the operational torque was effectively doubled to approximately 0.16 Nm, while keeping the high 250 rpm limit and a highly compact chassis layout.

The next two medium motors are assigned to the auxiliary systems. One motor controls the steering system while the other controls the sweeping mechanism of the ultrasonic sensor placed at the front end.</p> 

### Drivetrain evolution and gear ratio optimization

There was several revisions done on the drivetrain in order to compensate the tradeoff between speed and precision:

<table>
  <thead>
    <tr>
      <th>Iteration</th>
      <th>Configuration</th>
      <th>Gear Ratio</th>
      <th>Performance Summary / Engineering Trade-off</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Version 1</b></td>
      <td>1x Medium Motor</td>
      <td>1:4 (Speed Up)</td>
      <td><b>Failure.</b> Insufficient torque. The robot failed to overcome static friction and could not consistently launch without manual assistance.</td>
    </tr>
    <tr>
      <td><b>Version 2</b></td>
      <td>2x Medium Motors</td>
      <td>1:3 (Speed Up)</td>
      <td>Optimized strictly for raw velocity during the empty track phase. High top speed but lacked fine positioning control.</td>
    </tr>
    <tr>
      <td><b>Version 3</b></td>
      <td>2x Medium Motors</td>
      <td>3:1 (Torque Multiplier)</td>
      <td>Gears reversed to maximize torque and angular resolution. Highly accurate but severely limited overall lap time.</td>
    </tr>
    <tr>
      <td><b>Version 4 (Final Design)</b></td>
      <td>2x Medium Motors</td>
      <td>(24T→8T)(20T→28T)</td>
      <td><b>Success.</b> Integrated a mechanical differential for smooth cornering. This hybrid ratio balances torque overhead via the dual-motor setup while maintaining high speed.</td>
    </tr>
  </tbody>
</table>

The drivetrain configuration went through numerous R&D iterations to address the compromise between peak linear speed and low speed accuracy.

The current Version 4 configuration employs a specially designed two-stage compound gear train in order to enhance the Medium Motor's optimal power output range:
* **First Stage (Speed Enhancer):** <br> There is a direct transmission from the 24-teeth driver gear to the 8-teeth follower gear. The $1:3$ step up provides maximum rotational speed.
* **Second Stage (Torque Compensator):** <br> The motion is conveyed by $1:1$ link to the 20-teeth gear, driving the 28-teeth gear that feeds the mechanical differential. In this way, the $20:28$ ($5:7$) step down mitigates the maximum velocity, allowing recovering mechanical torque. <br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/gear%20ratio.png width=15%> <br>

As a result of such optimization, torque consumption is balanced with physical acceleration. The average stable velocity in this case is **0.25 m/s** (1 meter per 4 seconds) in competition condition with payload. Such modification fully excludes any stress on the motor preventing heat generation.

### Steering geometry and mechanical backlash mitigation

#### Comparison between parallel steering system and Ackermann system 
The base of our chassis design comes from parallel steering model geometry. Wheels that are connected to the steering control always turn on the same angle. However, last year we used Pro-Akkerman steering model geometry. The difference is in the angle of the wheels. Pro-Akkerman makes inner wheel turn more than outer wheel, because distances that inner and outer wheels go are dissimilar(while turning). <br>
<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/concepts/akkermanangles.jpg" alt="Ackermann Design"> <br>

<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/concepts/turndistance.jpg" width="500" height="350" alt="Ackermann Design">

With a parallel steering model, the inner wheel does not align with its natural turning radius and tends to scrub against to surface, causing potential danger for the stability.
<p>Initially, the Ackermann steering system was used to provide smooth and efficient turns without slippage at high speeds. However, it was determined during tests that the Ackermann system necessitated a considerably bigger turning radius, making the robot highly vulnerable in cases where immediate and quick evasive action was necessary due to its obstacle arrangement.

To facilitate immediate direction switching, it was decided to adopt the Parallel Steering Geometry system for the chassis. Although the Parallel Steering Geometry system results in a small amount of friction for heavy vehicles, it has been shown experimentally that for such a light vehicle like this one with a mass of 0.8 kilograms, the friction is virtually non-existent. </p>

#### Backlash (Play) elimination
<p> The LEGO system, by nature, has mechanical tolerance and clearance issues . At low operating speed, the mechanical tolerance issue could be comparable to that of the steering commands itself (i.e., commanding 5 degrees but achieving 0 degree turn). </p>

This issue was solved entirely through structural component selection rather than software calibration:
* **Option A (High-Friction Black Connectors):** <br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/High-Friction%20Black%20Connectors.png width=10%> <br>
Provides rigid, zero-backlash mating but increases structural resistance, making the steering servo work harder.
* **Option B (Low-Friction Grey Pins):** <br> <img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Low-Friction%20Grey%20Pins.png width=10%> <br> Allows effortless steering rotation but introduces severe mechanical play (backlash).

**Engineering Decision:**  <br>*Option A was selected.* By eliminating mechanical play structurally, steering predictability was restored. 


### Wheel selection and odometry accuracy

<p> Wheel choice is directly linked to odometry accuracy because any slip from the wheels will result in inaccuracies from the wheel encoders that determine the location. </p> 

* **Drive Rear Axle:** <br> The robot is designed using LEGO SPIKE Prime wheels with a diameter of 5.6 cm. In previous designs, LEGO EV3 tires were used; they exhibited high coefficients of slippage when accelerating suddenly due to their design. LEGO SPIKE Prime tires are made of a unique rubber material, which provides better traction on the surface.
  * **Trade-off:** <br> Switching to 5.6 cm tires resulted in a somewhat lower theoretical maximum speed because of the wheel size, but the trade-off was made for better accuracy in tracking. <br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/LEGO%20SPIKE%20Prime%20wheels.jpg width=15%> <br>
  * **Experimental Evidence:** <br> The use of SPIKE Prime tires, compared to EV3 tires, lowered the overall drift in distance traveled from 10–15 cm to 3–5 cm over three laps.
 
* **Front Steering Axle:**  <br> Small wheels with a diameter of 2.4 cm were chosen to mount on the robot. Due to the size of the wheels and their limited angle of steering, there is no chance of contact between the tires and the sides of the chassis or the Intelligent EV3 Brick.<br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Front%20Steering%20%20wheels.png width=10%> <br>

  The explanation of our construction design is on our youtube channel <a href="https://www.youtube.com/channel/UC0_5yZ2aPdJc0X5wtIw4ZcA">"QZO Flame"[4] (tag: @QZOFlame)</a>.
   
   * [Building Instructions and BOM](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Instructions/instruction.pdf)
   * [3D model of Pixy Camera_Case](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/3D_models/README.md) <br> (used application AutoCAD)

### Center of mass and weight distribution
  The placement of heavy elements was extensively iterated to equalize the forces acting normally on both front and rear axles.

Previous designs had a heavy Intelligent EV3 Brick (275 g) located towards the back, along with the sensors. It meant that the Center of Gravity was displaced rearwards, thereby raising the front steering axle. Since the front wheels would be deprived of normal pressure, they started to slip during turning maneuvers, making the commands meaningless. Although additional weights could be installed in front for a temporary fix, it would increase the overall vehicle mass and strain the power train.

In the current design, the Intelligent EV3 Brick is moved forwards and placed above the mid-front part of the vehicle. It means that proper weight distribution allows applying enough normal force to the front tires so they can provide adequate mechanical grip when used for steering, while enough force will remain to be applied to the high-grip rear SPIKE wheels. Additional weights become unnecessary in the current configuration.
<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Vehicle_photos/FEfinalbalance.jpg" width="600">


# <hr/>

# Power and sensor architecture

### Power architecture and source selection
Powering the sub-electronics on board the robot is done only by the<a href="https://pybricks.com/ev3-micropython/startbrick.html"> **LEGO MINDSTORMS EV3 Rechargeable DC Battery Pack**</a>  (Nominal 7.4V, model number 60530) in an untouched form. The use of third-party lithium batteries or any other non-standard modifications was not considered at all for reasons of safety and durability of equipment.

Empirically measuring during track tests, it was discovered that the most optimal interval for operation in which the sensors show reliable readings and motor functions operate deterministically falls within the range of **7.6V to 8.2V**. 

The EV3 P-Brick has **4 ports for motors** and **4 ports for sensors**.  
Power consumption details for motors and sensors can be found here:  
<a href="https://www.dexterindustries.com/ev3-current-consumption-measurement/">EV3 Current Consumption Measurement[6]</a>
The calculation for power consumption is based on the standard power consumption values of the LEGO EV3 motors and sensors.
The power consumption capacity of the EV3 Large Motor can be as much as 1.6 A at maximum power while the power consumption of the EV3 Medium Motor can be as much as 0.7 A.
<br> *Detailed structural routing diagrams and current benchmarks are cataloged within our [Electrical Wiring Diagrams Portfolio](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/schemes/README.md).*

<table>
  <thead>
    <tr>
      <th>Component</th>
      <th>Quantity</th>
      <th>Current (official / estimated)</th>
      <th>System Role</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td><b>EV3 Medium Motor (rear drive)</b></td>
      <td>1</td>
      <td>Up to 0.7A</td>
      <td>Locomotion</td>
    </tr>
    <tr>
      <td><b>EV3 Medium Motor (reart drive)</b></td>
      <td>1</td>
      <td>Up to 0.7A</td>
      <td>Locomotion</td>
    </tr>
    <tr>
      <td><b>EV3 Medium Motor (steering control)</b></td>
      <td>1</td>
      <td>Up to 0.7A</td>
      <td>Directional steering system</td>
    </tr>
    <tr>
      <td><b>EV3 Medium Motor (ultrasonic rotation)</b></td>
      <td>1</td>
      <td>Up to 0.7A</td>
      <td>Environmental scanning mechanism</td>
    </tr>
    <tr>
      <td><b>EV3 Intelligent Brick</b></td>
      <td>1</td>
      <td>~0.1–0.2A</td>
      <td>Central processing unit</td>
    </tr>
    <tr>
      <td><b>Gyroscope sensor</b></td>
      <td>1</td>
      <td>~0.02A</td>
      <td>Orientation tracking</td>
    </tr>
    <tr>
      <td><b>Ultrasonic sensor</b></td>
      <td>1</td>
      <td>~0.02A</td>
      <td>Distance measurement</td>
    </tr>
    <tr>
      <td><b>Color sensor</b></td>
      <td>1</td>
      <td>~0.02A</td>
      <td>Line detection and odometry reference</td>
    </tr>
    <tr>
      <td><b>Pixy camera module</b></td>
      <td>1</td>
      <td>~0.14–0.17A</td>
      <td>Object detection system</td>
    </tr>
  </tbody>
</table>
<p>
<b>Total estimated peak current:</b> approximately 3.2 – 3.8A depending on load distribution.
</p>
<br>
Considering the potential decrease in battery voltage that may affect the repeatability of control signals of the steering controller and velocity curves, it was decided that it must be adhered to:

<table>
  <thead>
    <tr>
      <th>Operational Metric</th>
      <th>Voltage Range</th>
      <th>Engineering Impact & Strategic Mitigation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Peak Performance Window</b></td>
      <td>7.6V - 8.2V</td>
      <td>Ensures maximum torque overhead for the dual-motor rear axle and clear, stable data lines for the UART sensors.</td>
    </tr>
    <tr>
      <td><b>Voltage Drop Risk Zone</b></td>
      <td>Below 7.6V</td>
      <td>Causes inconsistent acceleration and subtle micro-steering deviations, negatively impacting dead reckoning.</td>
    </tr>
    <tr>
      <td><b>Mitigation Strategy</b></td>
      <td>Active Hot-Swapping</td>
      <td>The team uses a parallel logistics system whereby one pack drives the current vehicle, whereas a fully charged backup pack remains on standby. Once telemetry indicates that the main pack voltage falls to around 7.6 volts, it is swiftly swapped with the hot backup pack.</td>
    </tr>
  </tbody>
</table>




---

### Power distribution architecture

The power distribution is done purely using the EV3 Intelligent Brick. There is no external regulation of power as all motors and sensors are directly interfaced using EV3 standard interfaces.

System Architecture
 * Power to motors is controlled using PWM signal internally
 * Sensor data is polled using internal EV3 firmware loops
 * No external power modules

This system simplifies the system and makes it more reliable by removing potential sources of error.

---


### Sensor placement and reasoning 

* **Pixy camera:** <br> The camera called Pixy is fitted in the rear top part of the robot. This particular camera detects obstacles when the robot travels backwards. When the camera had an angle of 60°, it detected objects from outside the field, resulting in navigation problems during the 2025 national competition. The angle was then lowered to 45°.
</p>

* **Gyroscope:** <br> The gyroscope is located in an easy-to-reach position on the chassis to ensure that any repairs are easily carried out and the connection between the sensor can be rapidly made before the start of the trial. This is because this position has been selected based on its ease of use, mainly with regards to disconnection and reconnection of the sensor to ensure calibration. The position does not impact the accuracy of measurements.
   * [gyro sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/gyro_sensor.md)

* **Ultrasonic sensor:** <br> The ultrasonic sensor is mounted at the front of the robot and connected to a medium motor for rotation. This allows a single sensor to cover multiple directions (left, front, right) without increasing hardware complexity. The placement was chosen for practical reasons, mainly to keep the mechanical design simple and reduce the number of sensors needed. Using one rotating sensor also simplifies wiring and reduces calibration effort compared to using multiple fixed sensors.
  * [ultrasonic sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/ultrasonic_sensor.md)
  
* **Color sensor:** <br> The color sensor will be mounted in the middle of the robot, underneath, at the bottom. This will enable the color sensor to detect markings on the floor consistently below the robot when in motion. The central mounting of the sensor was done to facilitate odometry and line detection, making it easy to refer to the robot's position when in motion.
  * [color sensor](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/color_sensor.md) <br><br>  and other sense managements:
  * [encoders from motors](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/encoders_from_motors.md)
  * [odometry](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Power_and_Sense_Management/odometry.md)


---

### Calibration methods

Calibration for the Pixy camera is done through PixyMon, the software used on a computer to adjust the camera. The software offers many parameters to be adjusted so that we can set up the camera according to the current environment. In most cases, we test the color signature of objects and confirm if the camera can recognize red and green objects based on the current lighting conditions. Due to different lighting conditions depending on location, we do this calibration many times before every race. *Here you can see how to set up this camera* <br>
 * [Pixy2 camera's configuration](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/README.md) <br>

The calibration process for the gyroscope is done automatically during the start of every race. Through the EV3-G software, we use a reset block to set the value of the sensor to zero.

---

### Failure cases and mitigation

**Gyroscope drift** <br>
Drift in the gyroscope could be experienced in some cases when the device operates, and this would have an impact on the turning accuracy and odometry. To minimize the occurrence of drift, the gyroscope would be reinitialized at the start of each run. Additionally, different gyroscope devices were tested, and the most reliable one was used.

**Camera misdetection** <br>
Pixy camera is dependent on the calibration settings and lighting. Calibration settings that are not proper will result in the robot detecting some unnecessary objects. In the initial tests that were performed, a large camera angle helped the robot detect objects that were beyond the area of the competition. However, after several tries, the camera angle was lowered from about 60 degrees to 45 degrees.

**Voltage drop**  <br>
Low battery voltage can affect both motor performance and camera operation. Reduced brightness and unstable sensor behavior may decrease obstacle detection reliability. To avoid this, the robot is operated within a voltage range of 7.6V–8.2V, and batteries are replaced before performance degradation becomes noticeable

---

### Iteration and improvements

Many adjustments have been made along the process of testing and participating in the competitions aimed at improving reliability and avoiding unpredicted behavior.

The first major adjustment concerned the angle of installation of the Pixy camera. The camera was initially installed at an angle of about 60°, giving a very broad vision field. During the 2025 National Competition, the robot used to detect objects located outside of the competition ground and interpret it as an obstacle leading to the robot heading toward the border line.

This problem was analyzed and the camera installation angle decreased by 15° and was slightly adjusted. This way, only the visible area of the competition ground remained and the detection became more accurate.

The gyroscope was also adjusted during the design phase. Several types of sensors were tested and the one demonstrating least drift was chosen for the design in order to avoid any unpredictable changes in position.

Moreover, several actions have been undertaken to enhance the repeatability of results. The camera calibration is performed before each test and the gyroscope is reset at start-up.

---

### Wiring diagram

<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Wiring%20Diagram.png> <br>
A wiring layout for the robot is based entirely on the EV3 Intelligent Brick and its ports, in which all sensors and actuators are plugged directly into the brick's inputs and outputs.

Motor ports include the following connections:
- The rear wheel driving system uses Ports A and B. Medium Motors in this port are connected to the same shaft, thus ensuring the synchronization of rear wheels' rotations.
- Port C includes a Medium Motor that controls the rotation of the front steering wheel.
- Port D controls the rotation of an ultrasonic sensor, which allows for directional detection within the environment.

Sensor ports include the following devices:
- Port 1 includes the Pixy camera to detect objects behind the robot.
- Port 2 contains the gyroscope sensor for detecting rotational changes in the robot.
- Port 3 contains the ultrasonic sensor for distance detection in several directions.
- Port 4 contains the color sensor for line detection and odometry.

Wiring allows for proper segregation of the mechanisms used for locomotion, steering, perception, and navigation of the robot.


# <hr/>


#  Software Architecture and Obstacle Strategy
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
      
  ![linear function](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/Linear%20function%20convert.jpeg)
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

## Finite State Machine 

Robot's behavior depends on state which is determined by the input from sensors and field location.
The robot's trajectory is determined by two main situations: <br>
<ul>
  <li>
    when pixy camera sees a road sign 
  </li>
  <li>
    when pixy camera does not see road sign
  </li>
</ul> <br>

### Bypassing obstacles (when pixy camera sees a road sign (State 1)) 
We use steering mechanism and pixy2 coordinates and connect them with linear function. Y value from pixy2 gives how far the robot should be from the object, using a linear function. Using the obtained value and the real value X from pixy2, we can find an error between robot and pillar and give this error to the steering mechanism. So if the pillar is close to robot linear function gives high values to steering mechanism's motor in order to avoid crush. <br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/linear%20function.png> <br>
However, now we use a quadratic function for obstacle avoidance instead of a linear one. Unlike the linear function, which requires only two points, the quadratic function needs at least three points to define the trajectory. This allows the robot to generate a smoother path when avoiding obstacles, improving motion stability and reducing the risk of hitting pillars. In the tests that were done, the linear function was found to make the robot either scratch or move off the desired path in about 1 out of 6. However, after adopting the quadratic function, this reduced to 1 out of 15 test attempts. <br>
<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/quadratic%20function.png> <br>

https://github.com/user-attachments/assets/eb8f1eea-5bec-42ee-9bcd-57115f89046b
### Align center (when pixy camera does not see road sign (State 2))
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

### Parking position (State 3)

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

https://github.com/user-attachments/assets/bfa87282-f41e-4c83-8d34-f1d38a4ead7e

*Most tasks are performed using a pixy camera, here you can see how to set up this camera*
 * [Pixy2 camera's configuration](https://github.com/QZOFlameFE/FE2024_1st_repo_ByFlame/blob/main/Instructions/Obstacle_management/README.md)


## Kalman filter
Kalman Filter - an algorithm that uses a series of measurements observed over time, including statistical noise and other inaccuracies, to produce estimates of unknown variables that tend to be more accurate than those based on a single measurement, by estimating a joint probability distribution over the variables for each time-step. In other words, whole round lasts for a few minutes and our obstacle management works only thanks for odometry, but in the long term driving, uncertainty rises gradually and in the end it can be crucial to robots movements, that is why we need Kalman Filter, that can compensate error of odometry.

<img src="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/Uncertaintity.jpg">
In this graph you can see how error of odometry slowly rises by one minute compared to ultrasonics values. Y coordinate shows the distance between robot and outer wall. 
<div class="section">
  <h3>Kalman Filter Usage</h3>
  <p>
    How we use Kalman Filter? It compares 2 values from odometry and ultrasonic. In case difference is negligible, special coefficient <b>Trust</b> will rise. Normally it is close to 1, so robot will move and trust to Ultrasonics values, but if difference between values are too big or it changes too fast, trust will sharply decline. For example, Ultrasonic can detect the obstacle and its value will decrease, so with trusts downfall, robot will rely on Odometry system.
  </p>

  ### Previous system (Odometry correction method)

Before adopting Kalman Filter, we adopted direct correction between the values obtained from ultrasonic sensor readings and odometry values. In this case, we matched the odometry values and ultrasonic values and if their difference is less than 10, we directly applied the ultrasonic reading to correct odometry. But, in practice, this method did not work well under competition situations. Whenever the difference between ultrasonic readings and odometry readings exceeded 10, this system would yield huge errors due to accumulating odometry drift.

### Problem analysis
The first problem of the above approach is the absence of smooth changes in the level of trust.
In fact, there were only two possibilities:
* The values were similar: the direct replacement took place
* The values were different: the system became instable

Thus, the position of the robot was jumping, causing instable odometry.

### Moving towards Kalman-based system
To improve this situation, we have introduced the filter approach based on Kalman and a new dynamic parameter – Trust.
Instead of switching between the readings of the sensors, we now define the weight of each of them for the final value.
- The more similar values from ultrasonic and odometry were, the higher the level of Trust.

## Improving the obstacle avoidance function (Linear to Quadratic)

During the initial development of the obstacle avoidance program, a linear function was applied to model the avoidance process in relation to the pillars. In some cases, this led to an occurrence of sharper steering maneuvers and thus, increased the chance of hitting a pillar.
The latest implementation of the avoidance function involves the use of a quadratic equation. The use of this function has made it possible to achieve smoother steering maneuvers and avoid pillars much more effectively than before.
  
  
## Ultrasonic Rotation Control

Generally, 3 motors are sufficient for FE category robots, but we wanted to make our robot more flexible and reliable, especially in hard situations, which is why our last motor rotates the Ultrasonic sensor by 180 degrees horizontally. How does it work? If the robot moves to the pillar, which has red color, then it has to bypass it from the right side, but when moving clock wise, the Ultrasonic sensor will be pointed at the left, which is dangerous, because it may detect a pillar. As soon as Ultrasonic detects pillar, 4th motor rotates sensor till the moment it faces inner wall (bypassing pillar), like in LIDAR system.

In the previous version of our robot, we faced the problem when there was an increase in odometry error while moving and robot started to confuse objects and walls. Thus, robot could have difficulties in understanding his surrounding area.

Therefore, in order to decrease the chance of mistake, we decided to use rotating ultrasonic sensors which measure distances from clear side. <br>
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

# Systems Thinking and Engineering Decisions

## System-level design constraints

Constraints observed during robot design include:

- Processor power of the EV3 Intelligent Brick
- Limited number of sensor connections (maximum of four sensors)
- Space restrictions for motors
- Stability requirements in the duration of its run
- Dependability under changes in battery voltages

Such constraints played an important role in the design of hardware and software.

---

## Trade-offs in sensor and system design

### Ultrasonic system trade-off

A decision was made to deploy an ultrasonic sensor rather than multiple fixed sensors since the number of hardware components used would be reduced. Additionally, there will be less wiring and less of a burden on the limited ports of the EV3 brick. However, there is one drawback with this choice as one single ultrasonic sensor fixed in position cannot capture all directions of the surrounding area. This problem is solved through rotation, which can be done by the help of a Medium Motor.

---

### Pixy camera placement trade-off

In the beginning, the Pixy camera was mounted with an angle of around 60°, but that would make the robot detect objects not within the competition environment, thus making for wrong obstacle detections. It was then adjusted to an angle of around 45° because it ensures accurate field-based object detections and avoids any errors.

---

### Algorithm trade-off (Linear or Quadratic function)

Initially, we applied a linear function to our obstacle avoidance, however, we subsequently substituted the linear function with a quadratic function due to the reason that while using a linear function, abrupt movements occurred in the car; in contrast, by applying the quadratic function, we could achieve smoother movement.

---

## Iteration cycles (version development)

### Version 1
The first attempt was to employ a linear function to avoid obstacles, use a fixed ultrasonic distance measurement sensor, and set the Pixy camera viewing angle to about 60° for maximum coverage of the environment.

The first problem with this robot had issues discovered during the run test such as unsteady steering when avoiding an obstacle, recognizing objects outside the race track, and inadequate correction for odometry error that occurred after long periods. This made navigation difficult, particularly in complex areas of the racing circuit.

---

### Version 2
In the second version, several important improvements were introduced based on the issues observed in Version 1. The Pixy camera angle was reduced to approximately 45° to limit detection outside the competition field and improve focus on relevant objects. In addition, the sensor calibration procedure was refined to ensure more consistent readings under different lighting conditions and between runs. We also improved alignment using odometry to make the robot’s positioning more stable along straight sections of the track.

These changes resulted in clear performance improvements, including a significant reduction in false obstacle detections and more stable and predictable navigation behavior during full run tests.

---

### Version 3 (current system)

In the third and current version of the system, we introduced several major improvements based on the limitations observed in previous iterations. We replaced the linear obstacle avoidance approach with a quadratic function to achieve smoother steering behavior and reduce abrupt corrections when bypassing pillars. In addition, we implemented a rotating ultrasonic sensor system driven by a Medium Motor, allowing the robot to measure distances from multiple directions and improve environmental awareness, especially in situations where a fixed sensor position

---

## Risk identification and mitigation

### Risk: Odometry drift over long distance

Our first identified risk associated with our system is the problem of odometry drift. This involves increasing positioning errors that occur over time when moving at long distances. Consequently, there will be errors in the estimation of the position of the robot, particularly during long trips, where any errors can cause problems with navigation.
The following corrective measures were used to address this particular risk: a method of correcting position using gyroscopes, validating the distances using the environment via ultrasonic sensors, and an intelligent trust system like the Kalman method.

---

### Risk: Mis-detection of Camera

The major issue was the mis-detection by the camera, wherein the Pixy camera was detecting objects lying outside the perimeter of the competition field. The reason for this was largely attributed to the field of view being too large, leading to inaccurate interpretation of unrelated objects as obstacles.
In order to overcome this limitation, we limited the angle of view of the camera and calibrated it for each trial.

---

### Risk: blind spot of the ultrasonic detector

The problem that arose was ultrasonic blind spot due to the restriction of one-way distance measurement. This restriction limited the capability of the robot to detect obstacles in all important positions, potentially causing a delayed reaction or wrong movement choice when moving around.
To solve this problem, we utilized the rotating mechanism for the ultrasonic detector with the help of another Medium Motor.

---

### Risk: unstable sensor fusion
The main problem identified was instability in sensor fusion, where there was a mismatch between ultrasonic sensor readings and odometry data. This inconsistency could lead to incorrect position estimation, especially when both systems produced conflicting information during dynamic movement or in areas with accumulated odometry drift.
To mitigate this issue, we implemented a trust-based Kalman-inspired weighting system. This system dynamically adjusts the influence of each sensor based on their agreement level: when both measurements are close, the system increases trust in ultrasonic data, and when the difference becomes large or unstable, it reduces its weight and relies more on odometry. This adaptive balancing improves robustness and overall navigation reliability.

---

## System integration rationale

<img src=https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/schemes/sensor%20fusion%20diagram.png>

The robot is conceived as an integrated system such that:

- The Pixy camera is responsible for obstacle detection
- The ultrasonic sensor performs distance validation as well as navigation
- The gyroscope balances orientation
- The encoder performs odometry tracking
- The software-based FSM controls state change behavior.

All systems are connected to each other.
---

## Summary of final engineering decisions

We have adopted a multi-sensor fusion design rather than depending on one navigation approach since there is not any sensor which can be trusted completely while competing.
All of the systems complement the deficiencies of each other; therefore, their performance becomes more consistent and reliable. On 10 consecutive trials of the complete race (including three laps as well as parking maneuvers), the robot accomplished a successful completion of the race without touching in 9 out of 10 tries (90% success rate), averaging 26 seconds per lap.

# <hr/>

# Reproducibility and GitHub Quality

Our GitHub repository is structured in a way to make the project simple, understandable, and extendable. It includes the entire source code, documentation, circuit diagrams, and everything else needed in order to make our robot.
The repository is designed in such a way that any other teams, judges, or future contributors will be able to understand how the robot was made and how its software works. All the major changes that were introduced to the project were tracked via commits to demonstrate its progression.
The README file contains all the information about the project structure and is aimed at giving necessary details for the analysis of the robot's performance.

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
  
</td>
      <td width=50%>
        
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
![alt text](https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Team_photos/team%20photo%20together.jpeg)
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
### Robot parts discussion: https://youtu.be/EO1Ps9sOk3s</br>
# <hr/>


# Code explanation
The code is written in LEGO MINDSTORMS block programming language and you can download and check it 
<a href="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/tree/main/Instructions">here</a>. </br>
You can also download the previous version of the code, compare it with the new one, and follow our progress.</br>
<a href="https://github.com/QZOFlameFE/FE2025_1st_repo_ByFlame/blob/main/Instructions/FECHALLENGE2025YA.ev3">previous code</a> <br> <br>

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
