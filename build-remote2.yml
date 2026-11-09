name: Build Remote 2 APK
on:
  push:
    paths:
      - 'ac-remote-2-*.zip'
      - '.github/workflows/build-remote2.yml'
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Unpack project (latest Remote 2 zip)
        run: unzip -q "$(ls ac-remote-2-v*.zip | sort -V | tail -n 1)" -d proj
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.7'
      - name: Build debug APK
        working-directory: proj
        run: gradle assembleDebug --no-daemon
      - uses: actions/upload-artifact@v4
        with:
          name: AC-Remote-2-APK
          path: proj/app/build/outputs/apk/debug/app-debug.apk
