Setup slicer 

![image](https://user-images.githubusercontent.com/38026441/146629658-c0127869-2e4e-4e4a-9a78-7d3499869f02.png)

![image](https://user-images.githubusercontent.com/38026441/146629687-a4bf4242-197d-4131-83fb-973f13ff48f5.png)

![image](https://user-images.githubusercontent.com/38026441/146629713-15132bce-3921-41df-8b9e-a8669b441342.png)

![image](https://user-images.githubusercontent.com/38026441/146629735-546d95b2-5896-47b8-ad8c-2fc8d654a237.png)


Increase max_accel and max_accel_to_decel parameters in your printer.cfg to 7000. Note that this is only needed for tuning, and more proper value will be selected in the corresponding section.
If square_corner_velocity parameter was changed, revert it back to 5.0. It is not advised to increase it when using the input shaper because it can cause more smoothing in parts - it is better to use higher acceleration value instead.
Restart the firmware: RESTART.
Disable Pressure Advance: SET_PRESSURE_ADVANCE ADVANCE=0.
If you have already added [input_shaper] section to the printer.cfg, execute SET_INPUT_SHAPER SHAPER_FREQ_X=0 SHAPER_FREQ_Y=0 command. If you get "Unknown command" error, you can safely ignore it at this point and continue with the measurements.
Execute the command TUNING_TOWER COMMAND=SET_VELOCITY_LIMIT PARAMETER=ACCEL START=1250 FACTOR=100 BAND=5. Basically, we try to make ringing more pronounced by setting different large values for acceleration. This command will increase the acceleration every 5 mm starting from 1500 mm/sec^2: 1500 mm/sec^2, 2000 mm/sec^2, 2500 mm/sec^2 and so forth up until 7000 mm/sec^2 at the last band.
Print the test model sliced with the suggested parameters.
You can stop the print earlier if the ringing is clearly visible and you see that acceleration gets too high for your printer (e.g. printer shakes too much or starts skipping steps).
