#### barrel pattern
lib/
 └─ features/
    └─ auth/
       ├─ screens/
       │  ├─ login_page.dart
       │  ├─ signup_page.dart
       │  └─ auth_screens.dart   👈 barrel
       ├─ routes/
       │  └─ auth_routes.dart
       └─ widgets/

#### On barrel file
export 'login_page.dart';
export 'signup_page.dart';

#### Barrel Usage
import 'package:prac1/features/auth/screens/auth_screens.dart';

LoginPage()
SignupPage()

--- 

lib/
├── app/
├── bootstrap/
├── core/
├── domain/
│   ├── auth/
│   │   ├── auth.service.dart
│   │   ├── authr.epositories.dart  -> interface only
│   ├── users/
│   ├── events/
├── presentation/
│   ├── auth/
│   │   ├── state/ <- ui bound 
│   │   │   ├── auth.notifier.dart
│   │   │   ├── auth.state.dart
│   │   │   ├── auth.providers.dart
│   │   ├── login_page.dart
│   │   ├── signup_page.dart
	  ├── auth.route.dart <- subnode base routing
│   ├── dashboard/
│   ├── profile/
│   ├── bookings/
│   ├── root.route.ts <- node base routing
├── infrastructure/
│   ├── http/
│   │   ├── dio_client.dart
│   │   └── interceptors.dart
│   ├── storage/
│   │   ├── secure_storage.dart
│   │   └── local_storage.dart
│   ├── analytics/
│   ├── logging/
├── shared/
├── theme/
├── localization/
├── main.dart

--- 

### platform & startup wiring
bootstrap/
├── bootstrap.dart
├── env.dart
├── platform_config.dart
void bootstrap() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Env.load();
  await PlatformConfig.init();

  runApp(const App());
}

app/ the real root of your app
├── app.dart
├── app_providers.dart

features/
├── auth/
│   ├── data/
│   ├── domain/
│   ├── presentation/
│   ├── auth.dart
├── dashboard/
├── profile/
├── bookings/

auth/
├── data/
│   ├── auth_api.dart
│   ├── auth_repository_impl.dart
│   └── auth_dto.dart
├── domain/
│   ├── auth_repository.dart
│   ├── login_usecase.dart
│   └── user_entity.dart
├── presentation/
│   ├── pages/
│   │   ├── login_page.dart
│   │   └── signup_page.dart
│   ├── widgets/
│   │   └── login_form.dart
│   └── state/
│       └── auth_controller.dart
├── auth.dart   👈 barrel export


infrastructure/ cross-feature services
├── http/
│   ├── dio_client.dart
│   └── interceptors.dart
├── storage/
│   └── secure_storage.dart
├── analytics/
├── logging/

shared/ reusable UI & utils
├── widgets/
│   ├── buttons/
│   ├── inputs/
│   ├── modals/
├── utils/
├── extensions/

core/ app-wide contracts
├── errors/
├── result.dart
├── usecase.dart

theme/ serious theming
├── app_theme.dart
├── colors.dart
├── typography.dart
├── spacing.dart
