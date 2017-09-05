# FlagSecureSample
A simple barebones app for testing Android window `FLAG_SECURE` functionality.

Use this app for testing pages/windows that are marked secure by `FLAG_SECURE` window flag layout parameter.

Check the Releases tab for builds for the Secure and Not Secure version of the app.

## How to Programmatically Check For Secure Screen
See the StackOverflow question: [How to query FLAG_SECURE from current APK screen via command line?](https://stackoverflow.com/questions/45928313/how-to-query-flag-secure-from-current-apk-screen-via-command-line)

Whether or not the current Android screen is secure (`FLAG_SECURE`) can be found by running

```shell
adb shell dumpsys SurfaceFlinger | grep "secureVis" | tr "," "\n" | tr -s ' ' | grep "secureVis" | cut -d"=" -f2
```

which will return a boolean of `0` for not secure, or `1` for secure.

The SurfaceFlinger service reports a `secureVis` value which gives the secure flag state.

`isSecure` may seem like the right value based on its name, but it is not and always shows `1` for some reason, possibly just saying that the device supports secure pages in general.

This seems to be the only solution (as of yet), after parsing through the entire `dumpsys` output and looking at file diffs between secure and not secure versions of the same barebones app.
