cd ios
rm -rf ~/Library/Developer/Xcode/DerivedData
pod install --verbose
cd ..
npx react-native start --reset-cache
npx react-native run-ios


📌 Difference Between NSLog and os_log in iOS Development
Both NSLog and os_log are used for logging in iOS/macOS applications, but they have key differences in performance, visibility, and system integration.

🔍 NSLog
✅ Features
Simple and easy to use
Outputs to Xcode Console and system logs
Always logs messages in production (even in release builds)
Slow performance (not optimized for high-volume logging)
No structured logging (plain text format)
❌ Drawbacks
Not optimized for performance; can slow down apps.
Always logs messages, even in production (security risk).
Cannot categorize logs (all logs appear in the same stream).
Less control over log filtering.
📌 Example Usage
objective
Copy
Edit
NSLog(@"This is a debug message.");
NSLog(@"🚀 Alarm scheduled: %@", alarmID);
📌 Where to View NSLog Logs
Xcode Console (Visible when running the app)
Console.app (Search for your app's bundle identifier)
🔥 os_log (Recommended)
✅ Features
More efficient and optimized for performance.
Does NOT log in release builds unless explicitly enabled.
Structured logging (categories, filtering, and severity levels).
Better security (supports privacy controls).
Faster than NSLog, since logs can be collected asynchronously.
✅ Logging Levels
.default – Standard logs (general debug info)
.info – Informational messages
.debug – Debug-level logs
.error – Error messages
.fault – Critical errors (crashes, memory corruption)
📌 Example Usage
swift
Copy
Edit
import os

let logger = OSLog(subsystem: "com.example.MyApp", category: "Alarm")

os_log("🚀 Alarm scheduled: %{public}@", log: logger, type: .info, alarmID)
os_log("❌ Alarm failed due to error: %{public}@", log: logger, type: .error, error.localizedDescription)
📌 Where to View os_log Logs
Xcode Console (Only in Debug mode)
Console.app → Search for "subsystem" name
Terminal (Live Logs)
sh
Copy
Edit
log stream --predicate 'subsystem == "com.example.MyApp"' --style compact
🚀 Key Differences
Feature	NSLog	os_log (Recommended)
Performance	Slower (Blocks Main Thread)	Faster (Optimized for Background)
Security	Always logs (Even in production)	Can be disabled in Release builds
Filtering	No categories or filtering	Supports structured categories
Visibility	Xcode Console & Console.app	Xcode, Console.app, Terminal
Logging Levels	No levels (Only prints text)	Supports .info, .debug, .error, .fault
Output to Release Builds	Always logs	Can be disabled in Release
📌 When to Use What?
Scenario	Best Choice
Simple debugging during development	NSLog
High-performance logging	os_log
Categorized and structured logs	os_log
Production apps (for debugging issues)	os_log
Large-scale apps with many logs	os_log
🔥 Final Recommendation
✅ Use NSLog for quick debugging.
✅ Use os_log for production-ready, secure, and efficient logging. 🚀



🔑 Key Reasons for restoreAlarms
1️⃣ Persistence After App Restart
iOS does not automatically restore pending notifications when an app restarts.
If a user sets an alarm and then closes & reopens the app, the alarm would be lost unless we restore it manually.
2️⃣ Persistence After Device Reboot
If a user restarts their device, all scheduled local notifications are cleared by iOS.
restoreAlarms helps re-register these alarms from UserDefaults when the app starts again.
3️⃣ Ensuring Background Alarm Execution
If an alarm is scheduled and the app is closed by iOS due to inactivity, iOS may cancel pending alarms.
restoreAlarms helps restore and re-trigger any lost alarms when the app is opened again.
🔍 How It Works
On App Launch (didFinishLaunchingWithOptions), we call restoreAlarms to check for previously saved alarms in UserDefaults.
If found, we reschedule each alarm using scheduleAlarm, ensuring it is set again.
This ensures that users don't lose their alarms even if they close, restart, or reboot their device.
🔧 Example Scenario Without restoreAlarms
❌ Issue: Alarm Lost After App Restart
User sets an alarm for 7:00 AM.
The user closes the app before the alarm rings.
iOS clears the alarm when the app is closed (if not using background mode).
The alarm never rings! ❌
✅ Example Scenario With restoreAlarms
🎉 Solution: Alarm Works Even After Restart
User sets an alarm for 7:00 AM.
The user closes the app.
On next app launch, restoreAlarms reloads all saved alarms and reschedules them.
The alarm rings at 7:00 AM as expected! ✅
📌 When Should You Call restoreAlarms?
✅ Inside AppDelegate.mm:

objective
Copy
Edit
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self restoreAlarms]; // 🔄 Restores alarms when the app launches
    return YES;
}
✅ Inside applicationWillTerminate:

objective
Copy
Edit
- (void)applicationWillTerminate:(UIApplication *)application {
    [self restoreAlarms]; // 💀 Ensures active alarms are saved before termination
}
🚀 Final Thought
restoreAlarms is crucial for alarm persistence on iOS. Without it, alarms may disappear when the app restarts or the device reboots. It ensures that your alarm system remains reliable for users, no matter what happens! 🚀💡

1️⃣ Wrong Timezone Conversion (Fixed Now ✅)
Issue:

The system was defaulting to UTC (GMT+0000) instead of the device's local timezone (Asia/Colombo +0530).
The alarm time was being converted incorrectly when DateComponents were used.
Root Cause:

Calendar.current.date(from: dateComponents) was using the default timezone (UTC).
Solution: Explicitly set dateComponents.timeZone = TimeZone.autoupdatingCurrent before scheduling.