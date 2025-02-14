**Build**  
Note: the zenoh bridge is prebuilt. You can simply unzip the binary to the workspace and run it. The cmake file just automates this.
```bash
colcon build --packages-select zenoh_vendor
```

**Run**  
The bridge takes an optional config (-c) that allows specification of key parameters such as topics to bridge and mode selection.
```bash
ros2 run zenoh_vendor zenoh-bridge-ros2dds -c /workspace/src/zenoh_vendor/configs/zenoh_starling.json5
```
