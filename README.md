# navvis_playback

This ROS package is designed to handle the playback of ROS bag files and the visualization of sensor and robot data in RVIZ. It provides functionality to either use the command line or a GUI tool to play back bag files and display the corresponding data in an RVIZ environment.

## Requirements
- ROS (Noetic/Melodic or compatible version)
- `rqt_bag` (for GUI playback)
- `rosbag` (for command-line playback)
- `RVIZ` for visualization
- `map_server` (optional, for 2D map display)

## Package Contents
- **config/**: Contains the RVIZ configuration file `config.rviz` that defines the RVIZ display settings.
- **urdf/**: Contains the XACRO file `navvis_bag_playback.xacro`, which describes the robot model used in the bag files.
- **launch/**: Contains the following launch files:
  - `bag.launch`: Handles the playback of bag files, with support for both GUI and command-line methods.
  - `navvis_playback.launch`: The main launch file that integrates both `bag.launch` and the robot display, and passes configuration files to RVIZ.

## Setup Instructions

### 1. Clone the repository
```bash
cd ~/catkin_ws/src
git clone https://github.com/cwru-courses/ecse473_f24_jxc2077_navvis_playback.git
cd ~/catkin_ws
catkin_make
```

### 2. Download ROS bag files
The ROS bag files for this project can be found [here](https://drive.google.com/drive/folders/1ptmPrQc8g12GmbfNCklQ2fOF5rFum46). Download the bag files and place them in the `bags` directory within the package.

```bash
cd ~/catkin_ws/src/navvis_playback
mkdir bags
ln -s <full_path_to_bag_file> bags/
```

> **Note:** Bag files should not be included in the repository.

## Usage

### Playing Back Bag Files

#### Using GUI (`rqt_bag`)
To playback the bag files using a graphical interface:
```bash
roslaunch navvis_playback navvis_playback.launch use_bag:=gui
```

#### Using Command Line (`rosbag`)
To playback the bag files using the command line:
```bash
roslaunch navvis_playback navvis_playback.launch use_bag:=cmd_line
```

### Displaying the Robot in RVIZ
This package includes the robot model and necessary configuration for RVIZ. To launch the robot model and view the sensor data:
```bash
roslaunch navvis_playback navvis_playback.launch
```
You can modify the `use_xacro` argument to `false` if you prefer to use a URDF file instead of a XACRO file.

```bash
roslaunch navvis_playback navvis_playback.launch use_xacro:=false
```

## File Descriptions

### `bag.launch`
- **Parameters:**
  - `use_bag_gui`: Controls whether to use GUI (`rqt_bag`) or command line (`rosbag`) to playback bag files. Can be `true` or `false`.
  - `bag_file_name`: The name of the bag file to be played back.
  - `full_bag_path`: The full path to the bag file.

### `navvis_playback.launch`
- Includes `bag.launch` for bag playback and passes necessary arguments.
- Includes `navvis_description/launch/display.launch` for robot and sensor visualization in RVIZ.
- **Parameters:**
  - `use_bag`: Controls whether to use GUI or command line for playback.
  - `use_xacro`: Controls whether to use XACRO or URDF for the robot model.
  - `rviz_conf`: The path to the RVIZ configuration file.
  - `file`: The path to the XACRO file.

## Troubleshooting

1. **Bag file not playing:**
   - Ensure that the bag file path is correct and that the file exists in the `bags` directory.
   - Check the parameters `bag_file_name` and `full_bag_path` in the `launch` files.
   
2. **RVIZ not displaying data:**
   - Ensure that the correct topics are being published.
   - Try resetting RVIZ by pressing the “Reset” button at the bottom left if using bag playback with timestamps.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
