# Analysis of the doorbell

## Preparations

Took related android app APK to get details about communication:
https://apkcombo.com/de/philips-welcomeeye/com.extel.philipswelcomeeye/download/apk

Reverse Engineered with:
http://www.javadecompilers.com/apk

Extract all files and open into vscode, installed Java plugins.

## Code Understanding

At start working lot with search functionality. For example searched "bell", found the key of the door bell:
public static final int key_door_bell = 2131820944;
