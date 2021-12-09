### Cân chỉnh Z OFFSET

```wrap
Send: PROBE_CALIBRATE
Recv: // probe at 107.000,85.000 is z=3.100000
Recv: // Starting manual Z probe. Use TESTZ to adjust position.
Recv: // Finish with ACCEPT or ABORT command.
Recv: // Z position: ?????? --> 8.100 <-- ??????
Recv: ok
[...]
Send: TESTZ z=-8
Recv: // Z position: ?????? --> 0.100 <-- 8.100
Recv: ok
[...]
Recv: // Z position: 0.100 --> 0.200 <-- 0.300
Recv: ok
[...]
Send: TESTZ z=-0.1
Recv: // Z position: 0.000 --> 0.100 <-- 0.200
Recv: ok
[...]
Send: TESTZ z=0.1
Recv: // Z position: 0.100 --> 0.200 <-- 0.300
Recv: ok
[...]
Send: TESTZ z=-0.05
Recv: // Z position: 0.100 --> 0.150 <-- 0.200
Recv: ok
[...]
Send: ACCEPT
Recv: // probe: z_offset: 2.950
Recv: // The SAVE_CONFIG command will update the printer config file
Recv: // with the above and restart the printer.
#### Recv: ok
[...]
Send: SAVE_CONFIG
Recv: ok

```

### Kiểm tra đầu dò xem ổn định không 

```wrap
Send: PROBE_ACCURACY
Recv: // PROBE_ACCURACY at X:107.000 Y:115.000 Z:5.025 (samples=10 retract=2.000 speed=30.0 lift_speed=30.0)
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe at 107.000,115.000 is z=2.937500
Recv: // probe at 107.000,115.000 is z=2.937500
Recv: // probe at 107.000,115.000 is z=2.937500
Recv: // probe at 107.000,115.000 is z=2.937500
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe at 107.000,115.000 is z=2.925000
Recv: // probe accuracy results: maximum 2.937500, minimum 2.925000, range 0.012500, average 2.930000, median 2.925000, standard deviation 0.006124
Recv: ok

```

### Kiểm tra từng trigger 

```wrap 

Send: QUERY_ENDSTOPS
Recv: x:open y:open z:open
Recv: ok
[...]
Send: QUERY_ENDSTOPS
Recv: x:open y:open z:TRIGGERED
Recv: ok

```


### PID Tune Heated Bed
Move nozzle to the center of the bed and approximately 5-10mm above the bed surface, then run:

#### PID_CALIBRATE HEATER=heater_bed TARGET=100

It will perform a PID calibration routine that will last about 10 minutes. Once it is finished, 
type SAVE_CONFIG which will save the parameters into your configuration file.

```wrap


Send: PID_CALIBRATE HEATER=heater_bed TARGET=100
Recv: B:43.5 /100.0 T0:55.7 /0.0
Recv: B:43.5 /100.0 T0:55.6 /0.0
Recv: B:43.5 /100.0 T0:55.4 /0.0
Recv: B:43.5 /100.0 T0:55.3 /0.0
Recv: B:43.5 /100.0 T0:55.1 /0.0
Recv: B:43.5 /100.0 T0:55.0 /0.0
Recv: B:43.5 /100.0 T0:55.0 /0.0
Recv: B:43.5 /100.0 T0:54.9 /0.0

```

### PID Tune HEATER Extruder
ok B:33.4 /0.0 T0:32.7 /0.0
#### PID_CALIBRATE HEATER=extruder TARGET=220

```wrap
PID_CALIBRATE HEATER=extruder TARGET=220
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0
// PID parameters: pid_Kp=25.197 pid_Ki=1.098 pid_Kd=144.568
// The SAVE_CONFIG command will update the printer config file
// with these parameters and restart the printer.
```

### Pressure_Advance.md

https://github.com/Klipper3d/klipper/blob/master/docs/Pressure_Advance.md

```wrap
SET_VELOCITY_LIMIT SQUARE_CORNER_VELOCITY=1 ACCEL=500
// max_velocity: 300.000000
// max_accel: 500.000000
// max_accel_to_decel: 3250.000000
// square_corner_velocity: 1.000000
ok
TUNING_TOWER COMMAND=SET_PRESSURE_ADVANCE PARAMETER=ADVANCE START=0 FACTOR=.005
// Starting tuning test (start=0.000000 factor=0.005000)
ok
```

https://github.com/AndrewEllis93/Print-Tuning-Guide#tower-method-simple

1) Download and slice the pressure advance tower with your normal print settings (accelerations included).
The only modifications you should make are these:

```wrap 
    120mm/s external perimeter speed
    1 perimeter
    0% infill
    0 top layers
    0 second "minimum layer time" / "layer time goal"
    High fan speed
```

Pressure Advance => Thay đổi sự phân bố của nhựa , không phải thay đổi số lượng nhựa.

Giá trị thấp hơn dẫn đến ít nhựa hơn ở giữa các dòng và nhiều hơn ở các đầu / góc.

Giá trị cao hơn dẫn đến nhiều nhựa hơn ở giữa các dòng và ít hơn ở các đầu / góc.

Hãy nhớ rằng: Hiếm khi có cái gọi Pressure Advance hoàn hảo 

Việc tăng tốc hoặc giảm tốc hầu như luôn luôn không hoàn hảo. Bạn nên luôn luôn sai lầm về phía các giá trị PA thấp hơn.

Pressure Advance  có thể thay đổi với các nhựa  khác nhau. Nên thay đổi nhựa nhớ tính toán lại

Thông thường, tôi chỉ thấy cần thiết phải điều chỉnh theo từng loại nhựa - ABS, PETG, PLA, TPU,

### input shape 

https://www.youtube.com/watch?v=OoWQUcFimX8

https://www.klipper3d.org/RPi_microcontroller.html

https://www.klipper3d.org/Measuring_Resonances.html

![image](https://user-images.githubusercontent.com/38026441/136640537-97f0ea9a-60b8-447d-9656-590493f2beb7.png)

![image](https://user-images.githubusercontent.com/38026441/136640558-afe3f08a-39a4-4bd1-a43c-5fbb4fc01c47.png)

![image](https://user-images.githubusercontent.com/38026441/136640658-237ca161-5a5f-4af3-b2c7-5b6fe78dc31e.png)

```wrap
Setup 

[mcu rpi]
serial: /tmp/klipper_host_mcu

[adxl345]
cs_pin: rpi:None

[resonance_tester]
accel_chip: adxl345
probe_points:
    100,100,20  # an example
#########################

Send: ACCELEROMETER_QUERY
Recv: // adxl345 values (x, y, z): -9408.500010, -1453.345530, -1300.361790
Recv: ok

TEST_RESONANCES AXIS=X


Send: TEST_RESONANCES AXIS=X
Recv: !! Must home axis first: 107.000 100.000 20.000 [0.000]
Recv: ok
Send: M105
Recv: ok B:30.5 /0.0 T0:58.9 /0.0
Send: M105
Recv: ok B:30.5 /0.0 T0:58.2 /0.0
Send: G91
Recv: ok
Send: G28 Z0
Recv: ok
Send: G90
Recv: ok
Send: M105
Recv: ok B:30.5 /0.0 T0:56.5 /0.0
Send: TEST_RESONANCES AXIS=X
Recv: // max_velocity: 200.000000
Recv: // max_accel: 10000.000000
Recv: // max_accel_to_decel: 10000.000000
Recv: // square_corner_velocity: 4.000000
Recv: // Testing frequency 5 Hz
Recv: // Testing frequency 6 Hz
......

Recv: // Testing frequency 109 Hz
Recv: // Testing frequency 110 Hz
Recv: // Testing frequency 111 Hz
Recv: // Testing frequency 112 Hz
Recv: // Testing frequency 133 Hz
Recv: // max_velocity: 200.000000
Recv: // max_accel: 1000.000000
Recv: // max_accel_to_decel: 500.000000
Recv: // square_corner_velocity: 4.000000
Recv: // xy-axis accelerometer stats: drops=0,overflows=3,time_per_sample=0.000314001,start_range=0.000068,end_range=0.000037
Recv: // Wait for calculations..
Recv: // Resonances data written to /tmp/resonances_x_20211009_032546.csv file
Recv: ok
```    

~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png

~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_*.csv -o /tmp/shaper_calibrate_y.png


```wrap
pi@octopi:/tmp $ rm resonances_x_20211009_032546.csv
pi@octopi:/tmp $ ~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png
Fitted shaper 'zv' frequency = 34.6 Hz (vibrations = 27.4%, smoothing ~= 0.130)
To avoid too much smoothing with 'zv', suggested max_accel <= 4500 mm/sec^2
Fitted shaper 'mzv' frequency = 26.2 Hz (vibrations = 7.6%, smoothing ~= 0.297)
To avoid too much smoothing with 'mzv', suggested max_accel <= 2000 mm/sec^2
Fitted shaper 'ei' frequency = 32.8 Hz (vibrations = 7.4%, smoothing ~= 0.299)
To avoid too much smoothing with 'ei', suggested max_accel <= 2000 mm/sec^2
Fitted shaper '2hump_ei' frequency = 39.0 Hz (vibrations = 5.4%, smoothing ~= 0.355)
To avoid too much smoothing with '2hump_ei', suggested max_accel <= 1500 mm/sec^2
Fitted shaper '3hump_ei' frequency = 48.0 Hz (vibrations = 5.3%, smoothing ~= 0.356)
To avoid too much smoothing with '3hump_ei', suggested max_accel <= 1500 mm/sec^2
Recommended shaper is mzv @ 26.2 Hz
```   

![image](https://user-images.githubusercontent.com/38026441/136641388-c0021fe6-c0a9-4f4b-a05f-5f7ab0e3db84.png)

![image](https://user-images.githubusercontent.com/38026441/136641455-14965b76-8117-4e46-850f-1d7443d0684d.png)


```wrap
[input_shaper]
shaper_freq_x: 27
shaper_freq_y: 36
shaper_type: mzv
```

### Selecting max_accel

https://www.klipper3d.org/Resonance_Compensation.html

https://www.klipper3d.org/prints/ringing_tower.stl

```wrap
SET_PRESSURE_ADVANCE ADVANCE=0
// pressure_advance: 0.000000
// pressure_advance_smooth_time: 0.040000
ok
TUNING_TOWER COMMAND=SET_VELOCITY_LIMIT PARAMETER=ACCEL START=1250 FACTOR=100 BAND=5
// Ending tuning test mode
// Starting tuning test (start=1250.000000 factor=100.000000)
ok
TUNING_TOWER COMMAND=SET_VELOCITY_LIMIT PARAMETER=ACCEL START=1250 FACTOR=100 BAND=5
// Ending tuning test mode
// Starting tuning test (start=1250.000000 factor=100.000000)
```


# Verify stepper_buzz
```wrap
STEPPER_BUZZ STEPPER=stepper_z
STEPPER_BUZZ STEPPER=stepper_z1
STEPPER_BUZZ STEPPER=stepper_z2
```


### Extrusion multiplier và Pressure Advance Có quan hệ với nhau, nên chỉnh 1 trong 2 giá trị không đúng dẫn đến in không đẹp 

Approximate Values
|Hotend  |	Flow Rate (mm3/sec) |
| --- | --- |
|E3D V6  |	11
|E3D Revo |	15
|Dragon SF|	15
|Dragon HF |	24
|Mosquito |	20
|Mosquito Magnum |	30



## cHow Volumetric Flow Rate Relates to Print Speed

Working out how quickly you can print at a given volumetric flow rate is quite simple:

   ### speed = volumetric flow / layer height / line width
    
  ####  167  = 15 / 0.2 / 0.45 
    
  ####  222  = 20 / 0.2 / 0.45 
    
Or, inversely,

 ### volumetric flow = speed * line width * layer height

For example, if your hotend is capable of 24mm3/sec, and you are printing with 0.4mm line width, at 0.2mm layer height:

    24 / 0.4 / 0.2 = Maximum print speed of 300mm/sec
