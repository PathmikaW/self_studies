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
