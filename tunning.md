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
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0
B:33.4 /0.0 T0:32.7 /220.0

```
