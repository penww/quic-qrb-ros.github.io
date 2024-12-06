======================
QRB ROS System Monitor
======================

Overview
--------

`QRB ROS System Monitor <https://github.com/quic-qrb-ros/qrb_ros_system_monitor>`__ is a ROS package to publish system informations.

Main features:

-  ``/cpu``: Topic for CPU usage informations
-  ``/memory``: Topic for memory usage informations
-  ``/disk``: Topic for disk usage informations
-  ``/swap``: Topic for swap partition informations
-  ``/temperature``: Topic for CPU temperature
-  ``/battery``: Topic for device battery level
-  ``/system_info_server``: Service for providing system informations.


System Requirements
-------------------

-  Linux, now only support Linux systems

Quickstart
----------

.. tabs::
   .. tab:: Build with QIRP SDK

      1. Setup QCLINUX SDK environments: Reference :doc:`Getting Started - Environment Setup </getting_started/environment_setup>`

      2. Create workspace in QCLINUX SDK environment and clone source code

         .. code:: bash

            mkdir -p <qirp_decompressed_workspace>/qirp-sdk/ros_ws
            cd <qirp_decompressed_workspace>/qirp-sdk/ros_ws

            git clone https://github.com/quic-qrb-ros/qrb_ros_system_monitor.git

      3. Build source code with QCLINUX SDK

         .. code:: bash

            export AMENT_PREFIX_PATH="${OECORE_TARGET_SYSROOT}/usr;${OECORE_NATIVE_SYSROOT}/usr"
            export PYTHONPATH=${PYTHONPATH}:${OECORE_TARGET_SYSROOT}/usr/lib/python3.10/site-packages

            colcon build --merge-install --cmake-args \
            -DPython3_ROOT_DIR=${OECORE_TARGET_SYSROOT}/usr \
            -DPython3_NumPy_INCLUDE_DIR=${OECORE_TARGET_SYSROOT}/usr/lib/python3.10/site-packages/numpy/core/include \
            -DPYTHON_SOABI=cpython-310-aarch64-linux-gnu -DCMAKE_STAGING_PREFIX=$(pwd)/install \
            -DCMAKE_PREFIX_PATH=$(pwd)/install/share \
            -DBUILD_TESTING=OFF

      4. Install ROS package to device

         .. code:: bash

            cd <qirp_decompressed_workspace>/qirp-sdk/ros_ws/install
            tar czvf qrb_ros_system_monitor.tar.gz lib share
            scp qrb_ros_system_monitor.tar.gz root@[ip-addr]:/opt/
            ssh ssh root@[ip-addr]
            (ssh) tar -zxf /opt/qrb_ros_system_monitor.tar.gz -C /opt/qcom/qirp-sdk/usr/

      5. Login to device and run

         .. code:: bash

            ssh root@[ip-addr]
            (ssh) export HOME=/opt
            (ssh) source /usr/bin/ros_setup.bash
            (ssh) source /opt/qcom/qirp-sdk/qirp-setup.sh
            (ssh) ros2 run qrb_ros_system_monitor qrb_ros_system_monitor

   .. tab:: Build with QRB ROS Docker

      1. Pull Docker image

         .. code:: bash

            docker pull qcom/qrb-ros-docker

      2. Download source code

         .. code:: bash

            git clone https://github.com/quic-qrb-ros/qrb_ros_system_monitor.git

      3. Build with Docker

         .. code:: bash

            colcon build

   .. tab:: Build on QCOM Ubuntu

      1. Create workspace and clone source code from GitHub

         .. code:: bash

            mkdir -p ~/ros2_ws/src && cd ~/ros2_ws/src
            git clone https://github.com/quic-qrb-ros/qrb_ros_system_monitor.git

      2. Build source code

         .. code:: bash

            cd ~/ros2_ws
            source /opt/ros/${ROS_DISTRO}/setup.bash
            colcon build

      3. Run system monitor

         .. code:: bash

            cd ~/ros2_ws
            source install/setup.bash
            ros2 run qrb_ros_system_monitor qrb_ros_system_monitor

Packages
--------

.. toctree::
   :maxdepth: 2

    qrb_ros_system_monitor <./qrb_ros_system_monitor>
    qrb_ros_system_monitor_interfaces <./qrb_ros_system_monitor_interfaces>

Supported Platforms
-------------------

.. include:: ../common/supported_platforms.rst

Updates
-------------

+------------+--------------------------+
| Date       | Changes                  |
+------------+--------------------------+
| 2024-10-19 | Initial release          |
+------------+--------------------------+
