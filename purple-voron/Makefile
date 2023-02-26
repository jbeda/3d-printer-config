push:
	scp -rO *.{cfg,conf} pi@voron-purple.local:printer_data/config
	curl -X POST http://voron-purple.local/printer/gcode/script?script=firmware_restart

pull:
	scp -rO 'pi@voron-purple.local:printer_data/config/*.{cfg,conf}' .
	mkdir -p printer-backups/
	mv printer-????????_??????.cfg printer-backups/

clear_resonance:
	ssh pi@voron-purple.local rm '/tmp/resonances*'

calibrate_resonance:
	ssh pi@voron-purple.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_*.csv -o /tmp/shaper_calibrate_x.png'
	ssh pi@voron-purple.local '~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_*.csv -o /tmp/shaper_calibrate_y.png'

pull_resonance_data:
	mkdir -p resonances/
	scp -rO 'pi@voron-purple.local:/tmp/resonances*.csv' resonances/
	scp -rO 'pi@voron-purple.local:/tmp/shaper_calibrate_?.png' resonances/
