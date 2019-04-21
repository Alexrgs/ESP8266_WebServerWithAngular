# ESP8266_WebServerWithAngular
ESP8266 AP mode serving a full Angular page 

## Preparing the Arduino IDE
1. Install the ESP8266 on yolur IDE more info at: [Here](https://github.com/esp8266/Arduino) or [here](https://learn.sparkfun.com/tutorials/esp8266-thing-hookup-guide/installing-the-esp8266-arduino-addon )
1. Install the SPIFFS [uploader](https://github.com/esp8266/arduino-esp8266fs-plugin)

## Preparing the Angular app
1. Intall node To get Node.js, go to [nodejs.org](nodejs.org).
1. Install Angular CLI ```npm install -g @angular/cli```
1. Create a new angular app  ```ng new my-app```
1. Build the app using ```ng build --base-href ./ --prod - --output-hashing none``` (it will remove the hash and change the base href to ./) PS: it's nessessary due the SPIFFS limit of 32 bytes file names
1. Install [7-Zip](https://www.7-zip.org/)
1. Create a .bat file named compress.bat inside the app distribution folder
1. Open the file and paste the folowing code: 
```
@echo off
cd /d %~dp0
rem 7z.exe path
set sevenzip=
if "%sevenzip%"=="" if exist "%ProgramFiles(x86)%\7-zip\7z.exe" set sevenzip=%ProgramFiles(x86)%\7-zip\7z.exe
if "%sevenzip%"=="" if exist "%ProgramFiles%\7-zip\7z.exe" set sevenzip=%ProgramFiles%\7-zip\7z.exe
if "%sevenzip%"=="" echo 7-zip not found&pause&exit
set extension=.*
for %%a in (*%extension%) do "%sevenzip%" a -mx=9 -tgzip "%%~a.gz" "%%a"
pause
```
1. run the conpress.bat it will compact the files individualy in the gzip format
1. Now you have a compressed version of the app 



