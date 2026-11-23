# 🌾 KrishiMitra

### One stop application for Indian farmers.

![Platform](https://img.shields.io/badge/platform-Android-green.svg)
![Language](https://img.shields.io/badge/language-Kotlin-blue.svg)
![Min API](https://img.shields.io/badge/min%20SDK-21-orange.svg)
![License](https://img.shields.io/badge/license-MIT-yellow.svg)

KrishiMitra is an Android application built to bring the tools an Indian farmer needs into a single place. Instead of juggling separate apps for mandi prices, weather, government schemes, shopping, and community updates, KrishiMitra combines them into one focused, easy-to-use experience.

The project is written in Kotlin with an MVVM-style structure, Jetpack components, Retrofit for network calls, Firebase for cloud data and authentication, and Razorpay for in-app payments.

---

## 📑 Table of contents

- [Why KrishiMitra](#-why-krishimitra)
- [Features](#-features)
- [Architecture](#-architecture)
- [Technology stack](#-technology-stack)
- [Project structure](#-project-structure)
- [Getting started](#-getting-started)
- [Configuration](#-configuration)
- [Testing](#-testing)
- [Design](#-design)
- [Possible next steps](#-possible-next-steps)
- [Contributing](#-contributing)
- [License](#-license)
- [Support](#-support)

---

## 🎯 Why KrishiMitra

Technology is now part of everyday life and makes routine work easier. Agriculture, however, is still served by fragmented tools that each solve only one small problem. A farmer who wants to check today's APMC rate, read about a scheme, follow the weather, order inputs, and talk to other farmers has to move between many apps and accounts.

KrishiMitra was created to remove that friction:

- One app instead of many.
- One familiar interface for every feature.
- Information and services organised around real farming workflows.
- A community space for farmers to share and learn.

---

## ✨ Features

### 1. Government Yojna Awareness
Browse government schemes and announced programmes from the app so that useful information is not missed. Scheme content is surfaced through dedicated list and detail screens.

### 2. E-commerce Platform
A complete marketplace flow for agricultural inputs and related products:

- Product listing and category browsing
- Product detail screens with attributes
- Shopping cart with quantity controls
- Order history
- Checkout through Razorpay

### 3. Daily APMC Price Updates
Agricultural Produce Market Committee (APMC) price data is fetched from the public `data.gov.in` API. The app supports district-based filtering so farmers can focus on the markets relevant to them.

### 4. Community Network (Social Media)
A social feed where farmers can create posts, attach images, and browse updates from the community. Profile-related screens show a user's own posts.

### 5. Category-based Articles
Reading material is organised into categories such as fruits and machinery. Article lists and individual articles are loaded into simple, readable screens.

### 6. Weather Forecasting
Location-based forecasts are retrieved from the OpenWeatherMap API. Current conditions and upcoming forecasts are displayed through dedicated weather screens and adapters.

### 7. Onboarding and Authentication
A short intro flow explains the app before sign-in. Login and signup screens are backed by Firebase Authentication, and the dashboard is the main entry point after authentication.

---

## 🧱 Architecture

KrishiMitra follows a layered, MVVM-style approach:

```text
Activity / Fragment  (UI)
        |
        v
ViewModel + Listener (UI state, events)
        |
        v
Repository           (data coordination)
        |
        v
Retrofit API / Firebase services
        |
        v
Data models / DTOs
```

Key architectural choices:

| Layer | Implementation |
| --- | --- |
| UI | Activities, Fragments, DataBinding, Material Components, RecyclerView adapters |
| State | `ViewModel`, LiveData, listener interfaces |
| Data coordination | Repository classes for APMC, weather, articles, authentication |
| Networking | Retrofit 2 with Gson converter |
| Dependency injection | Kodein |
| Cloud | Firebase Authentication, Firestore, Storage, Realtime Database |
| Navigation | Jetpack Navigation with Safe Args |
| Payments | Razorpay Checkout |
| Images | Picasso and Glide |
| Async work | Kotlin coroutines |

---

## 🛠️ Technology stack

| Area | Tools / libraries |
| --- | --- |
| Language | Kotlin 1.3.72 |
| Build | Gradle 4.0.1 Android plugin, Gradle wrapper |
| Android SDK | compileSdk 29, minSdk 21, targetSdk 29, build tools 29.0.2 |
| UI | AndroidX, ConstraintLayout, Material Components, DataBinding |
| Architecture | ViewModel, LiveData, Navigation, Safe Args, Kodein |
| Networking | Retrofit, Gson, OkHttp (via Retrofit) |
| Firebase | Auth, Firestore, Storage, Realtime Database, Cloud Messaging config via `google-services.json` |
| Location | Google Play Services Location |
| Payments | Razorpay Checkout |
| Image loading | Picasso, Glide |
| Layout helpers | StackLayoutManager, CarouselLayoutManager, PosterSlider |
| Testing | JUnit 4, AndroidX Test, Espresso |

---

## 📂 Project structure

```text
KrishiMitra/
├── app/
│   ├── google-services.json
│   ├── build.gradle
│   └── src/
│       ├── androidTest/                 # Instrumented tests
│       ├── test/                        # Unit tests
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/com/project/farmingapp/
│           │   ├── model/
│           │   │   ├── data/            # API and domain models
│           │   │   ├── APMCApi.kt
│           │   │   ├── APMCRepository.kt
│           │   │   ├── WeatherApi.kt
│           │   │   └── WeatherRepository.kt
│           │   ├── utilities/           # Small helpers and click listeners
│           │   ├── viewmodel/           # ViewModels and listener interfaces
│           │   ├── adapter/             # RecyclerView and slider adapters
│           │   ├── view/
│           │   │   ├── auth/            # Login and signup
│           │   │   ├── dashboard/       # Main dashboard
│           │   │   ├── apmc/            # Mandi prices
│           │   │   ├── weather/         # Forecast
│           │   │   ├── ecommerce/       # Products, cart, orders, payment
│           │   │   ├── articles/        # Category-based reading
│           │   │   ├── socialmedia/     # Community feed and post creation
│           │   │   ├── yojna/           # Government schemes
│           │   │   ├── user/            # Profile
│           │   │   └── introscreen/     # Onboarding
│           │   └── PrePaymentFragment.kt
│           └── res/
│               ├── layout/              # Screen and item layouts
│               ├── drawable/            # Icons, backgrounds, artwork
│               ├── drawable-v24/
│               ├── mipmap-*/            # Launcher icons
│               ├── values/              # Strings, colors, styles, fonts
│               ├── font/
│               ├── anim/
│               ├── color/
│               └── menu/
├── gradle/wrapper/
├── build.gradle
├── settings.gradle
├── KrishiMitra.png
└── README.md
```

---

## 🚀 Getting started

### Prerequisites

- Android Studio with Android Gradle Plugin 4.0.x support
- JDK 8
- Android SDK Platform 29 and build tools 29.0.2
- An Android device or emulator running API 21 or above
- Internet access for Gradle dependency resolution and live API data

### Steps

```bash
git clone https://github.com/theRkakkad/KrishiMitra.git
cd KrishiMitra
```

1. Open the project folder in Android Studio.
2. Allow Gradle to sync and download dependencies.
3. Connect a device or start an emulator.
4. Run the `app` configuration.
5. The app opens on the dashboard; onboarding and authentication screens are available from the navigation flow.

Command-line build alternative:

```bash
./gradlew assembleDebug
```

---

## ⚙️ Configuration

The repository already contains the configuration needed for a local debug build:

| Setting | Location |
| --- | --- |
| Firebase project | `app/google-services.json` |
| Razorpay key | `app/src/main/res/values/strings.xml` (`key_id`) |
| APMC data endpoint | `app/src/main/java/com/project/farmingapp/model/APMCApi.kt` |
| Weather endpoint | `app/src/main/java/com/project/farmingapp/model/WeatherApi.kt` |
| App label | `app/src/main/res/values/strings.xml` (`app_name`) |
| Permissions | `app/src/main/AndroidManifest.xml` |

Declared permissions:

- `android.permission.INTERNET` — required for API and Firebase calls
- `android.permission.ACCESS_FINE_LOCATION` — used for location-aware weather
- `android.hardware.location.gps` — declared as a required hardware feature

> The prototype embeds third-party API keys directly in source for simplicity. Before any production release, move them to `local.properties` or BuildConfig fields, restrict them by package/signature, and rotate any exposed keys.

---

## 🧪 Testing

The project includes the standard Android test placeholders:

- `app/src/test/java/com/project/farmingapp/ExampleUnitTest.kt`
- `app/src/androidTest/java/com/project/farmingapp/ExampleInstrumentedTest.kt`

Run them with:

```bash
./gradlew test
./gradlew connectedAndroidTest
```

---

## 🖼️ Design

The application icon and branding artwork are stored in the repository root and under the launcher resource folders.

<img src="KrishiMitra.png" alt="KrishiMitra app design" width="320" />

---

## 🔮 Possible next steps

These are ideas for future work, not current features:

- Move all API keys out of source control.
- Add caching and offline support for APMC and article data.
- Replace legacy synthetic view access with View Binding.
- Expand unit and UI test coverage beyond the starter tests.
- Add accessibility labels and larger text support.
- Prepare a signed release build and Play Store listing.
- Consider a gradual Jetpack Compose migration for UI screens.

---

## 🤝 Contributing

1. Fork the repository.
2. Create a topic branch from `master`.
3. Make focused changes with clear commit messages.
4. Run the unit tests.
5. Open a pull request describing what changed and why.

Please keep user-facing naming consistent as **KrishiMitra** and avoid committing credentials.

---

## 📄 License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.

---

## ⭐ Support

If KrishiMitra helped you or inspired you, give the repository a ⭐ and fork it to build on top of the idea.
