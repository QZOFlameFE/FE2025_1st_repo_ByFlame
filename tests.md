# Robot Engineering Tests and Configuration Optimizations

This document details the structured testing, experimental setups, and empirical engineering decisions made during the iteration cycles of our competition robot.

---

## Test 1: Steering Geometry
### Objective
To determine the optimal steering geometry configuration that minimizes the robot's turning radius and mitigates physical trajectory errors caused by mechanical play (backlash/люфт) in the steering hub assembly.

### Configurations Tested
* **Pro-Ackermann Steering Geometry:** The inner wheel turns at a sharper angle than the outer wheel to accommodate dissimilar turning radii.
* **Parallel Steering Geometry:** Both steered wheels maintain identical turning angles throughout the entire steering range.

### Problem Observed
* **The Pro-Ackermann System** provided smooth, slippage-free cornering at high speeds, but it drastically increased the robot's minimum turning radius. This made the vehicle highly vulnerable and slow when executing the immediate, sharp evasive actions required to bypass close-proximity obstacle pillars.
* **The Parallel Steering System** theoretically causes the inner wheel to scrub against the surface because it does not align perfectly with its natural turning radius, creating potential instability in heavier vehicle designs.

### Final Decision
Adopted the **Parallel Steering Geometry** system to achieve tight, immediate direction switching capabilities.

### Result
* Drastically reduced the turning radius, enabling rapid and responsive obstacle avoidance maneuvers.
* Experimental testing proved that for this lightweight $0.8\text{ kg}$ chassis, the tire scrubbing friction typical of parallel systems is virtually non-existent and does not degrade battery performance or surface grip.


---

## Test 2: Rear Axle Powertrain & Gear Ratio Optimization

### Objective
To resolve the critical engineering trade-off between peak linear speed and low-speed positional accuracy while ensuring sufficient mechanical torque to overcome static friction.

### Configurations Tested
* **Version 1:** Single Medium Motor with a $1:4$ speed-up gear ratio.
* **Version 2:** Dual Medium Motors with a $1:3$ speed-up gear ratio.
* **Version 3:** Dual Medium Motors with a $3:1$ torque multiplier ratio (reversed gears).
* **Version 4 (Final Design):** Dual Medium Motors coupled with a two-stage compound gear train integrated into a mechanical differential.

### Problem Observed
* **Version 1** suffered from severe torque starvation; the single motor could not overcome static friction and failed to launch without manual assistance. 
* **Version 2** achieved high top speeds but lacked the fine positioning resolution required for precise obstacle avoidance.
* **Version 3** provided excellent accuracy and torque overhead but severely limited the robot's linear velocity, resulting in uncompetitive lap times.

### Final Decision
Implemented **Version 4**, combining two Medium Motors locked onto a shared powertrain driving a two-stage compound gear train:
1.  **First Stage (Speed Enhancer):** A $24\text{T}$ driver gear meshes into an $8\text{T}$ follower gear ($1:3$ step-up) to maximize rotational velocity.
2.  **Second Stage (Torque Compensator):** Power transfers to a $20\text{T}$ gear driving a $28\text{T}$ gear ($5:7$ step-down) feeding into the mechanical differential, recovering essential torque and dampening velocity fluctuations.

### Result
* Achieved an optimal balance between physical acceleration and torque overhead.
* Maintained a highly stable average velocity of $0.25\text{ m/s}$ ($1\text{ meter per 4 seconds}$) under full competition payload conditions.
* Eliminated mechanical stress and excessive heat generation within the EV3 Medium Motors, preventing thermal degradation during prolonged runs.
* Smoother cornering dynamics due to the integration of the mechanical differential.
---

## Test 3: Wheel Selection & Odometry Accuracy

### Objective
To minimize sudden acceleration slippage and decrease cumulative distance tracking errors (drift) through empirical tire compound and diameter optimization.

### Configurations Tested
* **Configuration A (LEGO EV3 Wheels):** Standard high-profile tires utilized on the drive rear axle.
* **Configuration B (LEGO SPIKE Prime Wheels):** Medium-profile $5.6\text{ cm}$ diameter tires engineered with a high-traction rubber compound.

### Problem Observed
* **Configuration A (EV3 Tires)** exhibited low surface grip and a high coefficient of slippage during rapid acceleration phases. This wheel slip corrupted the internal motor encoder data, generating severe odometry positioning errors.
* **Front Axle Clearence:** Oversized or poorly positioned front wheels risked physical contact with the robot chassis or the EV3 Intelligent Brick during sharp steering adjustments, causing structural jamming.

### Final Decision
Selected **Configuration B (LEGO SPIKE Prime Wheels)** for the main drive rear axle to optimize surface traction. For the front steering axle, small wheels with a diameter of $2.4\text{ cm}$ were chosen to ensure zero physical contact with the chassis or wiring harnesses, even at maximum steering angles.

### Result
* **Drift Reduction:** Experimental testing over a 3-lap run proved that SPIKE Prime tires drastically reduced cumulative distance drift from **10–15 cm down to just 3–5 cm**.
* **Speed vs. Precision Trade-off:** While the smaller $5.6\text{ cm}$ diameter slightly reduced the theoretical maximum top speed compared to larger wheels, it delivered a net positive gain in dead reckoning and path tracking accuracy.
* **Zero Mechanical Jamming:** The $2.4\text{ cm}$ front wheel configuration guaranteed clean clearance profiles, allowing unhindered execution of the quadratic steering curves.

---

## Test 4: Pixy2 Camera Field of View (FOV) Adjustments

### Objective
To isolate obstacle detection strictly to active competition zones and completely filter out out-of-bounds (OOB) visual noise.

### Configurations Tested
- Wide perspective camera pitch: $60^\circ$ mounting angle
- Restricted perspective camera pitch: $45^\circ$ mounting angle

### Problem Observed
At a $60^\circ$ installation angle, the Pixy2 camera's vertical and horizontal field of view captured objects, judges, and barriers located entirely outside the official perimeter during the 2025 National Competition, triggering false-positive obstacle avoidance subroutines.

### Final Decision
Reduced the physical camera mount angle precisely by $15^\circ$, setting the permanent mechanical lock at $45^\circ$, and paired it with mandatory environmental signature testing via PixyMon before every heat.

### Result
- Field of view restricted entirely to the active competition floor.
- $0\%$ false-positive detections from out-of-bounds external elements.
- Clean color signature processing for red and green pillars under variable arena lighting.

---

## Test 5: Steering Hub Assembly & Backlash Elimination

### Objective
To eliminate physical mechanical tolerance and clearance issues within the steering hub assembly that degrade directional repeatability and compromise low-speed steering accuracy.

### Configurations Tested
* **Option A (High-Friction Black Connectors):** Rigid structural pins utilized to create tight, zero-backlash mechanical joints.
* **Option B (Low-Friction Grey Pins):** Standard smooth structural pins utilized to enable effortless steering rotation.

### Problem Observed
* The LEGO building system naturally introduces mechanical tolerances and clearances. At low operating speeds, this play was comparable to the steering commands themselves (e.g., commanding a $5^\circ$ wheel angle resulted in a $0^\circ$ physical turn due to the loose coupling).
* **Option B** allowed for effortless rotation with low power consumption but introduced severe mechanical play, making precise odometry and line-tracking impossible over long distances.
* **Option A** successfully eliminated physical play but increased rotational structural resistance, forcing the steering servo motor (Port C) to work harder and draw more current.

### Final Decision
Selected **Option A (High-Friction Black Connectors)**. A purely mechanical and structural solution was chosen over software calibration to restore physical predictability. To offset the increased structural resistance on the servo motor, the chassis weight was kept optimized at $0.8\text{ kg}$, and the battery voltage threshold was maintained strictly between $7.6\text{V} - 8.2\text{V}$.

### Result
* Completely eliminated low-speed steering dead zones ($5^\circ$ command now yields a precise $5^\circ$ mechanical response).
* Restored steering path predictability, directly reducing cumulative tracking errors in the odometry subroutines.
* Achieved high steering repeatability without relying on complex, processing-heavy software compensation loops on the EV3 Intelligent Brick.
