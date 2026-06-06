
flutter create inventory_app
flutter run

---
#### adb
flutter devices
flutter run -d emulator-5554
flutter run -d linux

--- 
#### When app is running
r -> hot reload
R -> restart

--- 
#### Install dependencies
flutter pub get
flutter pub add http
flutter pub add mobile_scanner

pubspec.yaml

flutter pub remove mobile_scanner

flutter pub upgrade

--- 
#### Clean Build Cache
flutter clean

#### Analyze/Lint
flutter analyze

--- 
#### Build APK
flutter build apk
flutter build apk --release

output -> build/app/outputs/flutter-apk/

--- 
#### Build App Bundle (Play Store)
flutter build appbundle

-> .aab

--- 
#### Doctor Command 
flutter doctor

