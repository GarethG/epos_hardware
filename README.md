epos_hardware
============

Overview
============
A ROS wrapper for the Maxon Motor EPOS Command Library to allow use of EPOS motor controllers with ros_control.

Nodes
============

epos_hardware_node
Node that launches a controller manager with Maxon Motors as the robot hardware. Transmissions are also loaded from the URDF. The motors to load are specified as arguments.
Parameters

robot_description (string)
The robot description that is searched for transmissions to load

Usage

 $ rosrun epos_hardware epos_hardware_node motor_name1 motor_name2 motor_name3
Each name that is specified as an argument will be loaded as a motor. See below for configuration

Configuration
============

Both the epos_hardware_node node and the epos_manager library are configured using ROS parameters. If a parameter is related to a register value then the register is listed in the parameter description. (NOTE: the values may not be the same if the units are different) See the EPOS Command Library documentation for more information.

NOTE: while amps and seconds are used for most parameters, all position and velocity parameters and control inputs are in the device units (this is normally rotations and rpm by default).

Device Parameters
~/motor_name/serial_number (string)

The serial number of the motor (in hex). This is used to locate the motor.
~/motor_name/actuator_name (string)
The name of the actuator this motor corresponds to in the URDF
~/motor_name/operation_mode (string)
The mode the motor runs in. One of 'profile_position', 'profile_velocity'
~/motor_name/clear_faults (bool, default: false)
If the driver should attempt to clear errors on the device before enabling it
Motor Parameters
~/motor_name/motor/type (int)

The type of the motor (0x6402-00)
DC Motor Parameters

~/motor_name/motor/dc_motor/nominal_current (double)

The max continuous motor current in amps (0x6410-01)
~/motor_name/motor/dc_motor/max_output_current (double)
The max peak current in amps (0x6410-02)
~/motor_name/motor/dc_motor/thermal_time_constant (double)
The thermal time constant in seconds (0x6410-05)
EC Motor Parameters

~/motor_name/motor/ec_motor/nominal_current (double)

The max continuous motor current in amps (0x6410-01)
~/motor_name/motor/ec_motor/max_output_current (double)
The max peak current in amps (0x6410-02)
~/motor_name/motor/ec_motor/thermal_time_constant (double)
The thermal time constant in seconds (0x6410-05)
~/motor_name/motor/ec_motor/number_of_pole_pairs (int)
The number of pole pairs (0x6410-03)
Sensor Parameters
~/motor_name/sensor/type (int)

The type of the sensor (0x2210-02)
Incremental Encoder Parameters

~/motor_name/motor/incremental_encoder/resolution (int)

The resolution of the encoder (0x2210-01)
~/motor_name/motor/incremental_encoder/inverted_polarity (bool)
If the encoder is inverted from the motor (0x2210-04)
Hall Sensor Parameters

~/motor_name/motor/hall_sensor/inverted_polarity (bool)

If the hall sensor is inverted from the motor
SSI Absolute Encoder Parameters

~/motor_name/motor/ssi_absolute_encoder/inverted_polarity (bool)

If the encoder is inverted from the motor (0x2210-04)
~/motor_name/motor/ssi_absolute_encoder/data_rate (int)
(0x2211-01)
~/motor_name/motor/ssi_absolute_encoder/number_of_multiturn_bits (int)
(0x2211-02)
~/motor_name/motor/ssi_absolute_encoder/number_of_singleturn_bits (int)
(0x2211-02)
Safety Parameters
~/motor_name/safety/max_following_error (int)

Max following error (0x6065-00)
~/motor_name/safety/max_profile_velocity (int)
Max velocity (0x607F-00)
~/motor_name/safety/max_acceleration (int)
Max acceleration/deceleration (0x60C5-00)
Position Regulator Parameters
~/motor_name/position_regulator/gain/p (int)

Regulator P parameter (0x60FB-01)
~/motor_name/position_regulator/gain/i (int)
Regulator I parameter (0x60FB-02)
~/motor_name/position_regulator/gain/d (int)
Regulator D parameter (0x60FB-03)
~/motor_name/position_regulator/feed_forward/velocity (int)
Regulator feed forward velocity (0x60FB-04)
~/motor_name/position_regulator/feed_forward/acceleration (int)
Regulator feed forward acceleration (0x60FB-05)
Velocity Regulator Parameters
~/motor_name/velocity_regulator/gain/p (int)

Regulator P parameter (0x60F9-01)
~/motor_name/velocity_regulator/gain/i (int)
Regulator I parameter (0x60F9-02)
~/motor_name/velocity_regulator/feed_forward/velocity (int)
Regulator feed forward velocity (0x60F9-04)
~/motor_name/velocity_regulator/feed_forward/acceleration (int)
Regulator feed forward acceleration (0x60F9-05)
Current Regulator Parameters
~/motor_name/velocity_regulator/gain/p (int)

Regulator P parameter (0x60F6-01)
~/motor_name/velocity_regulator/gain/i (int)
Regulator I parameter (0x60F6-02)
Position Profile Parameters
~/motor_name/position_profile/velocity (int)

Position profile velocity (0x6081-00)
~/motor_name/position_profile/acceleration (int)
Position profile acceleration (0x6083-00)
~/motor_name/position_profile/deceleration (int)
Position profile deceleration (0x6084-00)
~/motor_name/position_profile/window/window (int)
Position window value (0x6067-00)
~/motor_name/position_profile/window/time (int)
Position window time value in seconds (0x6068-00)
Velocity Profile Parameters
~/motor_name/velocity_profile/acceleration (int)

Velocity profile acceleration (0x6083-00)
~/motor_name/velocity_profile/deceleration (int)
Velocity profile deceleration (0x6084-00)
~/motor_name/velocity_profile/window/window (int)
Position window value (0x606D-00)
~/motor_name/velocity_profile/window/time (int)
Position window time value in seconds (0x606E-00)
Tools
list_devices

 $ rosrun epos_hardware list_devices [--rs232]
Enumerate all EPOS devices on USB and optionally RS232 ports

get_state

 $ rosrun epos_hardware get_state serial_number
Get the position, velocity, and current from the motor with the given serial number
