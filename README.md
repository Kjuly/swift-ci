# swift-ci
Some reusable CI Workflows for app development in Swift (also including Objective-C).

## Usage for "unit-tests.yml"

```unit-tests-sample.yml
name: Unit Tests

on:
  push:

  pull_request:

jobs:
  call-reusable-workflow-to-test:
    uses: Kjuly/swift-ci/.github/workflows/unit-tests.yml@main
    with:
      use_xcodebuild: true
      platforms: 'iOS,watchOS,macOS'
    secrets: # Required only if need to access a private repo.
      token: ${{ secrets.YOUR_GITHUB_ACTION_TOKEN }} # Replace the `YOUR_GITHUB_ACTION_TOKEN` with your own.

```

| Options (with)   | Type    | Required | Default | Description
| ---------------- | ------- | -------- |--- | ---
| os               | string  | false    | "" (auto) | Preferred runner OS, e.g. "macos-latest", "ubuntu-latest".
| use_xcodebuild   | boolean | false    | false | Use 'xcodebuild test'; if not, will use 'swift test'.
| scheme           | string  | false    | (repo name) | The Xcode scheme for testing.
| platforms        | string  | false    | "iOS" | Paltform destinations to do testing, e.g. "iOS,watchOS,macOS".
| xcode_version    | string  | false    | "16.1" | Specify the Xcode version to use.
| iphone_simulator | string  | false    | "iPhone 16 Pro" | The name of the iPhone simulator to do testing for iOS.
| watch_simulator  | string  | false    | "Apple Watch Series 10 (46mm)" | The name of the Apple Watch simulator to do testing for watchOS.

| Secrets (secrets) | Type    | Required | Description
| ----------------- | ------- | -------- | ---
| token             | string  | false    | Github action token secrect, it's required if you need to access a private repo under the same user/org scope.

## Usage for "swift-lint.yml"

```swift-lint-sample.yml
name: Swift Lint

on:
  push:

  pull_request:
    paths:
      - '.swiftlint.yml'
      - '**/*.swift'

jobs:
  call-reusable-workflow-to-swift-lint:
    uses: Kjuly/swift-ci/.github/workflows/swift-lint.yml@main
    with:
      use_default_config: true
      force_exclude: true
```

| Options            | Type    | Required | Default | Description
| ------------------ | ------- | -------- |-------- | ---
| use_default_config | boolean | false    | false   | Whether use the default swiftlint.yml config file.
| force_exclude      | boolean | false    | false   | Whether exclude files in config `excluded` even if their paths are explicitly specified.

