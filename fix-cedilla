#!/bin/bash
#
# fix-cedilla
#
# This is a very simple script to configure your personal ".XCompose" file and
# your environment so that typing 'c will generate a cedilla c instead of an
# accented c.
#
# For further information, visit:
# http://github.com/marcopaganini/gnome-cedilla-fix
#
# (C) Marco Paganini <paganini@paganini.net>

LANG=${LANG:=en_US.UTF-8}
COMPOSE_DIR="/usr/share/X11/locale"
USER_COMPOSE="$HOME/.XCompose"
BOLD=$(tput bold)
RESET=$(tput sgr0)

PROGNAME="${0##*/}"

# Find compose file for the current language.
system_compose=${COMPOSE_DIR}/$(sed -ne "s/^\([^:]*\):[ \t]*$LANG/\1/p" <"${COMPOSE_DIR}/compose.dir" | head -1)
if [ -z "${system_compose}" ]; then
  echo >&2 "${PROGNAME} error: Unable to find a system compose file for your system language (${LANG})"
  exit 1
fi

if [ ! -s "${system_compose}" ]; then
  echo >&2 "${PROGNAME} error: Unable to open system Compose file: ${system_compose}"
  exit 1
fi

if [ -s "${USER_COMPOSE}" ]; then
  echo >&2 "${BOLD}*** WARNING: ***${RESET}"
  echo >&2 "A file named ${USER_COMPOSE} already exists."
  echo >&2 "Saving original to ${USER_COMPOSE}.ORIGINAL"
  echo >&2
  rm -f "${USER_COMPOSE}.ORIGINAL"
  cp -f "${USER_COMPOSE}" "${USER_COMPOSE}.ORIGINAL"
fi

# Save a copy of the system Compose file into .XCompose, replacing
# all ocurrences of accented-c by cedilla-c
sed -e 's/\xc4\x87/\xc3\xa7/g' \
    -e 's/\xc4\x86/\xc3\x87/g' <"${system_compose}" >"${USER_COMPOSE}"

cat <<EOM
${BOLD}System configuration changed.${RESET}

Please log out of your X session and re-login to effect changes.
You may need to restart your X server if a simple logout/login does not work.

To revert the system to the previous state, type the following command:

  rm "${USER_COMPOSE}"

If things don't work after a reboot, make sure your Input Method is configured
to "Auto" in the Gnome Settings.

Operation complete.
EOM
