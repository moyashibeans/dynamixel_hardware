# single_unit_test

## Test command list

### Start single motor test launch

Start with no controller interfaces.

```shell
$ ros2 launch single_unit_test single_unit_test.launch.xml
```

Start with position controller interface.

```shell
$ ros2 launch single_unit_test single_unit_test.launch.xml use_position_controller:=true
```

Start with position controller interface and effort controller interface. (use CurrentBasedPosition control)

```shell
$ ros2 launch single_unit_test single_unit_test.launch.xml use_position_controller:=true use_effort_controller:=true
```


### Start double motor test launch

Start with no controller interfaces.

```shell
$ ros2 launch single_unit_test double_units_test.launch.xml
```

Start with position controller interface.

```shell
$ ros2 launch single_unit_test double_units_test.launch.xml use_position_controller:=true
```

Start with position controller interface and effort controller interface. (use CurrentBasedPosition control)

```shell
$ ros2 launch single_unit_test double_units_test.launch.xml use_position_controller:=true use_effort_controller:=true
```

### Change command interfaces

deactivate all command interfaces.

```shell
$ ros2 control switch_controllers --deactivate position_controller velocity_controller effort_controller
```

start current based position control

```shell
$ ros2 control switch_controllers --activate position_controller effort_controller
```

### Motor move commands in currentBasedPosition control mode

Note that the message to be published to '/effort_controller/commands' is in units of current(mA),not torque(N*m) and effort(N).

```shell
$ ros2 topic pub /effort_controller/commands std_msgs/msg/Float64MultiArray "data: [400,200]"
$ ros2 topic pub /position_controller/commands std_msgs/msg/Float64MultiArray "data: [0.1,0.3]"
```
