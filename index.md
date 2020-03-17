---
layout: content
---

# Linux notes
## Github

[https://github.com/dangduytung/linux](https://github.com/dangduytung/linux){:target="_blank"}

### &#35; Characteristics

- [x] Simple
- [x] Friendly to read

### &#35; Shell script example move file to usb

~~~ bash
#!/bin/sh
# file : viettel_move_app_to_usb.sh
# run on Git Bash : ./viettel_move_app_to_usb.sh (param1: live_iptv/test) (param2: release or not default log)

ROOT_PROJECT='D:\\workspace\\viettel_nextui\\phase1\\windmill_viettel';
# 0. Check input param
if [ -z "$1" ]
  then
    echo "No argument supplied. Need (live_iptv|live|test|test_iptv) (release|debug)";
	exit 1;
fi
# 1. Check exist usb label F: G:
usbLabel='F:';
usbInfo=`df -h | grep $usbLabel`;
if [ "$usbInfo" == "" ] ; then
	echo -e "\e[90mCannot find USB label "$usbLabel;
	echo -e "\e[90mTry USB with label G:";

	usbLabel='G:';
	usbInfo=`df -h | grep $usbLabel`;
	if [ "$usbInfo" == "" ] ; then
		echo -e "\e[31mCannot find USB label "$usbLabel;
		exit 1;
	fi
fi


# 2. Find current build number of project
filename="${ROOT_PROJECT}\\build_number.properties"
n=1
# build_number="2.3.149";
build_number='';
while read line; do
    # echo "Line No. $n : $line"
    if [ $n -gt 1 ]; then
        number="$(cut -d'=' -f2 <<<"$line")"
        # echo "number=$number"
        build_number+="$number."
    fi
n=$((n+1))
done < $filename

# Remove last character (dot unused)
build_number=${build_number::-1}

# Echo build number to console
echo -e "\e[90mbuild_number : $build_number"

# 3. Check name file is current day
name="viettel_new_ui_v"$build_number$"-log(";
if [ $# -eq 2 ]; then
	if [ $2 == 'release' ];then
		name="viettel_new_ui_v"$build_number$"(";
	fi
fi
name+=$(date +%Y%m%d)"_";
#echo $name;

# 4. Check param input: live_iptv, test_iptv...
buildType=$1;

#concat url file with input param
pathFile=${ROOT_PROJECT}'\\_rel\\'${build_number}'\\';
pathFile+="$buildType/*.zip";
# echo "pathFile : $pathFile";

# flag to check print notify out
flag=false;

# 5. Move file to USB and backup old file in USB
for file in $pathFile; do
    # printf -- '%s\n' "${file##*/}"

	if [[ "$file" == *$name* ]];then
		#printf '%s\n' "${file##*/}";
		echo -e "\e[96m${file##*/}";
		
		#! backup file app.zip to app_bak.zip and move new file to app.zip at usb
		if [ -f "$usbLabel\\app.zip" ] ; then
			mv $usbLabel'\\app.zip' $usbLabel'\\app_bak.zip';
		else
			echo -e '\e[36m'$usbLabel'\\app.zip not found.'	
		fi
		
		mv $file $usbLabel'\\app.zip';
		
		flag=true;
	fi
done


# 6. Backup log.txt and remove some file unused
if $flag ; then

	#! remove files log in usb
	rm -rf $usbLabel'\\BOOTEX.LOG';
	rm -rf $usbLabel'\\log.txt.backup';

	fileLog=$usbLabel'\\log.txt';
	if [ -f "$fileLog" ] ; then
		# echo "$fileLog found."
		mv $fileLog $usbLabel'\\log_1.backup';
		#rm -rf $usbLabel'\\log.txt';
	else
		echo -e "\e[36m$fileLog not found."
	fi

	echo -e "\e[32mSuccessfully"
else 
	echo -e "\e[31mFile not found"
fi
~~~
