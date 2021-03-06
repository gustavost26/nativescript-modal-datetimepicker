# nativescript-modal-datetimepicker [![Build Status](https://travis-ci.org/shiv19/nativescript-material-datetimepicker.svg?branch=master)](https://travis-ci.org/davecoffin/nativescript-modal-datetimepicker) [![npm](https://img.shields.io/npm/dt/express.svg)](https://www.npmjs.com/package/nativescript-modal-datetimepicker) [![npm](https://img.shields.io/npm/v/nativescript-material-datetimepicker.svg)](https://www.npmjs.com/package/nativescript-modal-datetimepicker)

[![Twitter URL](https://img.shields.io/badge/twitter-%40MultiShiv19-blue.svg)](https://twitter.com/MultiShiv19)


[![NPM](https://nodei.co/npm/nativescript-modal-datetimepicker.png)](https://nodei.co/npm/nativescript-modal-datetimepicker/)

This plugin is a wrapper around `android.app.DatePickerDialog` for Android, and `UIDatePicker` for iOS.

## Android Screenshots

### Date Picker
<img src="https://github.com/davecoffin/nativescript-modal-datetimepicker/blob/master/assets/datepicker.jpeg?raw=true" height="320" > 

### Time Picker
<img src="https://github.com/davecoffin/nativescript-modal-datetimepicker/blob/master/assets/timepicker.jpeg?raw=true" height="320" > 

## iOS
<img src="https://github.com/davecoffin/nativescript-modal-datetimepicker/blob/master/assets/iosdatepicker.gif?raw=true" height="320" > 

## Installation

```javascript
tns plugin add nativescript-modal-datetimepicker
```

## Configuration 

For android, the clock style can be `clock` or `spinner`
For android, the calendar style can be `calendar` or `spinner`

This can be changed in `App_Resources/Android/values-21/styles.xml`
```xml
<!-- Default style for DatePicker - in spinner mode -->
<style name="SpinnerDatePicker" parent="android:Widget.Material.Light.DatePicker">
    <item name="android:datePickerMode">calendar</item>
</style>

<!-- Default style for TimePicker - in spinner mode -->
<style name="SpinnerTimePicker" parent="android:Widget.Material.Light.TimePicker">
    <item name="android:timePickerMode">clock</item>
</style>
```

## Usage

NativeScript Core

```js

const ModalPicker = require("nativescript-modal-datetimepicker").ModalDatetimepicker;

const picker = new ModalPicker();

// Pick Date
exports.selectDate = function() {
    picker.pickDate({
        title: "Select Your Birthday",
        theme: "light",
        maxDate: new Date()
    }).then((result) => {
        // Note the month is 1-12 (unlike js which is 0-11)
        console.log("Date is: " + result.day + "-" + result.month + "-" + result.year);
        var jsdate = new Date(result.year, result.month - 1, result.day);
    }).catch((error) => {
        console.log("Error: " + error);
    });
};

// Pick Time
exports.selectTime = function() {
    picker.pickTime()
        .then((result) => {
            console.log("Time is: " + result.hour + ":" + result.minute);
        })
        .catch((error) => {
            console.log("Error: " + error);
        });
};

```

## API

`pickDate(options): Promise<{}>;`

Returns a promise that resolves to date object  (Note: the month is 1-12, unlike js which is 0-11)
```js
date: {
    day: number,
    month: number,
    year: number
}
```

`pickTime(options): Promise<{}>;`

Returns a promise that resolves to time object
```js
time: {
    hour: number,
    minute: number
}
```

options conform to the following interface: 
```ts
export interface PickerOptions {
    title?: string, // iOS ONLY: The title to display above the picker, defaults to "Choose A Time" or "Choose A Date"
    theme?: string, // iOS ONLY: light for a light blurry effect, dark for a dark blurry effect - defaults to dark
    maxDate?: Date,
    minDate?: Date,
    startingHour?: number, // Ignored on pickDate()
    startingMinute?: number, // Ignored on pickDate()
    startingDate?: Date // Ignored on pickTime()
}
```

    
## License

Apache License Version 2.0, January 2004
