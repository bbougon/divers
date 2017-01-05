# Launch mongodb at OS X startup

Create a file call **org.mongo.mongod.plist** in **/Library/LaunchDaemons/**
```bash
sudo vim /Library/LaunchDaemons/org.mongo.mongod.plist
```
Copy this into **org.mongo.mongod.plist**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>org.mongo.mongod</string>
    <key>RunAtLoad</key>
    <true/>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/mongod</string>
        <string>--dbpath</string>
        <string>/data/db</string>
        <string>--logpath</string>
        <string>/var/log/mongodb.log</string>
    </array>
</dict>
</plist>
```

Run the following commands
```bash
sudo launchctl load /Library/LaunchDaemons/org.mongo.mongod.plist  
sudo launchctl start org.mongo.mongod

Check into the log file that mongo has started successfully 
