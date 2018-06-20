#JINS MEME Controller Library
====

##Overview

- Event detection of the first orientation and the number of consecutive times when the neck is swung right and left or up and down in short intervals
- Event detection of the first orientation and the number of consecutive times when the line of sight is moved right and left or up and down in short intervals
- Measurement of absolute value of neck angle (needs no calibration)

## Description
You can use this library to forward a page, send an intent to  some other application, or issue a WebHook.
 Of course, the number of consecutive times == 1 frequently occurs in everyday life, use more than 2 as a trigger. 
The point is to move continuously at short intervals. This behavior is not usually done in everyday life,
 so it can be extracted with less misjudgment. 

## Requirement
- cordova >= 6.5
- com.jins_jp.meme.plugin >= 1.2 (or monaca-plugin-jins-meme >= 1.3)

## Usage

- A client_id and secret in index.html are needed for JINS MEME SDK verification.
- Include following line.
> <script src="jmctrllib.js"></script>

### Swing and Eye move events

- Put methods that fire controll events.
Put following lines in cordova.plugins.JinsMemePlugin.startDataReport() callback.
```
 jmoplib.getSequentialSwing(data); 
 jmoplib.getSequentialEyeMove(data);
```

- Listen the controll events
Put following lines in somewhere.
```
// Lateral swings
document.addEventListener('jmoplib_swing_lat', function(e) {
    // do something
    //console.log("lat directoin:" + e.detail.direction + " times:" + e.detail.count);
});
// Longitudinal swings
document.addEventListener('jmoplib_swing_long', function(e) {
    // do something
    //console.log("lng directoin:" + e.detail.direction + " times:" + e.detail.count);
});
// Lateral eye movements
document.addEventListener('jmoplib_eyemove_lat', function(e) {
    // do something
    //console.log("lat directoin:" + e.detail.direction + " times:" + e.detail.count);
});
// Lateral eye movements
document.addEventListener('jmoplib_eyemove_long', function(e) {
    // do something
    //console.log("lng directoin:" + e.detail.direction + " times:" + e.detail.count);
});
```
These events have CustomEvent interface ('e').
-- e.detail.direction: Which direction did it occur at first time? (right/up == 1, left/down == -1) 
-- e.detail.count: How many times did it occur?

### Tilt calculation
- Put following lines in cordova.plugins.JinsMemePlugin.startDataReport() callback.
 ```
 var tilt = jmoplib.calcTilt(data);
 ```

## Licence

MIT

## Author

[jins-tkomoda](https://github.com/jins-tkomoda)
