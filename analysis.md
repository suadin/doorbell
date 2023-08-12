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

If search `key_door_bell` than find lot of matches, as well where that key is used:
```
public String getAlarmEventName(Context context, int i, int i2, String str, String str2) {
  switch (i) {
    ...
    case 7:
      return context.getString(R.string.key_door_bell);
```

Search for the method `getAlarmEventName`, found classes like `PushHelper`. Btw. please avoid using `Helper` as suffix for your classes.

We are interested into parameter `i==7`, therefore we focus on input of second parameter:
* `PushHelper`: `alarmMessageInfo.getAlarmEvent()`
* `DeviceAlarmDetailActivity`: `intExtra` -> `= getIntent().getIntExtra(TYPE, 2);` -> `TYPE = "intent_type"`
* `AlarmInfoAdapter`: `qvAlarmMsgItem.getEvent()`

An adapter usually translates message between two systems, therefore the third usage gets my interest:
* `class QvAlarmMsgItem` contains properties like `alarmId`, `alarmState`, `sensorChannel`, ...
* `new QvAlarmMsgItem` has two matches: `LtAlarmManager`, `QvAlarmCore` (another bad suffix `...Manager`)

Both are doing similar things, they iterate over a list. One over `QvLtPushBean` elements, the other over `AlarmListQueryResp.AlarmItem` elements.

In that way the code understanding will continue.

## Features

After code understanding we are aware about which features are supported by that android app and which features we could integrate into home assist.

Currently a possible & useful feature could be:
* recognition of door bell activation
* ...
