# HotelRooms (Kempinski Room Booking)

An Android app for managing hotel room client bookings, built with **Kotlin** and **Jetpack Compose**, backed by **Firebase** (Authentication, Realtime Database, and Storage). Staff can register/log in and add, view, update, and browse guest booking records.

## Features

- **Authentication** — sign-up and login via Firebase Auth
- **Client/booking management** — add a client booking (name, ID number, phone/"tell", date, room), view a list of all clients, view a single client's details, and update an existing booking
- **Entry/home screens** — a landing entry screen and a home screen for navigating between features
- Hotel imagery bundled as drawable resources (used for branding/visual context in the UI, e.g. `kempinski.jpg`, `hilton.jpg`, `sarova.jpg`, `panari.jpg`, and others)

## Tech stack

| Layer | Technology |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose (Material 3) |
| Navigation | Jetpack Navigation Compose |
| Backend | Firebase Authentication, Realtime Database, Storage |
| Build system | Gradle (Kotlin DSL), AGP |

**Key SDK versions:** see `gradle/libs.versions.toml` for exact versions; Java/Kotlin target 1.8 (per `app/build.gradle.kts`).

## Project structure

```
KempinskiRoomBooking-master/
├── app/
│   ├── google-services.json          # Firebase config (see below)
│   └── src/main/java/com/example/hotelrooms/
│       ├── MainActivity.kt
│       ├── data/                     # ViewModels
│       │   ├── AuthViewModel.kt      # signup/login logic
│       │   └── ClientViewModel.kt    # add/update/view client logic
│       ├── models/                   # Data models: Client, User
│       ├── navigation/               # AppNavHost + route constants
│       └── ui/theme/screens/
│           ├── home/                 # Entry screen, home screen
│           ├── login/                # Login screen
│           ├── register/             # Registration screen
│           └── clients/
│               ├── AddClientScreen.kt
│               ├── viewClients.kt
│               ├── viewClient.kt      # single client detail view
│               ├── singleClient.kt
│               └── updateClients.kt
├── build.gradle.kts
├── settings.gradle.kts
└── gradle/libs.versions.toml           # Version catalog
```

## Prerequisites

- Android Studio (Koala or newer recommended)
- JDK 17 (bundled with recent Android Studio releases)
- An Android device or emulator running API level matching `minSdk` (see `app/build.gradle.kts`)
- A Firebase project with Authentication, Realtime Database, and Storage enabled

## Setup

1. **Clone the repo**

   ```bash
   git clone <this-repo-url>
   cd KempinskiRoomBooking-master
   ```

2. **Open in Android Studio**

   File → Open → select the `KempinskiRoomBooking-master` folder, and let Gradle sync.

3. **Firebase configuration**

   The project ships with an `app/google-services.json` pointing at the original developer's Firebase project. To run against your own backend:

   - Create a project in the [Firebase console](https://console.firebase.google.com/)
   - Enable **Authentication** (Email/Password), **Realtime Database**, and **Storage**
   - Register an Android app with package name `com.example.hotelrooms`
   - Download your own `google-services.json` and replace `app/google-services.json`

   > ⚠️ If you plan to publish this project or push it to a public repo, don't commit your own `google-services.json` / real Firebase credentials — add it to `.gitignore` instead.

4. **Build and run**

   ```bash
   ./gradlew assembleDebug
   ```

   Or click **Run** in Android Studio to install on a connected device/emulator.

## App flow

- The app launches into an **Entry screen**, leading to **Login** or **Register**.
- Once authenticated, users land on the **Home screen**, from which they can add a new client booking, view the full client list, view a single client's details, or update an existing booking. See `navigation/Routes.kt` for the full route list and `navigation/AppNavHost.kt` for how screens are wired together.

## Notes

- Despite the repo name referencing Kempinski specifically, the app itself (`app_name` = "HotelRooms", package `com.example.hotelrooms`) is a general hotel room booking/client-management tool — the bundled images include several different hotel brands (Kempinski, Hilton, Sarova, Panari, Parkinn), suggesting these are sample/placeholder images rather than a single-property branding.
- No automated CI or unit test suite is set up beyond the default Android Studio-generated instrumented/unit test stubs (`ExampleInstrumentedTest.kt`, `ExampleUnitTest.kt`).

## License

Not specified.
