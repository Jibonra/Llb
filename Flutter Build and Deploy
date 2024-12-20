name: Flutter Build and Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Checkout the repository
      - name: Checkout repository
        uses: actions/checkout@v3

      # Install Flutter
      - name: Install Flutter
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.13.0' # Replace with your required Flutter version

      # Get dependencies
      - name: Get dependencies
        run: flutter pub get

      # Run tests (optional)
      - name: Run tests
        run: flutter test

      # Build APK
      - name: Build APK
        run: flutter build apk --release

      # Upload APK as an artifact
      - name: Upload APK
        uses: actions/upload-artifact@v3
        with:
          name: app-release
          path: build/app/outputs/flutter-apk/app-release.apk

  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
      # Checkout the repository
      - name: Checkout repository
        uses: actions/checkout@v3

      # Upload APK to Firebase Hosting (optional if using Firebase Hosting)
      - name: Deploy to Firebase Hosting
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        run: |
          npm install -g firebase-tools
          firebase deploy --only hosting
          
