# uga-marketplace

A React Native / Expo mobile frontend for a UGA student marketplace. Students can list, browse, wishlist, and purchase items from other UGA students. Payments are handled peer-to-peer via Zelle.

## Prerequisites

- Node.js (LTS)
- Java `21.0.2-tem` (required for Android builds)
- Expo CLI: `npm install -g expo-cli`
- Android Studio + emulator (for Android development)

## Quick Start

1. Install dependencies:

```bash
npm install
```

2. Create a `.env` file in the project root and populate it with the required variables (see [Environment Variables](#environment-variables) below).

3. Start the development server:

```bash
npx expo start
```

Then press `a` to launch on the Android emulator.

> The API client is hardcoded to `http://10.0.2.2:5274/api` (Android emulator loopback to host). If running on a physical device or a different setup, update the `baseURL` in `src/api/client.ts`.

## Environment Variables

All variables are prefixed with `EXPO_PUBLIC_` and must be set in a `.env` file in the project root.

| Variable | Description |
|---|---|
| `EXPO_PUBLIC_SUPABASE_URL` | Supabase project URL (used for image storage) |
| `EXPO_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous/public API key |
| `EXPO_PUBLIC_SUPABASE_BUCKET_NAME` | Supabase storage bucket name for product images |
| `EXPO_PUBLIC_GOOGLE_MAPS_API_KEY_IOS` | Google Maps API key for iOS |
| `EXPO_PUBLIC_GOOGLE_MAPS_API_KEY_ANDROID` | Google Maps API key for Android |
| `EXPO_PUBLIC_PLACES_API_KEY` | Google Places API key for address autocomplete |

## Key Dependencies

| Package | Version |
|---|---|
| `expo` | ~55.0.5 |
| `react-native` | 0.83.2 |
| `react` | 19.2.0 |
| `expo-router` | ~55.0.4 |
| `react-native-paper` | ^5.15.0 |
| `react-native-maps` | 1.27.2 |

## For clean standalone development build

Android:

```bash
npx expo prebuild --clean
npx expo run:android --variant release
```

iOS:

```bash
# placeholder
```

## Known compatibility issues and pitfalls

- Compile using `java 21.0.2-tem`

```bash
sdk install java 21.0.2-tem   # install Temurin 21
sdk use java 21.0.2-tem        # switch to it
```

- debug/production SHA1 should match the `OAuth 2.0 Client IDs` configs on Google Cloud Console

```bash
# Emulator SHA1: grab the debug variant SHA1
$ ./gradlew signingReport
```

- (This is for requests to go through properly if using an emulator) For cleartext HTTP on Android, add it directly in AndroidManifest.xml since the app.json key isn't supported. After prebuild, open `android/app/src/main/AndroidManifest.xml` and add:

```xml
<application
    android:usesCleartextTraffic="true"
    ...>
```

## Important flag

```
%%%%%%%%%%%%%%%% VALIDATE UGA EMAIL DOMAIN %%%%%%%%%%%%%%%%
```
