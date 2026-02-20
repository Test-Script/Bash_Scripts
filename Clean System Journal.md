==========================================================================================================                                  Clean Systemd Journal
==========================================================================================================

#!/bin/bash

if command -v journalctl >/dev/null 2>&1; then
  log "Vacuuming journal logs..."
  journalctl --vacuum-time=7d
fi
