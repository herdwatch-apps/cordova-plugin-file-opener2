
----------

# A File Opener Plugin for Cordova

[![Latest Stable Version](https://img.shields.io/npm/v/@herdwatch/cordova-plugin-file-opener.svg)](https://www.npmjs.com/package/@herdwatch/cordova-plugin-file-opener2) [![Total Downloads](https://img.shields.io/npm/dt/@herdwatch/cordova-plugin-file-opener2.svg)](https://npm-stat.com/charts.html?package=@herdwatch/cordova-plugin-file-opener2)

This plugin will open a file on your device file system with its default application.

```js
cordova.plugins.fileOpener2.open(
    filePath,
    fileMIMEType,
    {
        error : function(){ },
        success : function(){ }
    }
);
```

## Installation

```shell
$ cordova plugin add @hedwatch/cordova-plugin-file-opener2
```

## Requirements

The following platforms and versions are supported by the latest release:

- Android 5.1+ / iOS 9+ / Windows / Electron
- Cordova CLI 7.0 or higher


## fileOpener2.open(filePath, mimeType, options)

Opens a file

### Supported Platforms

- Android 5.1+
- iOS 9+
- Windows
- Electron

### Quick Examples

Open a PDF document with the default PDF reader and optional callback object:

```js
cordova.plugins.fileOpener2.open(
    '/Download/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        }
    }
);
```

__Note on Electron:__ Do not forget to enable Node.js in your app by adding `"nodeIntegration": true` to `platforms/electron/platform_www/cdv-electron-settings.json` file, See [Cordova-Electron documentation](https://cordova.apache.org/docs/en/latest/guide/platforms/electron/index.html#customizing-the-application's-window-options).

### Market place installation
Install From Market: to install an APK from a market place, such as Google Play or the App Store, you can use an `<a>` tag in combination with the `market://` protocol:

```html
<a href="market://details?id=xxxx" target="_system">Install from Google Play</a>
<a href="itms-apps://itunes.apple.com/app/my-app/idxxxxxxxx?mt=8" target="_system">Install from App Store</a>
```
or in code:

```js
window.open("[market:// or itms-apps:// link]","_system");
```

## fileOpener2.showOpenWithDialog(filePath, mimeType, options)

Opens with system modal to open file with an already installed app.

### Supported Platforms

- Android 5.1+
- iOS 9+

### Quick Example

```js
cordova.plugins.fileOpener2.showOpenWithDialog(
    '/Downloads/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        },
        position : [0, 0]
    }
);
```
`position` array of coordinates from top-left device screen, use for iOS dialog positioning.


### Supported Platforms

- Android 5.1+

## fileOpener2.appIsInstalled(packageId, callbackContext)

Check if an app is already installed.

### Supported Platforms

- Android 5.1+

### Quick Example
```javascript
cordova.plugins.fileOpener2.appIsInstalled('com.adobe.reader', {
    success : function(res) {
        if (res.status === 0) {
            console.log('Adobe Reader is not installed.');
        } else {
            console.log('Adobe Reader is installed.')
        }
    }
});
```
---

## SD card limitation on Android

It is not always possible to open a file from the SD Card using this plugin on Android. This is because the underlying  Android library used [does not support serving files from secondary external storage devices](https://stackoverflow.com/questions/40318116/fileprovider-and-secondary-external-storage). Whether or not your the SD card is treated as a secondary external device depends on your particular phone's set up.

---

## Notes

- For properly opening _any_ file, you must already have a suitable reader for that particular file type installed on your device. Otherwise this will not work.


- If you are wondering what MIME-type should you pass as the second argument to `open` function, [here is a list of all known MIME-types](http://svn.apache.org/viewvc/httpd/httpd/trunk/docs/conf/mime.types?view=co)


---


