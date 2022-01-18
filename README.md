# The fork of Open Motion Planning Library (OMPL) with Modified Intelligent Bidirectional Rapidly-exploring Random Tree planner (MIBRRT)

Visit the [OMPL installation page](https://ompl.kavrakilab.org/core/installation.html) for
detailed installation instructions.

OMPL has the following required dependencies:

* [Boost](https://www.boost.org) (version 1.58 or higher)
* [CMake](https://www.cmake.org) (version 3.5 or higher)
* [Eigen](http://eigen.tuxfamily.org) (version 3.3 or higher)

The following dependencies are optional:

* [ODE](http://ode.org) (needed to compile support for planning using the Open Dynamics Engine)
* [Py++](https://github.com/ompl/ompl/blob/main/doc/markdown/installPyPlusPlus.md) (needed to generate Python bindings)
* [Doxygen](http://www.doxygen.org) (needed to create a local copy of the documentation at
  https://ompl.kavrakilab.org/core)

Once dependencies are installed, you can build OMPL on Linux, macOS,
and MS Windows. Go to the top-level directory of OMPL and type the
following commands:
```bash
mkdir -p build/Release
cd build/Release
cmake -DCMAKE_INSTALL_PREFIX=/opt/ros/${ROS_DISTRO}../.. 
# next step is optional
make -j 4 update_bindings # if you want Python bindings
make -j 4 # replace "4" with the number of cores on your machine
```

## How to add the library to MoveIt!

After installation of OMPL from source:
1. Download the MoveIt! source (https://ros-planning.github.io/moveit_tutorials/doc/getting_started/getting_started.html) but **don't** build the package in your workspace.
2. In your MoveIt! directory, modify *src/moveit_planners/ompl/ompl_interface/src/planning_context_manager.cpp*: include the header file that defines your planner at the top and register your planner in the registerDefaultPlanners() function as the existing ones are.
3. Finish the last 2 steps of the MoveIt! installation (catkin_make/catkin build and source the install).
4. If you've already generated MoveIt! config files for your robot, modify */config/ompl_planning.yaml* in YOURROBOT_moveit_config to include the option for the new planner. 