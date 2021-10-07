Nếu gặp lỗi "min_temp or max_temp" => nguyên nhân dây Sensor bị đứt hoặc không gắn dây sensor

```wrap 

Recv: // MCU 'mcu' shutdown: ADC out of range
Recv: // This generally occurs when a heater temperature exceeds
Recv: // its configured min_temp or max_temp.
Recv: // Once the underlying issue is corrected, use the
Recv: // "FIRMWARE_RESTART" command to reset the firmware, reload the
Recv: // config, and restart the host software.
Recv: // Printer is shutdown
Recv: // Klipper state: Not ready
Recv: !! MCU 'mcu' shutdown: ADC out of range

```

Không thể move các axis X Y Z khi chưa homing

If the motors are disabled (via an M84 or M18 command) then the motors will need to be homed again prior to movement.

#### Lỗi Move exceeds maximum extrusion (0.752mm^2 vs 0.640mm^2)
Your printer's firmware reported an error. Due to that the ongoing print job will be cancelled. Reported error: Move exceeds maximum extrusion (0.752mm^2 vs 0.640mm^2)
=> put M82 at the end of START_PRINT to revert the effect of M83
M83 or G92 E0 causing "move exceeds max extrusion"


#### Lỗi  pid_calibrate interrupted

```wrap
Recv: // Klipper state: Shutdown
Recv: !! pid_calibrate interrupted

Fix: 

[verify_heater bed]  
heating_gain: 2 
check_gain_time:35  
hysteresis: 10  
max_error: 130 
```


#### LỖI KHÔNG KẾT NỐI VỚI MCU

Nguyên nhân lỗi này là do Cáp kết nối , file config MCU, Thẻ nhớ SD card cần format lại đúng chuẩn 
