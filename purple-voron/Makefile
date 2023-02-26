push:
	scp -rO *.{cfg,conf} pi@voron-purple.local:printer_data/config
	curl -X POST http://voron-purple.local/printer/gcode/script?script=firmware_restart

pull:
	scp -rO 'pi@voron-purple.local:printer_data/config/*.{cfg,conf}' .
	mkdir -p printer-backups/
	mv printer-????????_??????.cfg printer-backups/