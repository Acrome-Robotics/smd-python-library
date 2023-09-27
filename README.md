# Overview
This library provides easy-to-use Python modules and methods for interfacing with Acrome Smart Motor Driver products.

Embrace the world of motor control with simplicity using our SMD Python Library. Designed specifically for controlling SMDs, this library provides a seamless experience no matter your skill level in how you control motors.

Whether your project requires basic speed adjustments or precise position control, quickly and easily leverage the flexibility of Python to effortlessly implement a wide variety of motor control strategies.

SMD Python Library takes your projects to the next level by offering seamless integration ith SMD Sensor modules. With this library, you can increase the functionality and efficiency of your project bwy effortlessly collecting data from SMD sensor modules via SMD.

Develop your projects with "Acrome Smart Motor Drivers" and a computer that can run your Python code.

You can reach the Acrome Smart Motors Drivers documentation [here](https://acrome-smd.readthedocs.io/en/latest/getting-started.html).

# Installation

To use [Acrome Smart Motor Drivers](https://acrome.net/product/smart-motor-drivers) with python library, follow the installation steps below. Library is compatible with Python 3.x and can be installed on both Windows and Linux systems.

### Prerequisites

Before you begin, make sure you have the following prerequisites:

- Python 3.x: [Python Official Website](https://www.python.org/downloads/)

### Installation

#### Windows

1. Open a Command Prompt with administrative privileges.

2. Install SMD library using `pip` (Python package manager) by running the following command:

  ```shell
  pip install acrome-smd
  ```

3. Wait for the installation to complete. Pip will automatically download and install the library along with any required dependencies.

#### Linux
1. Open a terminal.

2. Install SMD library using pip (Python package manager) by running the following command:

  ```shell
  pip install acrome-smd
  ```

3. Wait for the installation to complete. Pip will automatically download and install SMD Library along with any required dependencies.

### Verification
To verify that SMD library has been successfully installed, open a Python interpreter and run the following command:

```python
import smd
import smd.red
```
If no errors are raised, the installation was successful.

### Upgrading
To upgrade SMD Library to the latest version, you can use the following pip command:

  ```shell
  pip install acrome-smd
  ```


## Usage


## Methods

- ### Red Class
  Methods of the `Red` class are used for the underlying logic of the Master class. As such, it is not recommended for users to call `Red` class methods explicitly. Users may create instances of the class in order to attach to the master. Thus, only `__init__` constructor is given here.

  - #### `__init__(self, ID: int)`:

    This is the initalizer for Red class which represents an object of SMD (Smart Motor Drivers) driver.

    `ID` argument is the device ID of the created driver.

- ### Master Class

  - #### `__init__(self, portname, baudrate=115200)`

    **`Return:`** *None*

    This is the initializer for Master class which controls the serial bus.

    `portname` argument is the serial/COM port of the host computer which is connected to the Acrome Smart Motor Drivers via Mastercard.

    `baudrate` argument specifies the baudrate of the serial port. User may change this value to something between 3.053 KBits/s and 12.5 MBits/s. However, it is up to the user to select a value which is supported by the user's host computer.

  - #### `update_driver_baudrate(self, id: int, br: int):`

    **`Return:`** *None*

    This method updates the baudrate of the driver, saves it to EEPROM and resets the driver board. Once the board is up again, the new baudrate is applied.

    `id` argument is the device ID of the connected driver.

    `br` argument is the user entered baudrate value. This value must be between 3.053 KBits/s and 12.5 MBits/s.

  - #### `update_master_baudrate(self, br: int):`

    **`Return:`** *None*

    This method updates the baudrate of the host computer's serial port and should be called after changing the baudrate of the driver board to sustain connection.

    `br` argument is the user entered baudrate value. This value must be between 3.053 KBits/s and 12.5 MBits/s.

  - #### `attach(self, driver: Red):`

    **`Return:`** *None*

    This method attaches an instance of Red class to the master. If a device ID is not attached to the master beforehand, methods of the master class will not work on the given device ID.

    `driver` argument is an instance of the Red class. Argument must be an instance with a valid device ID.


  - #### `detach(self, id: int):`

    **`Return:`** *None*

    This method removes the driver with the given devic ID from thee master. Any future action to the removed device ID will fail unless it is re-attached.

  - #### `set_variables(self, id: int, idx_val_pairs=[], ack=False)`

    **`Return:`** *List of the acknowledged variables or None*

    This method updates the variables of the driver board with respect to given index/value pairs.

    `id` argument is the device ID of the connected driver.

    `idx_val_pairs` argument is a list, consisting of lists of parameter indexes and their value correspondents.

  - #### `get_variables(self, id: int, index_list: list)`

    **`Return:`** *List of the read variables or None*

    This method reads the variables of the driver board with respect to given index list.

    `id` argument is the device ID of the connected driver.

    `index_list` argument is a list with every element is a parameter index intended to read.

  - #### `set_variables_sync(self, index: Index, id_val_pairs=[])`

    **`Return:`** *List of the read variables or None*

    This method updates a specific variable of the  multiple driver boards at once.

    `index` argument is the parameter to be updated.

    `id_val_pairs` argument is a list, consisting of lists of device IDs and the desired parameter value correspondents.

  - #### `scan(self)`

    **`Return:`** *List of the connected driver device IDs.*

    This method scans the serial port, detects and returns the connected drivers.

  - #### `reboot(self, id: int)`

    **`Return:`** *None*

    This method reboots the driver with given ID. Any runtime parameter or configuration which is not saved to EEPROM is lost after a reboot. EEPROM retains itself.

    `id` argument is the device ID of the connected driver.

  - #### `factory_reset(self, id: int)`

    **`Return:`** *None*

    This method clears the EEPROM config of the driver and restores it to factory defaults.
    
    `id` argument is the device ID of the connected driver.

  - #### `eeprom_write(self, id: int, ack=False)`

    **`Return:`** *None*

    This method clears the EEPROM config of the driver and restores it to factory defaults.
    
    `id` argument is the device ID of the connected driver.

  - #### `ping(self, id: int)`

    **`Return:`** *True or False*

    This method sends a ping package to the driver and returns `True` if it receives an acknowledge otherwise `False`.
    
    `id` argument is the device ID of the connected driver.

  - #### `reset_encoder(self, id: int)`

    **`Return:`** *None*
    
    This method resets the encoder counter to zero.

    `id` argument is the device ID of the connected driver.

  - #### `scan_sensors(self, id: int)`

    **`Return:`** *List of connected sensors*
    
    This method scans and returns the sensor IDs which are currently connected to a driver.

    `id` argument is the device ID of the connected driver.

  - #### `enter_bootloader(self, id: int)`

    **`Return:`** *None*
    
    This method puts the driver into bootloader. After a call to this function, firmware of the driver can be updated with a valid binary or hex file. To exit the bootloader, unplug - plug the driver from power or press the reset button.

    `id` argument is the device ID of the connected driver.

  - #### `get_driver_info(self, id: int)`

    **`Return:`** *Dictionary containing version info*
    
    This method reads the hardware and software versions of the driver and returns as a dictionary.

    `id` argument is the device ID of the connected driver.
    
  - #### `update_driver_id(self, id: int, id_new: int)`

    **`Return:`** *None*
    
    This method updates the device ID of the driver temporarily. `eeprom_write(self, id:int)` method must be called to register the new device ID.

    `id` argument is the device ID of the connected driver.

    `id_new` argument is the new intended device ID of the connected driver.

  - #### `enable_torque(self, id: int, en: bool)`

    **`Return:`** *None*

    This method enables or disables power to the motor which is connected to the driver.

    `id` argument is the device ID of the connected driver.

    `en` argument is a boolean. `True` enables the torque while False `disables`.

  - #### `pid_tuner(self, id: int)`

    **`Return:`** *None*

    This method starts a PID tuning process. Shaft CPR and RPM values **must** be configured beforehand. If CPR and RPM values are not configured, motors will not spin.

    `id` argument is the device ID of the connected driver.

  - #### `set_operation_mode(self, id: int, mode: OperationMode)`

    **`Return:`** *None*

    This method sets the operation mode of the driver. Operation mode may be one of the following: `OperationMode.PWM`, `OperationMode.Position`, `OperationMode.Velocity`, `OperationMode.Torque`.

    `id` argument is the device ID of the connected driver.

  - #### `get_operation_mode(self, id: int)`

    **`Return:`** *Operation mode of the driver*

    This method gets the current operation mode from the driver.

    `id` argument is the device ID of the connected driver.

  - #### `set_shaft_cpr(self, id: int, cpr: float)`

    **`Return:`** *None*

    This method sets the count per revolution (CPR) of the motor output shaft.

    `id` argument is the device ID of the connected driver.

    `cpr` argument is the CPR value of the output shaft

  - #### `set_shaft_rpm(self, id: int, rpm: float)`

    **`Return:`** *None*

    This method sets the revolution per minute (RPM) value of the output shaft at 12V rating.

    `id` argument is the device ID of the connected driver.

    `rpm` argument is the RPM value of the output shaft at 12V

  - #### `set_user_indicator(self, id: int)`

    **`Return:`** *None*

    This method sets the user indicator color on the RGB LED for 5 seconds. The user indicator color is cyan.

    `id` argument is the device ID of the connected driver.

  - #### `set_position_limits(self, id: int, plmin: int, plmax: int)`

    **`Return:`** *None*

    This method sets the position limits of the motor in terms of encoder ticks. Default for min is -2,147,483,648 and for max is 2,147,483,647. The torque is disabled if the value is exceeded so a tolerence factor should be taken into consideration when setting these values.

    `id` argument is the device ID of the connected driver.

    `plmin` argument is the minimum position limit.

    `plmax` argument is the maximum position limit.


  - #### `get_position_limits(self, id: int)`

    **`Return:`** *Min and max position limits*

    This method gets the position limits of the motor in terms of encoder ticks.

    `id` argument is the device ID of the connected driver.

    `plmin` argument is the minimum position limit.

    `plmax` argument is the maximum position limit.


  - #### `set_torque_limit(self, id: int, tl: int)`

    **`Return:`** *None*

    This method sets the torque limit of the driver in terms of milliamps (mA).

    `id` argument is the device ID of the connected driver.

    `tl` argument is the new torque limit (mA).


  - #### `get_torque_limit(self, id: int)`

    **`Return:`** *Torque limit (mA)*

    This method gets the torque limit from the driver in terms of milliamps (mA).

    `id` argument is the device ID of the connected driver.

  - #### `set_velocity_limit(self, id: int, vl: int)`

    **`Return:`** *None*

    This method sets the velocity limit for the motor output shaft in terms of RPM. The velocity limit applies only in velocity mode. Default velocity limit is 65535.

    `id` argument is the device ID of the connected driver.

    `vl` argument is the new velocity limit (RPM).

  - #### `get_velocity_limit(self, id: int)`

    **`Return:`** *Velocity limit*

    This method gets the velocity limit from the driver in terms of RPM.

    `id` argument is the device ID of the connected driver.


  - ####  `set_position(self, id: int, sp: int)`

    **`Return:`** *None*

      This method sets the desired setpoint for the position control in terms of encoder ticks.

      `id` argument is the device ID of the driver.

      `sp` argument is the position control setpoint.


  - ####  `get_position(self, id: int)`

    **`Return:`** *Current position of the motor shaft*

      This method gets the current position of the motor from the driver in terms of encoder ticks.

      `id` argument is the device ID of the driver.

  - ####  `set_velocity(self, id: int, sp: int)`

    **`Return:`** *None*

      This method sets the desired setpoint for the velocity control in terms of RPM.

      `id` argument is the device ID of the driver.


  - ####  `get_velocity(self, id: int)`

    **`Return:`** *Current velocity of the motor shaft*

      This method gets the current velocity of the motor output shaft from the driver in terms of RPM.

      `id` argument is the device ID of the driver.

  - ####  `set_torque(self, id: int, sp: int)`

    **`Return:`** *None*

      This method sets the desired setpoint for the torque control in terms of milliamps (mA).

      `id` argument is the device ID of the driver.


  - ####  `get_torque(self, id: int)`

    **`Return:`** *Current drawn from the motor (mA)*

      This method gets the current drawn from the motor from the driver in terms of milliamps (mA).

      `id` argument is the device ID of the driver.

  - ####  `set_duty_cycle(self, id: int, pct: float):`

    **`Return:`** *None*

      This method sets the duty cycle to the motor for PWM control mode in terms of percentage. Negative values will change the motor direction.

      `id` argument is the device ID of the driver.

      `id` argument is the duty cycle percentage.

  - ####  `get_analog_port(self, id: int):`

    **`Return:`** *ADC conversion value of the port*

      This method gets the ADC values from the analog port of the device with
      10 bit resolution. The value is in range [0, 4095].

      `id` argument is the device ID of the driver.

  - ####  `set_control_parameters_position(self, id: int, p=None, i=None, d=None, db=None, ff=None, ol=None)`

    **`Return:`** *None*

      This method sets the control block parameters for position control mode.
      Only assigned parameters are written, `None`'s are ignored. The default
      max output limit is 950.

      `id` argument is the device ID of the driver.

      `p` argument is the the proportional gain. Defaults to None.

      `i` argument is the integral gain. Defaults to None.

      `d` argument is the derivative gain. Defaults to None.

      `db` argument is the deadband (of the setpoint type) value. Defaults to None.

      `ff` argument is the feedforward value. Defaults to None.

      `ol` argument is the maximum output limit. Defaults to None.

  - ####  `get_control_parameters_position(self, id: int)`

    **`Return:`** *Returns the list [P, I, D, Feedforward, Deadband, OutputLimit]*

      This method gets the position control block parameters.

      `id` argument is the device ID of the driver.

  - ####  `set_control_parameters_velocity(self, id: int, p=None, i=None, d=None, db=None, ff=None, ol=None)`

    **`Return:`** *None*

      This method sets the control block parameters for velocity control mode.
        Only assigned parameters are written, `None`'s are ignored. The default
        max output limit is 950.

      `id` argument is the device ID of the driver.

      `p` argument is the the proportional gain. Defaults to None.

      `i` argument is the integral gain. Defaults to None.

      `d` argument is the derivative gain. Defaults to None.

      `db` argument is the deadband (of the setpoint type) value. Defaults to None.

      `ff` argument is the feedforward value. Defaults to None.

      `ol` argument is the maximum output limit. Defaults to None.

  - ####  `get_control_parameters_velocity(self, id: int)`

    **`Return:`** *Returns the list [P, I, D, Feedforward, Deadband, OutputLimit]*

      This method gets the velocity control block parameters.

      `id` argument is the device ID of the driver.
  

  - ####  `set_control_parameters_torque(self, id: int, p=None, i=None, d=None, db=None, ff=None, ol=None)`

    **`Return:`** *None*

      This method sets the control block parameters for torque control mode.
        Only assigned parameters are written, `None`'s are ignored. The default
        max output limit is 950.

      `id` argument is the device ID of the driver.

      `p` argument is the the proportional gain. Defaults to None.

      `i` argument is the integral gain. Defaults to None.

      `d` argument is the derivative gain. Defaults to None.

      `db` argument is the deadband (of the setpoint type) value. Defaults to None.

      `ff` argument is the feedforward value. Defaults to None.

      `ol` argument is the maximum output limit. Defaults to None.

  - ####  `get_control_parameters_torque(self, id: int)`

    **`Return:`** *Returns the list [P, I, D, Feedforward, Deadband, OutputLimit]*

      This method gets the torque control block parameters.

      `id` argument is the device ID of the driver.

  - ####  `get_button(self, id: int, index: Index)`

    **`Return:`** *Returns the button state*

      This method gets the button module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the button module.

  - ####  `get_light(self, id: int, index: Index):`

    **`Return:`** *Returns the ambient light measurement (in lux)*

      This method gets the ambient light module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the ambient light module.

  - ####  `set_buzzer(self, id: int, index: Index, en: bool):`

    **`Return:`** *None*

      This method enables/disables the buzzer module with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the buzzer module.

      `en` argument enables or disables the buzzer. (Enable = 1, Disable = 0)

  - ####  `get_joystick(self, id: int, index: Index):`

    **`Return:`** *Returns the joystick module analogs and button data*

      This method gets the joystick module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the joystick module.

  - ####  `get_distance(self, id: int, index: Index):`

    **`Return:`** *Returns the distance from the ultrasonic distance module (in cm)*

      This method gets the ultrasonic distance module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the ultrasonic distance module.

  - ####  `get_qtr(self, id: int, index: Index):`

    **`Return:`** *Returns qtr module data: [Left(bool), Middle(bool), Right(bool)]*

      This method gets the qtr module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the qtr module.

  - ####  `set_servo(self, id: int, index: Index, val: int):`

    **`Return:`** *None*

      This method moves servo module to a desired position.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the servo module.

      `val`argument is the value to write to the servo (0, 255).

  - ####  `get_potantiometer(self, id: int, index: Index):`

    **`Return:`** *Returns the ADC conversion from the potantiometer module*

      This method gets the potantiometer module data with given index.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the potantiometer module.

  - ####  `set_rgb(self, id: int, index: Index, color: Colors):`

    **`Return:`** *None*

      This method sets the colour emitted from the RGB module.

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the RGB module.

      `color` argument is the color for RGB from Colors class.

  - ####  `get_imu(self, id: int, index: Index):`

    **`Return:`** *Returns roll, pitch angles*

      This method gets the IMU module data (roll, pitch).

      `id` argument is the device ID of the driver.

      `index` argument is the protocol index of the IMU module.



## Examples
### An Example of Autotune 
```python
from smd.red import *
import time

MASTER_PORT =  "/dev/ttyUSB0" #depending on operating system, port, etc. may vary depending on the
master = Master(MASTER_PORT) #creating master object

print(master.scan()) #prints ID list of connected SMDs

ID = master.attached()[0] #getting ID of first SMD from scanned ones. You can use directly ID = 0 if it has never been changed before.

master.set_shaft_rpm(ID,10000)  #rpm and cpr values are depend on the motor you use.
master.set_shaft_cpr(ID,64)
master.pid_tuner(ID)            #starts autotune for setting PID values of control algorithms
```
#### you can see the PID values after then autotune with code below. 
```python
from smd.red import *
import time

MASTER_PORT =  "/dev/ttyUSB0"
master = Master(MASTER_PORT) #creating master object
print(master.scan())
ID = 0 #ID of the SMD connected and autotuned.

print(master.get_control_parameters_position(ID))
print(master.get_control_parameters_velocity(ID))

```

### An Example of PWM Control
```python
from smd.red import *


MASTER_PORT =  "COM10"
master = Master(MASTER_PORT) #creating master object
print(master.scan())
ID = 0 

master.set_operation_mode(ID, 0)    #sets the operating mode to 0 represents PWM control mode.
master.set_duty_cycle(ID, 50)       #sets the duty cycle to 50 percent
master.enable_torque(ID, True)      #enables the motor torque to start rotating
```
### An Example of Position Control
```python
from smd.red import *

MASTER_PORT =  "COM10"
master = Master(MASTER_PORT) #creating master object
print(master.scan())
ID = 0 

master.set_shaft_rpm(ID, 10000)  #rpm and cpr values are depend on the motor you use.
master.set_shaft_cpr(ID, 64)
master.set_control_parameters_position(ID, 10, 0, 8) #SMD ID, Kp, Ki, Kd

master.set_operation_mode(ID, 1)    #sets the operating mode to 1 represents Position control mode.
master.enable_torque(ID, True)      #enables the motor torque to start rotating

while True:
    master.set_position(ID, 5000)   #sets the setpoint to 5000 encoder ticks.
    time.sleep(1.2)
    master.set_position(ID, 0)      #sets the setpoint to 0 encoder ticks. Motor goes to start
    time.sleep(1.2)

```
You should enter the PID values of Position Control Mode or just tune once the SMD at start. CPR and RPM values should be entered to SMD calculates the neseccary varaibles. If you don't then the motor cannot rotate.

### An Example of Velocity Control
```python
from smd.red import *

MASTER_PORT =  "COM10"
master = Master(MASTER_PORT) #creating master object
print(master.scan())
ID = 0 

master.set_shaft_rpm(ID,10000)  #rpm and cpr values are depend on the motor you use.
master.set_shaft_cpr(ID,64)
master.set_control_parameters_velocity(ID,10,1,0) #SMD ID, Kp, Ki, Kd

master.set_operation_mode(ID, 2)    #sets the operating mode to 2 represents Velocity control mode.
master.set_velocity(ID, 2000)       #sets the setpoint to 2000 RPM.   

master.enable_torque(ID, True)      #enables the motor torque to start rotating
```
You should enter the PID values of Position Control Mode or just tune once the SMD at start. CPR and RPM values should be entered to SMD calculates the neseccary varaibles. If you don't then the motor cannot rotate.

### An Example of Torque Control
```python
from smd.red import *

MASTER_PORT =  "COM10"
master = Master(MASTER_PORT) #creating master object
print(master.scan())
ID = 0 

master.set_shaft_rpm(ID,10000)  #rpm and cpr values are depend on the motor you use.
master.set_shaft_cpr(ID,64)
master.set_control_parameters_torque(ID, 10, 0.1, 0) #SMD ID, Kp, Ki, Kd
#master.set_torque_limit(220)

master.set_operation_mode(ID, 3)    #sets the operating mode to 3 represents Torque control mode.
master.set_torque(ID, 80)          #sets the setpoint to 80 mili amps(mA).
master.enable_torque(ID, True)      #enables the motor torque to start rotating
```
You must enter the PID values of the Torque Control Mode. Since Auto tune does not produce these values, you must set them yourself. If you do not do this, the motor cannot rotate properly.

