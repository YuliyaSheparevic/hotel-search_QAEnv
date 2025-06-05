To ensure the environment supports manual testing, the setup process is extended to include all necessary elements for running the tests:
1. **List of tools, dependencies, and versions**:

Tool Versions:

- Flutter SDK: 3.32.2
- Generate API key in SerpAPI (https://serpapi.com/) 
- Dart: 3.8.1
- Android Studio: 2024.3.2.15
- Android Emulator: API Level 34 (Android 14)
- Xcode: 16.4  (iOS 18.5)
- Patrol: 3.15.2  
- Maestro: 1.40.3

Tool Installation:
- Install Flutter from flutter.dev (https://flutter.dev/) .
- Install Android Studio and set up AVD Manager for emulators (https://developer.android.com/studio/install?hl=ru) .
- Install Xcode and configure the iOS Simulator (macOS only) (https://apps.apple.com/us/app/xcode/id497799835?mt=12) .
- Install Patrol (https://pub.dev/packages/patrol/versions).
- Install Maestro (https://github.com/mobile-dev-inc/maestro/releases)

2. **Install Necessary Tools - details:**
   
To test and work with the hotel_booking Flutter application, install the following dependencies and tools:

Core Tools:
 - Flutter SDK:
Install Flutter SDK for your operating system.
Verify the installation in cmd:
flutter --version

 - Android Studio (for Android Emulators):
Download Android Studio.
Ensure SDK Tools and AVD Manager are installed (via Android Studio > Preferences/Settings > Appearance & Behavior > System Settings > Android SDK).

- Xcode (only for macOS, for iOS Simulators):
Download Xcode from the App Store.
Go to Preferences > Locations in Xcode and select Command Line Tools.

- Git:
Ensure that git is installed in cmd:
git --version

Optional Tools for Automated Testing:
Patrol (to perform end-to-end testing for Flutter applications).
Maestro (for cross-platform E2E testing scenarios).

3. **Configure Android Emulator**
 - Open Android Studio and go to AVD Manager (Tools > Device Manager).
 - Create a new Android Emulator:
Device: Samsung Galaxy S25 / Pixel 5 or another device.
Android version:  API Level 34 (Android 14) or higher.
Save the setup and launch the emulator.
Verify Emulator Availability via Flutter: Run the command:
     flutter devices
.The emulator should appear in the list of connected devices.

4. **Configure iOS Simulator (For macOS Users)**
 - Launch iOS Simulator:
Open Xcode > Preferences > Components and install your desired simulator version (e.g., iOS 16.4 for iPhone 14).
- Start the simulator:
      open -a Simulator
 - Verify Simulator Availability via Flutter: Run the command:
      flutter devices
.The simulator should appear in the list of connected devices.

5. **Clone and Build the Application**
 - Clone the repository and navigate to the project:
      git clone https://github.com/akshdeep-singh/hotel_booking
      cd hotel_booking
 - Install Flutter Dependencies: Run the following command: 
      flutter pub get
 - Create .env File for API Key Setup: The app requires the SerpAPI key:
      touch .env
      echo "SERPAPI_API_KEY=<YOUR_API_KEY>" > .env
  Replace <YOUR_API_KEY> with your actual SerpAPI key obtained from serpapi.com.
 - Run Code Generation Script Using build_runner: The app uses the build_runner package for generating necessary files:
      flutter pub run build_runner build --delete-conflicting-outputs
 - Test the build by running the app:
      flutter run

6. **Running Tests**
 - for unit tests: 
       flutter test
 - for integration tests:
       flutter drive --target=integration_test/hotel_search_tests.dart

