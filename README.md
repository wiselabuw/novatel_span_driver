# novatel_span_driver

Version: 2.0.0

This ROS package connects via Ethernet to a [NovAtel](http://www.novatel.com/) receiver running
[SPAN](http://www.novatel.com/span).

Please see the ROS Wiki for details: http://wiki.ros.org/novatel_span_driver

DISCLAIMER:
The driver has reached end-of-life and it is no longer supported by Novatel.
This repository is "best effort" to provide compatibility with ROS Noetic and Python3
but the code is provided "AS IS", without any warranties or guarantees of correctness.
The driver has only been tested with Novatel ProPak6D with NTRIP and in RTK_FIXED mode.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

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
