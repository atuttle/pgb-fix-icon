# pgb-fix-icon

There's this [shitty bug in Phonegap Build][bug]. Android builds use the HDPI icon and splash screen on XHDPI devices.

This script fixes the icon, recompiles the APK, re-signs it (prompting you for your keystore passwords & alias), and re-[zipaligns][za] it.

## Install

    npm install -g pgb-fix-icon

## Usage

```bash
$ pgb-fix-icon [options]

Options:

  -h, --help               output usage information
  -V, --version            output the version number
  -i, --in-file <file>     The APK that needs to be un-fucked
  -o, --out-file <file>    The APK file to write when done
  -c, --config-xml <file>  Your app's config.xml
  -k, --keystore <file>    Signing keystore
```

## Example

```bash
$ pgb-fix-icon -i MyAppFromPGB.apk -o MyApp.apk -c config.xml -k ~/.android/MyCompany.keystore
```

After the apk has been unpacked, fixed, and re-packed, it will prompt you for your keystore's storepass, keypass, and alias, and use these to re-sign the re-packaged APK.

## Requirements

* Node.js
* jarsigner (comes with Java)
* [apktool][apktool] (hint: you need two downloads: the jar file (listed as all-platforms), and your platform-specific download as well.)
* [zipalign][za]

## TODO

* Switch CLI libraries -- (apparently commander.js doesn't work well since node 0.8? it crashes if I try to use masked prompts for passwords)

## License

MIT License


[bug]: https://github.com/phonegap/build/issues/9
[za]: http://developer.android.com/tools/help/zipalign.html
[apktool]: https://code.google.com/p/android-apktool/