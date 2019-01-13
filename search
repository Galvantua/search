#!/bin/bash

searchpattern=$1
results=$(locate "$searchpattern")

if [ "$results" = "" ] 
then
	echo "The results of locate do not exist"
elif [ "$results" != "" ]
then
	echo "The results of locate are below:"
	echo "$results"
	exit
fi
echo $?
search() {
	#$1=search criteria
	ls -laR | grep "$1"
}
while true; do
dirarray=$(ls -a)
for((i=2;i<"${#dirarray[@]}";i++)); do #start at 2 to avoid .. and .
	if [ -d "${dirarray[i]}" ]; then
		cd "${dirarray[i]}" || exit
		search "$searchpattern"
		while true ; do
			read -rp "Is this what you are looking for? " yn
			case $yn in
				[Yy]*)  break;;
				[Nn]*)  cd ..;
						break;;
				*) echo "Please enter yes or no ";;
			esac
		done
	fi
done
done
