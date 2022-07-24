# How to backup (import/export) settings for an app

*To sync settings for an app between different computers, check out the [Syncalicious](https://github.com/zenangst/Syncalicious) app or the [Mackup](https://github.com/lra/mackup) command-line tool. You can also use [Mackup](https://github.com/lra/mackup) to export and import app settings.*

For the next steps, you will need to be familiar with the [command-line](https://macpaw.com/how-to/use-terminal-on-mac).

## Export

You first need to find the bundle identifier of the app. Replace `AppName` with the app's name and run the following command:

```sh
osascript -e 'id of app "AppName"'
```

Then run the following command with the correct bundle identifier and app name:

```sh
defaults export BUNDLE_IDENTIFIER APP_NAME.plist
```

Example:

```sh
defaults export com.sindresorhus.Velja Velja.plist
```

You now have a `Velja.plist` file with all the data and settings for this app. You can either store this file in a safe place as a backup or use it to import the settings into another computer.

## Import

Make sure the app is not running.

Run the following command:

```sh
defaults import BUNDLE_IDENTIFIER APP_NAME.plist
```

Example:

```sh
defaults import com.sindresorhus.Velja Velja.plist
```

Then restart your computer to ensure the settings are correctly applied.
