# MPC_Tutorial
This tutorial mainly covers the installation of MPC Planner. Other contents like theory or usage might be added in the future.
1. Installing on your Computer (for simulation).
2. Installing on your machine (for real-world testing).

## Installation
Below will offer the process for installing on your machine. The process for installing on your computer will be added in the future.
### On your machine
If pc and the machine use SSH to connect, it's recommended to use [FileZilla](https://filezilla-project.org/) to transfer files between them. For both step 1 and 2, you can place dependent packages `coinor_libipopt_packages` and `control_box_rst` anywhere.
1. Install debian packages inside folder `coinor_libipopt_packages` via `dpkg`.
    ```
    # on the machine
    ~$ cd coinor_libipopt_packages

    # install all the deb files in coinor_libipopt_packages
    ~$ sudo dpkg -i *.deb
    ```
2.  Build `control_box_rst`. For more information, you can visit https://github.com/rst-tu-dortmund/control_box_rst.
    ```
    ~$ cd control_box_rst
    ~$ mkdir build
    ~$ cd build
    ~$ cmake ..
    ~$ make -j8 -l8
    ~$ make install
    ```
3. Run `catkin_make` in `catkin_ws`. You can also name your workspace (e.g. My_ws) on the machine. Then put [mpc_local_planner](https://codeload.github.com/rst-tu-dortmund/mpc_local_planner/zip/refs/heads/noetic-devel) and [yocs_cmd_vel_mux](https://github.com/yujinrobot/yujin_ocs.git) (there's various directories on yujin_ocs, you only need to download yocs_cmd_vel_mux) in the `src` folder of your workspace.
    ```
    ~$ mkdir -p catkin_ws/src
    # put both mpc_local_planner and yocs_cmd_vel_mux in the src folder
    ~$ cd catkin_ws
    ~$ catkin_make

    # you can add this line to bashrc, so that you don't need to source the workspace every time you open a new terminal
    ~$ source ~/catkin_ws/devel/setup.bash
    ```
4. Inside `move_base.launch`, modify the section that sets the `base_local_planner` parameter, which specifies the local planner to be used. Also change the `local_planner_parameters` to the path of `mpc_local_planner.yaml` (you can rename the yaml file).
    ```
    # inside move_base.launch
    <arg name="base_local_planner" default="mpc_local_planner/MpcLocalPlanner" />
    <rosparam file="path to mpc_local_planner.yaml" command="load" />
    ```

### On your computer
TODO