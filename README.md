# prusa-i3-settings

## Maschine Settings
	X (Width): 210
	Y (Depth): 190 
	Z (Height): 180

	Gcode Flavor: Marlin

## Start/End GCode
### Start GCode:

	; Setup Kram
	G21 ;metric values
	G90 ;absolute positioning
	M82 ;set extruder to absolute mode
	M107 ;start with the fan off
	
	; Referenzfahrt + Leveling
	G28 X0 Y0 ;move X/Y to min endstops
	G28 Z0 ;move Z to min endstops
	G29 ;Mesh Leveling  XXXX
	
	; Heizen
	M104 S{material_print_temperature_layer_0} ; set extruder temp
	M140 S{material_bed_temperature_layer_0} ; set bed temp
	M190 S{material_bed_temperature_layer_0} ; wait for bed temp
	M109 S{material_print_temperature_layer_0} ; wait for extruder temp
	
	; Nozzle primen
	G1 Z15.0 F9000 ;move the platform down 15mm
	G92 E0 ;zero the extruded length
	G1 F200 E3 ;extrude 3mm of feed stock
	G92 E0 ;zero the extruded length again
	
	; Default Feed
	G1 F9000
	
	;Put printing message on LCD screen
	M117 Printing...



### End GCode

	; Heizungen aus
	M107
	M104 S0 ;extruder heater off
	M140 S0 ;heated bed heater off (if you have it)
	
	; Letzte Bewegung
	G91 ;relative positioning
	G1 E-1 F300  ;retract the filament a bit before lifting the nozzle, to release some of the pressure
	G1 Z+0.5 E-5 X-20 Y-20 F9000 ;move Z up a bit and retract filament even more
	G28 X0 Y0 ;move X/Y to min endstops, so the head is out of the way
	
	; Teardown
	M84 ;steppers off
	G90 ;absolute positioning
	M104 S0
