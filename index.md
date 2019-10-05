---
layout: content
---

# Linux notes
## Github

[https://github.com/dangduytung/linux](https://github.com/dangduytung/linux){:target="_blank"}

### Characteristics

- [x] Simple
- [x] Friendly to read

### Shell script example move file to usb

~~~ bash
#!/bin/sh  
# file : viettel_move_app_to_usb.sh
# run ./viettel_move_app_to_usb.sh (live_iptv/test)

#Check exist usb
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


#check name file is current day
version="2.0.147";

name="viettel_new_ui_v"$version$"-log(";
name+=$(date +%Y%m%d)"_";
#echo $name;

#param input: live_iptv, test_iptv...
buildType=$1;

#concat url file with input param
pathFile='D:\\workspace\\viettel_nextui\\phase1\\windmill_viettel\\_rel\\'$version'\\';
pathFile+="$buildType/*.zip";
#echo $pathFile;


#flag to check print notify out
flag=false;


for file in $pathFile; do
    #printf -- '%s\n' "${file##*/}"

	if [[ "$file" == *$name* ]];then
		#printf '%s\n' "${file##*/}";
		echo -e "\e[96m${file##*/}";
		
		#! backup file app.zip to app_bak.zip and move new file to app.zip at usb
		mv $usbLabel'\\app.zip' $usbLabel'\\app_bak.zip';
		mv $file $usbLabel'\\app.zip';
		
		flag=true;
	fi
done


if $flag ; then

	#! remove files log in usb
	rm -rf $usbLabel'\\BOOTEX.LOG';
	rm -rf $usbLabel'\\log.txt.backup';

	fileLog=$usbLabel'\\log.txt';
	if [ -f "$fileLog" ]
	then
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
