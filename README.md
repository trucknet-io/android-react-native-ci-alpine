# Alpine React Native Android build image

All images are based on openjdk:8-alpine (JDK 8.181.13-r0)

Latest node and npm is installed to be able to build [React Native](https://facebook.github.io/react-native/) project and deps.
Latest ruby and ruby-dev is installed to be able to install [fastlane](https://fastlane.tools/).
Fastlane is pre-installed. Even if you use another fastlane version it is handy, because all the dependency gems (including the native extentions) are preinstalled in this image.

---

### Pull from Docker Hub
| API level | Command | Info |
| --------- | ------- | ---- |
| Android 21 (5.0) | `docker pull trucknet/android-react-native-ci-alpine:android-21` | [Info](https://github.com/alvr/alpine-android/tree/master/android-21) |
| Android 22 (5.1) | `docker pull trucknet/android-react-native-ci-alpine:android-22` | [Info](https://github.com/alvr/alpine-android/tree/master/android-22) |
| Android 23 (6.0) | `docker pull trucknet/android-react-native-ci-alpine:android-23` | [Info](https://github.com/alvr/alpine-android/tree/master/android-23) |
| Android 24 (7.0) | `docker pull trucknet/android-react-native-ci-alpine:android-24` | [Info](https://github.com/alvr/alpine-android/tree/master/android-24) |
| Android 25 (7.1) | `docker pull trucknet/android-react-native-ci-alpine:android-25` | [Info](https://github.com/alvr/alpine-android/tree/master/android-25) |
| Android 26 (8.0) | `docker pull trucknet/android-react-native-ci-alpine:android-26` | [Info](https://github.com/alvr/alpine-android/tree/master/android-26) |
| Android 27 (8.1) | `docker pull trucknet/android-react-native-ci-alpine:android-27` | [Info](https://github.com/alvr/alpine-android/tree/master/android-27) |
| Android 28 (9.0) | `docker pull trucknet/android-react-native-ci-alpine:android-28` | [Info](https://github.com/alvr/alpine-android/tree/master/android-28) |


### Use as Base Image
| API level | Command |
| --------- | ------- |
| Android 21 (5.0) | `FROM trucknet/android-react-native-ci-alpine:android-21` |
| Android 22 (5.1) | `FROM trucknet/android-react-native-ci-alpine:android-22` |
| Android 23 (6.0) | `FROM trucknet/android-react-native-ci-alpine:android-23` |
| Android 24 (7.0) | `FROM trucknet/android-react-native-ci-alpine:android-24` |
| Android 25 (7.1) | `FROM trucknet/android-react-native-ci-alpine:android-25` |
| Android 26 (8.0) | `FROM trucknet/android-react-native-ci-alpine:android-26` |
| Android 27 (8.1) | `FROM trucknet/android-react-native-ci-alpine:android-27` |
| Android 28 (9.0) | `FROM trucknet/android-react-native-ci-alpine:android-28` |