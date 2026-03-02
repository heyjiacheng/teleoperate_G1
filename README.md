# teleoperate_G1
A guide to teleoperate unitree G1 humanoid robot in RPL Lab.

Official Repository: https://github.com/unitreerobotics/xr_teleoperate

## Quick Start

Power on G1 robot

```bash
# enter damp mode
press L2 + press B 
# enter ready mode
press L2 + up
# enter motion mode 
press R2 + A
```

```bash
conda activate tv
cd xr_teleoperate/teleop
```

```bash
python teleop_hand_and_arm.py --headless --input-mode controller --record --dex3 --motion
```

Open browser in VR, and enter VR mode
```bash
https://192.168.123.2:8012/?ws=wss://192.168.123.2:8012
```

You can teleopare humanoid now :D

## Overview

This document only explains the steps to teleoperate the real G1 robot using a VR headset. 

Teleoprate G1 in simulation is not included. However, you can find it from the [official repo](https://github.com/unitreerobotics/xr_teleoperate.git). Ask me if you meet any problem (xujiacheng1016@hotmail.com).

## Hardware Components

VR Headset (Quest / Vision Pro)

Host Computer (Ubuntu, runs teleop code)

WiFi Router (dedicated for robot + VR)

Unitree G1

## Network Topology

This image shows how ethernet connect (you can find it from official repo wiki page: Network part)

![network topology](images/real_machine_teleoprate.jpg)

STA means wireless connect, LAN means you have to use wire. Also, make sure no firewall blocking.

## Wifi Router Setup

Keep all device under same subnet (e.g., 192.168.123.xxx). You can do this by login into the wifi router home page.

(Optional) To reduce the teleoprate latency, you can do following steps: use device of wifi 6 or above. Increase Wi-Fi channel bandwidth. Cancle Wi-Fi channel auto select, manually select one from 149-165. Disable 2.4 GHz network. After all, you can try to ping unitree robot to see latency, it should under 2ms.


## Operational Order (Critical)

Startup Sequence:

- Power on G1

- Connect G1 to WiFi router (use LAN)

- Connect Host to same WiFi (same subnet: 192.168.123.*)

- Connect VR headset to same WiFi (default should be same subnet)

- SSH into robot PC2 (just to test connection)

- (Optinal) Start image server

- Put robot into motion control mode (remote controller)

- Start teleoperation script on host

- Enter VR browser page and begin control

## Robot Motion Mode Switching

Teleoperation works if robot is in motion control mode.

Using the Unitree remote controller:

```bash
# power on G1 first, you will hear zero torque mode
# enter damp mode
press L2 + press B 
# enter ready mode
press L2 + up
# enter motion mode 
press R2 + A
```

## VR Access

Remember to connect VR to same Wi-Fi.

After teleop script starts on host:

Open VR browser and access (replace host ip by check ifconfig in your PC):
```bash
https://<host_ip>:8012/?ws=wss://<host_ip>:8012
```
Accept warning (allow VR control)

Verify:

Hand/controller tracking works (in Setting page)

## Safety

If abnormal motion:

press q in teleoperate program

OR

using unitree romote controller:
```bash
long press L2 + B
```

## Pitfalls (I’ve encountered)

- When installing environment, need to fix numpy == 1.26.4  params_proto==2.13.2  rerun-sdk==0.16.1

- To successful run simulation mode, need to cancel binocular in cam_config_server.yaml
