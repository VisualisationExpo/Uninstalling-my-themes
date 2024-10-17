# Uninstalling-my-themes
By popular demand, now that there's no more updates to AquaLickX in this current form.

# Uninstalling my themes

## Applies to all themes that I’ve made that require to have disabled SIP and additional ‘authenticated-root disable'

# Look in each repository and locate defaults .car files
# either as a compressed zip file or unpacked as their name, like `Aqua.car` , `VibrantLight.car`, `DarkAqua.car`, `VibrantDark.car`

## You’ll need to apply the same method of mounting your system disk.
**Leave SIP disabled and ‘authenticated-root’ disabled too until you’ve completed these steps for uninstalling.**

_**Basically it’s all about copying in default .car files instead of themed files**_

> text edited and snagged from jslegendre [https://github.com/jslegendre/ThemeEngine]()

Note for Big Sur, Monterey and Ventura users:
If you want to edit system .car files it is no longer enough to remount the boot volume as read/write.
You will need to follow the steps below:

1. Disable SIP and authenticated-root:
In recovery mode, open Terminal and enter

`csrutil disable`

`csrutil authenticated-root disable`

Then reboot into macOS.

2. Identify the System Volume Disk Device Name
Run the mount command in Terminal to identify the devices of your system volume snapshot. Look for the device mounted at “/“, which identifies the system volume disk.  In the following example, this disk is `/dev/disk4s5s1`.
```
/dev/disk4s5s1 on / (apfs, sealed, local, read-only, journaled)
devfs on /dev (devfs, local, nobrowse)
/dev/disk4s4 on /System/Volumes/VM (apfs, local, noexec, journaled, noatime, nobrowse)
/dev/disk4s2 on /System/Volumes/Preboot (apfs, local, journaled, nobrowse)
/dev/disk4s1 on /System/Volumes/Data (apfs, local, journaled, nobrowse)
```
To get the actual name of the system volume disk, remove the final “sX” from the device. In the preceding example, the name of the system volume disk is `/dev/disk4s5`.

3. Mount a Live Version of the System Volume
Run the mount command in Terminal to mount the system volume disk to a temporary location. When running the mount command, always include the nobrowse mount option to prevent Spotlight from indexing the volume.

`mkdir /Users/<YOUR USER NAME>/livemount`

`sudo mount -o nobrowse -t apfs  /dev/disk4s5 /Users/<YOUR USER NAME>/livemount`

4. `cd into the place where your AquaLick is downloaded to. "AquaLickX-master” or the like`
5. `Find the default “.car” files`
6. `sudo cp Aqua.car ~/livemount/System/Library/CoreServices/SystemAppearance.bundle/Contents/Resources/`
7. `sudo cp VibrantLight.car ~/livemount/System/Library/CoreServices/SystemAppearance.bundle/Contents/Resources/`
8. `sudo cp DarkAqua.car ~/livemount/System/Library/CoreServices/SystemAppearance.bundle/Contents/Resources/`
9. `sudo cp VibrantDark.car ~/livemount/System/Library/CoreServices/SystemAppearance.bundle/Contents/Resources/`
10. Bless your livemount directory with `sudo bless --mount /Users/<YOUR USER NAME>/livemount --bootefi --create-snapshot`
11. If you're on an Apple silicon Mac then issue this `bless` command instead

`sudo bless --mount "$HOME/livemount/System/Library/CoreServices/" --setBoot --create-snapshot`

# NOW THE EXCITING PART IF YOU’VE COPIED DEFAULT `.car` files in as you would a theme. There’s no hocus pokus to this operation.

## This time you boot to your desktop to check that the default theme for both light and dark mode are in place and no themed assets are left (traffic lights or scrollbars)

## Shutdown your Mac if it’s an Apple silicon based Mac. Or reboot and hold down CMD+R on an Intel Mac.

## An Intel Mac would boot to Recovery mode with CMD+R held down.

## An Apple silicon based Mac is to be shut down
**My advice is to check how to get to the recovery screen on *your* specific Mac model**

### An M2 or M1 Mac mini has to keep the power button held for a couple of seconds or just keep an eye on the power light on the front on the Mac mini.. when the light changes a little you can let go of the power button and be greeted with the recovery screen.

# Now that the recovery screen is shown you ought to know by know how to get to the actual fun part of that screen.. I won’t waste space explaining

1. When you’re past the part of entering the code for your user.
2. Enter Disk Utility
3. From the sidebar in Disk Utility select your boot drive. Usually the top most drive
4. Go to the menu bar
5. Select View menu -> Show All Devices
6. Go back to the Disk Utility sidebar and probably expand the disk tree or if already expanded to all disks… 
7. … choose the second Macintosh HD drive listed and check the bottom right hand side of Disk Utility …
8. You’ll notice an "APFS Snapshots" list
9. Take a look and see that you ought to have some `bless` snapshot entries there. You could have 4 bless commands or more - depending on how many times you’ve used the bless command when copying in stuff.
10. Select all but the top and bottom of the entries and delete them.
11. Reboot to macOS desktop.
12. Re-enable SIP once you’re certain everything is OK 


Terminal commands to harden your Mac again.
`csrutil enable` and `csrutil authenticated-root enable`

**See.. no hocus pokus. Just keep backups .. you have a responsibility for your own Mac system. I did my part**
