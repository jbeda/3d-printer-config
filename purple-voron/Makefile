push:
	scp -rO *.{cfg,conf} pi@voron-purple.local:printer_data/config
	curl -X POST http://voron-purple.local/printer/gcode/script?script=firmware_restart

pull:
	scp -rO 'pi@voron-purple.local:printer_data/config/*.{cfg,conf}' .
	mkdir -p printer-backups/
	mv printer-????????_??????.cfg printer-backups/

clear_resonance:
	ssh pi@voron-purple.local rm '/tmp/resonances*'

# To generate resonance data attach accelerometer and run:
# TEST_RESONANCES AXIS=X
# TEST_RESONANCES AXIS=Y
# Ideally this will return when the command is done but I get a gateway timeout.
# Need to muck with nginx config to avoid that and fully automate this.
test_resonances:
	curl -X POST http://voron-purple.local/printer/gcode/script?script=TEST_RESONANCES%20AXIS%3DX
	curl -X POST http://voron-purple.local/printer/gcode/script?script=TEST_RESONANCES%20AXIS%3DY

calibrate_resonance:
	ssh pi@voron-purple.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png'
	ssh pi@voron-purple.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_*.csv -o /tmp/shaper_calibrate_y.png'

pull_resonance_data:
	mkdir -p resonances/
	scp -rO 'pi@voron-purple.local:/tmp/resonances*.csv' resonances/
	scp -rO 'pi@voron-purple.local:/tmp/shaper_calibrate_?.png' resonances/

run_input_shaping: test_resonances calibrate_resonance pull_resonance_data

pushks:
	scp -rO KlipperScreen.conf pi@voron-purple.local:printer_data/config
	curl -X POST http://voron-purple.local/machine/services/restart?service=KlipperScreen