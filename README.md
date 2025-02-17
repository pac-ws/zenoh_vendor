**Build**  
Note: the zenoh bridge is prebuilt. You can simply unzip the binary and run it in the workspace. The cmake file just automates this.
```bash
colcon build --packages-select zenoh_vendor
```

**Run**  
The bridge takes an optional config (-c) that allows the specification of key parameters, such as topics for the bridge and mode selection.
```bash
ros2 run zenoh_vendor zenoh-bridge-ros2dds -c <file_name>
```
On the Ground Control Station (GCS) laptop:
```bash
ros2 run zenoh_vendor -c /workspace/src/zenoh_vendor/configs/zenoh_starling.json5
```

On the Starling quadrotor:
```bash
ros2 run zenoh_vendor -c /workspace/src/zenoh_vendor/configs/zenoh_gcs.json5
```
