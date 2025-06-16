push:
	scp -rO *.{cfg,conf} pi@voron-red.local:printer_data/config
	curl -X POST http://voron-red.local/printer/gcode/script?script=firmware_restart

pull:
	scp -rO 'pi@voron-red.local:printer_data/config/*.{cfg,conf}' .
	mkdir -p printer-backups/
	mv printer-????????_??????.cfg printer-backups/

clear_resonance:
	ssh pi@voron-red.local rm '/tmp/resonances*'

# To generate resonance data attach accelerometer and run:
# TEST_RESONANCES AXIS=X
# TEST_RESONANCES AXIS=Y
test_resonances:
	curl -X POST http://voron-red.local/printer/gcode/script?script=TEST_RESONANCES%20AXIS%3DX
	curl -X POST http://voron-red.local/printer/gcode/script?script=TEST_RESONANCES%20AXIS%3DY

calibrate_resonance:
	ssh pi@voron-red.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png'
	ssh pi@voron-red.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_*.csv -o /tmp/shaper_calibrate_y.png'

pull_resonance_data:
	mkdir -p resonances/
	scp -rO 'pi@voron-red.local:/tmp/resonances*.csv' resonances/
	scp -rO 'pi@voron-red.local:/tmp/shaper_calibrate_?.png' resonances/

run_input_shaping: test_resonances calibrate_resonance pull_resonance_data

pushks:
	scp -rO KlipperScreen.conf pi@voron-red.local:printer_data/config
	curl -X POST http://voron-red.local/machine/services/restart?service=KlipperScreen