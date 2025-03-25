# Sam's PLC Truck

## PROJECT DOCUMENTATION: RC ELECTRIC PICKUP TRUCK WITH PLC CONTROL

### PROJECT CONCEPT

Sam Walton's truck, if he were an Automation Engineer.

- 240mm x 480mm, 3D-printed body (PLA body, TPU tires)
- Allen-Bradley PLC as the primary relay/controller (Micro820 2080-LC20-20QBBR)
- Raspberry Pi Pico 2 micro controller for "special features" (blinker, sounds, other fun customizations)
- Remote-controlled with a custom-built controller (included in the box)

*This project is my application to work in this lab. Resume included in the envelope.*

---

### KEY COMPONENTS

#### 1. Programmable Logic Controller (PLC)
- **Make/Model**: Allen-Bradley Micro820 (2080-LC20-20QBBR)
- **Specs**: 24V DC, 12 digital inputs, 7 outputs, Ethernet port, compact at 90x100x80mm
- **Role**: The truck's mastermind—controls motors, steering, and more with industrial precision, proudly displayed in the bed.

#### 2. Motors
- **Make/Model**: 2 x Greartisan DC 24V 200RPM Gear Motors
- **Specs**: 200 RPM, 1.5 kg·cm torque, 24V, compact 37mm gearbox
- **Role**: Rear-wheel drive powerhouses—zippy, strong, and ready to burn rubber (or PLA).

#### 3. Battery
- **Make/Model**: Talentcell 24V 6Ah LiFePO4 Battery Pack
- **Specs**: 153.6Wh, 24-26V stable output, 2000+ cycles, lightweight at ~1.5 kg
- **Role**: The truck's juice—keeps it rolling for hours without breaking a sweat.

#### 4. 3D-Printed Components
- **Material**: PLA filament, 20% infill, black with silver accents
- **Parts**:
  - Chassis: Rugged base with mounts for PLC, battery, and motors
  - Body: Sleek pickup shell (cab + bed), 240mm x 480mm x 180mm
  - Wheels: 4 x 100mm, custom hubs for motor shafts
- **Role**: The truck's soul—beautiful, lightweight, and 100% custom.

#### 5. Remote Control
- **Make/Model**: Custom-built, based on Flysky FS-i6
- **Specs**: 6-channel, 2.4GHz, ergonomic grip, mapped to PLC inputs
- **Role**: Your keys to the kingdom—drive it, steer it, show it off.

---

### UNIQUE ASPECTS

- **PLC in the Bed**: An industrial controller in an RC truck? Hell yeah—visible and functional.
- **All 3D-Printed**: Chassis, body, wheels—crafted from scratch for max cool factor.
- **Custom Remote**: Built by hand, included in the box—total control, total flex.
- **Miniature Powerhouse**: Tiny size, massive impact—240mm x 480mm of pure engineering swagger.

---

### PROJECT GOALS

- **Speed**: Hit 0-3 mph in 2 seconds—fast enough to turn heads.
- **Runtime**: 2+ hours of driving—endurance meets elegance.
- **Looks**: So slick it could grace a magazine cover—beautiful and badass.
- **Wow Factor**: Make the lab crew fight over who gets to drive it first.

---

### CURRENT STATUS

- **Parts**: Ordered—PLC, motors, battery, remote kit, PLA filament.
- **Design**: Chassis and body 50% done in Fusion 360—sleek and sturdy.
- **Build**: Printing underway; remote assembly started.
- **Code**: PLC ladder logic in progress—motors and steering mapped.
- **Delivery Prep**: Boxed with truck, remote, and this doc—ready to drop off.

---

### OPEN QUESTIONS

- **Remote-to-PLC Link**: Controller decisions - build/buy considerations?
- **Motor Drive**: Which driver pairs best with PLC outputs and existing components?
- **Chassis Strength**: Will PLA hold up to lab shenanigans? (Reinforce how?)

---

### ENGINEERING DECISIONS

#### PLC: Allen-Bradley Micro820 (2080-LC20-20QBBR)

Learn PLC programming through industry-standard hardware/brand, and integrating custom components.

**I/O Requirements**:  
The RC truck requires precise control over two motors (for speed and direction) and a steering servo, alongside inputs from sensors like battery voltage or limit switches. The Micro820 provides 12 digital inputs and 7 digital outputs, which comfortably supports:
- 2 motors: 4 outputs total (2 per motor for speed and direction)
- 1 steering servo: 1 output (PWM signal)
- Spare I/O: Remaining inputs/outputs for remote control signals or additional sensors

Additionally, its 4 analog inputs enable real-time monitoring of battery voltage or other analog signals, enhancing system adaptability.

**Removable Terminal Blocks (RTB)**:  
We chose the 2080-LC20-20QBBR variant over alternatives like the 2080-LC20-20QBB or 2080-LC20-20QBBK due to its removable terminal blocks. This feature simplifies troubleshooting, wiring adjustments, and component replacements. For a project that may evolve or need maintenance, RTBs reduce downtime and prevent damage to the PLC during modifications.

**Additional Benefits**:  
The Micro820 includes an Ethernet port for remote programming and monitoring, aligning with modern control practices. Its two plug-in slots allow future expansion (e.g., extra I/O or communication modules) without a full redesign. Priced at ~$200, it offers industrial-grade reliability and native 24V support, outpacing hobbyist options like Arduino while staying cost-effective compared to high-end PLCs like the Siemens S7-1200.

#### Motors: 2 x Greartisan DC 24V 200RPM Gear Motors

**Rear-Wheel Drive Configuration**:  
We opted for rear-wheel drive to emulate real pickup trucks, improving traction for acceleration and delivering an authentic driving experience. This choice also simplifies the steering system, as only the front wheels need to pivot, reducing mechanical complexity.

**Two Motors (One per Rear Wheel)**:  
Using two motors—one for each rear wheel—instead of a single motor driving both offers multiple advantages:
- Simplified Mechanical Design: Each motor directly drives its wheel, eliminating the need for a differential or intricate gearing
- Torque Distribution: Splitting the load between two motors reduces strain on the drivetrain, enhancing reliability
- Flexibility: While not implemented here, this setup enables differential steering (varying motor speeds for tighter turns) if desired in future iterations

The trade-off of added cost is outweighed by the mechanical simplicity and robustness.

**24V Operation**:  
The motors' 24V rating matches the PLC and battery voltage, eliminating the need for voltage converters. This streamlines the electrical design, reduces component count, and improves efficiency.

**200 RPM Speed**:  
At 200 RPM with 100mm wheels, the truck achieves ~3.8 mph—fast enough for an engaging RC experience yet slow enough for safe, controllable operation in a lab setting. The 1.5 kg·cm torque per motor suffices for a ~5 kg truck on flat surfaces, and the compact 37mm gearbox integrates seamlessly into a 3D-printed chassis.

#### Battery: Talentcell 24V 6Ah LiFePO4 Battery Pack

**24V Nominal Voltage**:  
The 24V rating directly powers the PLC and motors without additional voltage regulation, simplifying the system and minimizing energy losses. Consistency across components reduces complexity and cost.

**6Ah Capacity**:  
Under normal operation, the PLC draws ~0.5A, and each motor draws ~0.18A (rated), totaling ~0.86A. With a 6Ah capacity, this yields ~7 hours of runtime. Even at higher loads (e.g., 1A per motor), runtime remains ~3 hours—ample for an RC truck. We chose 6Ah over a smaller 3Ah option to ensure longer playtime and accommodate potential inefficiencies or added features.

**LiFePO4 Chemistry**:  
LiFePO4 was selected for several reasons:
- Safety: Its low risk of thermal runaway or fire makes it ideal for a project handled by multiple users
- Durability: With 2000+ charge cycles, it far outlasts lead-acid (300-500 cycles) or standard lithium-ion batteries, reducing long-term costs
- Performance: It maintains a stable 24-26V output throughout most of its discharge cycle, ensuring consistent operation without extra regulation

The 10A max discharge rate exceeds the motors' estimated stall current (~2.4A total), providing reliability under peak loads.

**Trade-offs Considered**:  
Lead-acid batteries (e.g., 24V, 5Ah for $50) were cheaper but heavier (2.5 kg vs. 1.5 kg) and less durable. A 10Ah LiFePO4 ($150) offered more capacity than needed, inflating costs unnecessarily. The 6Ah LiFePO4 ($100) strikes the right balance, leaning toward higher capacity for flexibility rather than risking insufficient runtime.

#### 3D Printing
PLA—prints custom, clean, looks sharp, and keeps it DIY-cool.
