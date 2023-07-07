## BED MESH & FIRST LAYER

I have invested significant effort in attaining the ideal first layer, and I believe it would be beneficial to share my discoveries in case others are facing comparable challenges. These tips and tricks are not solely my ideas but a checklist gathered from various sources.

![test](https://i.imgur.com/M9eXow1.jpeg)

See this list as a complement to the excellent tuning guide: https://ellis3dp.com/Print-Tuning-Guide/

Although I am using Klicky mod in conjunction with Automatic Z calibration, the majority of this guide is applicable to other types of probes. 

1.To ensure accuracy, setting the appropriate values for mesh_min and mesh_max is important. The Klipper documentation provides an illustration of this point, as seen in the following link: https://imgur.com/a/vIFMCEY. Measure your max and min points 40x40mm in from both the front left corner and rear right corner.

2. To determine your probe offset to the nozzle, first lower your nozzle and make a mark. Next, attach your probe and move it until it's positioned on the spot. Compare the probe's y and x positions to the nozzle's. Finally, add this offset under the [probe] section.

3. Find the correct bicubic_tension, I've tried different values I think it is wise to start around bicubic_tension: 0.2 if you do not have a very warped bed. and increase if your mesh doesn't compensate enough and decrease if you are having over-compensation.

4. Make sure you set a correct relative_reference_index if you are using automatic Z calibration. I recommend setting this to the center of the bed, choosing an appropriate probe count that results in an uneven number, and setting relative_reference_index to the midpoint of your probe count. Ex: probe_count: 5,5 relative_reference_index: 12 ; ( zero-indexed )

5. Make sure your gantry is squared, follow this guide to make sure your gantry is square https://ellis3dp.com/Print-Tuning-Guide/articles/voron_v2_gantry_squaring.html

6. Make sure to turn to set stealthchop_threshold: 0 interpolate: false for all your z drives. This increases accuracy.

7. A probe count higher than 5x5 doesn't really improve anything.

8. Make sure your QGL retry_tolerance is low enough to get consistent results.

9. Make sure your points section under [quad_gantry_level] is correct, mark 4 points 40x40 mm in from the sides and attach your probe and jog your head until the probe is above each mark. Here you need to have the probe coordinates (nozzle + probe offset) contrary to the bed mesh where you should have the nozzle coordinates.

10. Make sure your probe samples_tolerance is low enough to achieve consistency (a nozzle scrub can help to get rid of any residue on the nozzle).

11. In your slicer, set your first layer to 0.24 (using 0.2 layer height)

12. Heat soak your printer before starting a print. More important the higher bed temp you use.

13. Fine adjust your first layer squish using these test prints spread out all over the bed: https://github.com/AndrewEllis93/Print-Tuning-Guide/tree/main/test_prints/first_layer_patches

14. You must not have a LOAD_GCODE_STATE or G28 or G28 Z in your print_start macro after calibrate_z or it will overwrite the z_offset.

15. Set your first layer line width to at least 120 %

16. If you are using Automatic Z offset, set bed_xy_position to the center of the bed.

17. Make sure to do a G28 after QGL and a G28 Z while the nozzle is up to print temp

18. I recommend doing a bed mesh at the start of every print, I use an adaptive bed mesh to speed things up (https://github.com/VGDev1/Voron-V2.4928/blob/main/config/adaptive_bed_mesh.cfg).

19. An adaptive purge is useful before starting to print, you can find the one I am using here https://github.com/VGDev1/Voron-V2.4928/blob/main/config/Adaptive_Purge.cfg

20. If using the Klicky mod, use high-quality magnets of the correct height to ensure great contact while docking. And make sure they are glued in place.

22. Make sure your Z belts (If you have any) are tightened to 140 Hz.

23. Get a high-quality PEI bed and magnetic sticker with tight tolerances (I use OSEQ)

24. Clean your bed with either high-quality dish soap or 99% IPA. I always use 99% IPA for convenience.

25. Do a proper heat soak if printing ABS, I aim for a bed temp derivative of 0.1 of a 30-second period, I use this script for heat soak macro https://github.com/garethky/klipper-voron2.4-config/blob/mainline/printer_data/config/heatsoak.readme.md

26. If printing a lot of ABS, consider Ellis bed fan mod to increase chamber temp. I went from 45-50 degrees to 60-65 degrees chamber temp(my setup https://imgur.com/a/QfpIZoS). Mod: https://github.com/VoronDesign/VoronUsers/tree/master/printer_mods/Ellis/Bed_Fans
