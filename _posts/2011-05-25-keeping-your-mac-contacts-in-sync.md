---
layout: post
title: Keeping your Mac contacts in sync with Gmail.
---

A few days ago, I was struggling to find a way to keep my contacts in sync between my Mac and Gmail.

I chose Gmail as my central point to keep contacts. I sync my iPhone to it using an Exchange connection and started looking for a way to keep Gmail in sync on Mac since I migrated from Gmail web interface to Mail.app.

After seeing many applications that provided this kind of sync, some paid, some with so many features that I didn't need. I found a way to keep it in sync without relying on external apps or third-party tools.

The solution uses MacOS own Address Book and iSync functionality for Gmail sync.

In my opinion, the best way to first sync contacts without all merge problems is to merge them "by hand". Choose one of the sides (Gmail or Address Book) and keep your contacts there, clear the other side(remove all contacts) then do the sync.

**Remember to backup your contacts from Address Book and Gmail**

The first step is to configure Address Book Gmail sync. This is in the preferences:

<img src="/images/2011-05-25-keeping-your-mac-contacts-in-sync/AddressBook_prefs.png" alt="Preferences" class="center">

<img src="/images/2011-05-25-keeping-your-mac-contacts-in-sync/AddressBook_prefs_2.png" alt="Preferences" class="center">

Then, start iSync and in it's preferences, check "Show status in menu bar" if you want it to display the sync (spinning arrows). This is not needed if you follow the next steps to enable automatic sync but allows one to manually sync the contacts.

<img src="/images/2011-05-25-keeping-your-mac-contacts-in-sync/iSync.png" alt="iSync" class="center">

<img src="/images/2011-05-25-keeping-your-mac-contacts-in-sync/iSync_prefs.png" alt="iSync Preferences" class="center">

<img src="/images/2011-05-25-keeping-your-mac-contacts-in-sync/iSync_menubar.png" alt="iSync menu bar" class="center">

Now, on the geeky part. iSync does not sync automatically in timed intervals. To do this, you will need to create a LaunchAgent. This is a plist file similar to a XML containing the arguments to be run and the running interval.

To create this, fire up your text editor and create a file with the following content:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>Label</key>
        <string>com.carlosedp.iSyncAutoRun</string>
        <key>ProgramArguments</key>
        <array>
            <string>/System/Library/PrivateFrameworks/GoogleContactSync.framework/Versions/A/Resources/gconsync</string>
            <string>--sync</string>
            <string>com.google.ContactSync</string>
        </array>
        <key>RunAtLoad</key>
        <false/>
        <key>StartInterval</key>
        <integer>1800</integer>
    </dict>
    </plist>
```

The parameter `StartInterval` is set to 1800 seconds(30 minutes).

Save it in: `~/Library/LaunchAgents/com.carlosedp.iSyncAutoRun.plist`

This will not automatically run for the current session, only after a reboot. If you want to test it and use without rebooting, drop into the console and run:

    launchctl load ~/Library/LaunchAgents/com.carlosedp.iSyncAutoRun.plist

Now, iSync will keep your contacts in sync every 30 minutes. In case you want to change the interval, set the `StartInterval` to the selected value and reboot.


