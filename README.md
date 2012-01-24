# iTunesSync

With iOS 5, Apple introduced wireless syncing of iPhones, iPads and iPods touch. However, you still have to manually click sync...

iTunesSync is my attempt to correct this!

## Manual usage

iTunesSync is a shell script that tells iTunes, via AppleScript (using the `osascript` command) to sync with a given device:

	iTunesSync "<device_name>" [-h|--help]
	  executes an iTunes Sync from the command line on the device
	  <device_name> whose name shall be provided.

	Arguments:
	    -h, --help  : Displays this help.

Example : `iTunesSync "John Doe's iPhone"`.

## Automated usage

With the script, I also provide an example `plist` file.

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
		<key>Label</key>
		<string>net.herbiet.iTunesSync.example.plist</string>
		<key>ProgramArguments</key>
		<array>
			<string>/some/path/to/iTunesSync</string>
			<string>"My Device Name"</string>
		</array>
		<key>StartInterval</key>
		<integer>1800</integer>
	</dict>
	</plist>


Edit it to your needs:

1. Change the first string in the `ProgramArguments` array to point to the location where you have put the script (e.g. `/Users/johndoe/bin/iTunesSync`)

2. Change the second string in the `ProgramArguments` array to the name of the device you want to sync (e.g. `"John Doe's iPhone"`).

3. Change the `StartInterval` value (this is by default 1800 sec or 30 min).

Then place the `plist` file in `~/Library/LaunchAgents/`: you can do a copy or a symbolic link.

For the automated sync to take effect, you can either restart or invoke the following command from the Terminal:

	$ launchctl load net.herbiet.iTunesSync.GuillaumesiPhone.plist 