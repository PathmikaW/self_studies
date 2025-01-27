Steps to Check Available Emulators and Run App
1. Check Available Emulators
Open the Command Palette in VS Code (Ctrl + Shift + P or Cmd + Shift + P on macOS).
Type "React Native: Run Android on Emulator" or "React Native: Run iOS on Simulator".
Alternatively, you can manually list the devices:

For Android:
bash
Copy code
adb devices
This command lists connected devices and emulators.
For iOS (macOS only):
bash
Copy code
xcrun simctl list devices
This command lists available iOS simulators.
2. Launch Emulator/Simulator
For Android:
Start an emulator from Android Studio or via CLI:
bash
Copy code
emulator -avd <emulator_name>
Replace <emulator_name> with the name of your emulator.
For iOS (macOS only):
Launch a simulator:
bash
Copy code
open -a Simulator
3. Run React Native App
Start the Metro Bundler:
bash
Copy code
npx react-native start
Run on Android:
bash
Copy code
npx react-native run-android
Run on iOS (macOS only):
bash
Copy code
npx react-native run-ios
Use VS Code for One-Click Run
Install the React Native Tools extension in VS Code.
Open the Command Palette and choose:
React Native: Run Android to run on Android.
React Native: Run iOS to run on iOS (macOS only).
Troubleshooting
Ensure your emulator is powered on and responsive.
If you encounter errors, check logs using:
bash
Copy code
adb logcat
or the VS Code Debug Console.


npx react-native run-android --deviceId <device_id>
