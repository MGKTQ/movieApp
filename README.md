# Himba Movie App

Himba is a native Android movie browser built with Kotlin and Jetpack Compose. It uses [The Movie Database (TMDB)](https://www.themoviedb.org/) API to show movie lists, search results, details, account favorites, and profile data.

## Features

- Browse movie collections such as popular, top rated, now playing, and best selling movies.
- View detailed movie information including poster/backdrop artwork, genres, release data, overview, ratings, and status.
- Search movies and persist search history locally.
- Sign in with TMDB credentials to access account-only features.
- Add or remove movies from TMDB favorites.
- View favorite movies and profile information after login.
- Bottom-tab navigation for Home, Search, Favorite, and Profile sections.
- Edge-to-edge Material 3 Compose UI with Coil-powered image loading.

## Tech Stack

- **Language:** Kotlin
- **UI:** Jetpack Compose, Material 3
- **Architecture:** MVVM-style presentation with repository interfaces and implementations
- **Navigation:** Navigation Compose with Kotlin serialization routes
- **Dependency Injection:** Hilt
- **Networking:** Retrofit with Moshi
- **Images:** Coil 3
- **Local Storage:** Room for search history and DataStore Preferences for auth/session values
- **Build:** Gradle Kotlin DSL, Android Gradle Plugin

## Project Structure

```text
.
├── app/
│   ├── build.gradle.kts                  # Android app configuration and dependencies
│   └── src/main/
│       ├── AndroidManifest.xml           # App entry point and permissions
│       ├── java/com/mgoudarzi/movieapp/
│       │   ├── data/                     # Remote APIs, DTOs, Room, DataStore, repository implementations
│       │   ├── di/                       # Hilt dependency graph
│       │   ├── domain/                   # Models, repository contracts, utilities
│       │   ├── ui/                       # Compose screens, components, theme, navigation helpers
│       │   ├── App.kt                    # Hilt application class
│       │   └── MainActivity.kt           # Compose navigation host
│       └── res/                          # Android resources
├── gradle/libs.versions.toml             # Version catalog
├── build.gradle.kts                      # Root Gradle plugin declarations
└── settings.gradle.kts                   # Gradle project settings
```

## Requirements

- Android Studio with Android Gradle Plugin support
- JDK 11 or newer
- Android SDK with compile SDK 35 installed
- A TMDB API access token

## TMDB Setup

This app sends TMDB requests with a Bearer token. To run it against the TMDB API:

1. Create or sign in to a TMDB account.
2. Request an API key/access token from TMDB.
3. Open `app/src/main/java/com/mgoudarzi/movieapp/data/util/Constants.kt`.
4. Replace the placeholder value:

```kotlin
const val API_KEY: String = "ENTER YOUR API KEY"
```

with your TMDB API read access token.

> Note: The current project stores the API token directly in source for local development. For production apps, move secrets out of source control and inject them through a secure build/runtime configuration.

## Getting Started

Clone the repository and open it in Android Studio, or build from the command line:

```bash
git clone <repository-url>
cd movieApp
./gradlew assembleDebug
```

Install the debug build on a connected device or emulator:

```bash
./gradlew installDebug
```

You can also run the app directly from Android Studio by selecting the `app` configuration.

## Useful Gradle Commands

```bash
# Build a debug APK
./gradlew assembleDebug

# Install the debug APK on a connected device/emulator
./gradlew installDebug

# Run unit tests if/when test sources are added
./gradlew test

# Run Android lint
./gradlew lint

# Clean build outputs
./gradlew clean
```

## Authentication Flow

- The login screen requests a TMDB token.
- User credentials validate the request token.
- A TMDB session ID is created and saved with DataStore Preferences.
- Favorite and profile screens require a saved session ID; otherwise, the app shows the login screen.

## Local Data

- Room stores search history in the `history` table.
- DataStore Preferences stores the TMDB request token, token timestamp, and session ID.

## Notes and Limitations

- `ProfileApi` currently targets account ID `21800203` directly in endpoint paths. If you use this project with another account, update those endpoints or refactor them to use the authenticated account details dynamically.
- The repository does not currently include test source sets.
- The app requires internet access for TMDB content and authentication.

## License

No license file is currently included. Add a license before distributing or reusing this project publicly.
