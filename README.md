# Xcode 27.2 crash compiling ExpoModulesCore from source

A blank `create-expo-app` (SDK 58) with one change: `expo-build-properties` sets
`ios.usePrecompiledModules: false`, so `ExpoModulesCore` is compiled from source.

With Xcode 27.2 (Swift 6.4.2) the Swift compiler crashes on
`expo-modules-core/ios/Core/Functions/AsyncFunctionDefinition.swift`, in the
`switch consume result` with `case .failure(let error as any Error)`.

```sh
npm install
npx expo run:ios
```

Expected: the app builds. Actual: `SwiftCompile` fails in target
`ExpoModulesCore` with a compiler crash. Changing that line to
`case .failure(let error):` makes it build.
