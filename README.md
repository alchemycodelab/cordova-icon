# @blvz/cordova-icon

[cordova-icon](https://github.com/AlexDisler/cordova-icon) fork + updates.
Uses [sharp](https://github.com/lovell/sharp/) instead of ImageMagick.

<img src="cordova-icon-resize.png"/>

Automatic icon resizing for Cordova. Create an icon in the root folder of your Cordova project and use cordova-icon to automatically resize and copy it for all the platforms your project supports (currenty works with iOS, Android, Windows 10 and OSX).

### Installation

```bash
$ yarn add --dev '@blvz/cordova-icon'
```

### Requirements

- At least one platform was added to your project ([cordova platforms docs](http://cordova.apache.org/docs/en/edge/guide_platforms_index.md.html#Platform%20Guides))
- Cordova's config.xml file must exist in the root folder ([cordova config.xml docs](http://cordova.apache.org/docs/en/edge/config_ref_index.md.html#The%20config.xml%20File))

### Usage

Create an `icon.png` file in the root folder of your cordova project.
You can provide a platform-specific icon by naming it `icon-[platform].png`
(e.g `icon-android.png`, `icon-ios.png`).
Then run:

     $ yarn exec cordova-icon

You also can specify manually a location for your `config.xml` or `icon.png`:

     $ yarn exec cordova-icon --config=config.xml --icon=icon.png

For good results, your file should be:

- square
- for Android and iOS, at least 1024\*1024px
- for Windows, at least 1240\*1240px

#### Notes:

- Your `config.ml` file will not be updated by the tool (because images are automatically created in the good folders)
- Therefore, in your `config.xml`, be sure to remove all lines looking like `<icon src="res/android/ldpi.png" density="ldpi" />`

### Creating a cordova-cli hook

Since the execution of cordova-icon is pretty fast, you can add it as a cordova-cli hook to execute before every build.
To create a new hook, go to your cordova project and run:

    $ mkdir hooks/after_prepare
    $ vi hooks/after_prepare/cordova-icon.sh

Paste the following into the hook script:

    #!/bin/bash
    yarn exec cordova-icon

Then give the script +x permission:

    $ chmod +x hooks/after_prepare/cordova-icon.sh

That's it. Now every time you `cordova build`, the icons will be auto generated.

### Splash screens

Check out [cordova-splash](https://github.com/blvz/cordova-splash)

### License

MIT
