# novatel_span_driver

This ROS package connects via Ethernet to a [NovAtel](http://www.novatel.com/) receiver running
[SPAN](http://www.novatel.com/span).

Please see the ROS Wiki for details: http://wiki.ros.org/novatel_span_driver

# Building and testing

We assume Ubuntu 20.04 Focal + ROS Noetic + catkin + colcon.

## Building

Create a colcon workspace and clone the repository:
```
$ mkdir -p novatel_span_driver_colcon_ws/src
$ cd novatel_span_driver_colcon_ws/src
$ git clone https://github.com/wiselabuw/novatel_span_driver.git
```

Install dependencies:
```
$ cd novatel_span_driver_colcon_ws/
$ rosdep install --from-paths src --ignore-src -y -r
ERROR: the following packages/stacks could not have their rosdep keys resolved
to system dependencies:
novatel_span_driver: Cannot locate rosdep definition for [python3-impacket]
Continuing to install resolvable dependencies...
#All required rosdeps installed successfully
```

Build:
```
$ cd novatel_span_driver_colcon_ws/
$ colcon build
Starting >>> novatel_msgs
Finished <<< novatel_msgs [0.67s]
Starting >>> novatel_span_driver
Finished <<< novatel_span_driver [0.47s]

Summary: 2 packages finished [1.23s]
```

## Testing

The tests depend on `python3-pcapy` and `python3-impacket` but they do not have
proper rosdep keys in https://github.com/ros/rosdistro/blob/master/rosdep/python.yaml
and they were not installed by rosdep automatically.
So, we have to install them manually:

```
$ sudo apt install python3-impacket python3-pcapy
```

Run tests:
```
$ cd novatel_span_driver_colcon_ws/
$ colcon test
Starting >>> novatel_msgs
Finished <<< novatel_msgs [0.04s]
Starting >>> novatel_span_driver
Finished <<< novatel_span_driver [19.0s]

Summary: 2 packages finished [19.2s]
$ colcon test-result
Summary: 7 tests, 0 errors, 0 failures, 0 skipped
```
