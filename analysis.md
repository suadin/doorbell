# Analysis of the doorbell

## Preparations

Took related android app APK to get details about communication:
https://apkcombo.com/de/philips-welcomeeye/com.extel.philipswelcomeeye/download/apk

Reverse Engineered with:
http://www.javadecompilers.com/apk

Extract all files and open into vscode, installed Java plugins.

## Code Understanding

At start working lot with search functionality. For example searched `bell`, found the key of the door bell:
```
public static final int key_door_bell = 2131820944;
```

If search `key_door_bell` than find lot of matches, as well whehere that key is used:
```
public String getAlarmEventName(Context context, int i, int i2, String str, String str2) {
  switch (i) {
    ...
    case 7:
      return context.getString(R.string.key_door_bell);
```

Id search for the method `getAlarmEventName`, found interesting classes like `PushHelper`, `AlarmHelper`, `AlarmMessage`. Btw. please avoid using `Helper` as suffix for your classes, thats meaningless.

