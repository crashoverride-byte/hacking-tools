#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Existing...\n"
	# Show the cursor
	tput cnorm
	exit 1
}

# Ctrl+C
trap ctrl_c SIGINT

declare -a ports=( $(seq 1 65535) )

function checkPort(){
	(exec 3<> /dev/tcp/$1/$2) 2>/dev/null

	if [ $? -eq 0 ]; then
		echo "port ($2) -> open"
	fi

	exec 3<&-
	exec 3<&-
}

# Hidde the cursor
tput civis

if [ $1 ]; then
	for port in ${ports[@]}; do
		checkPort $1 $port &
	done
else
	echo -e "\n\n[!] Usage: $0 <ip-address>\n"
fi

wait
