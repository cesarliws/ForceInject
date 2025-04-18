# 🔌 ForceInject
[![pub package](https://img.shields.io/pub/v/force_inject.svg)](https://pub.dev/packages/force_inject)
[![publisher: diegogarcia.ca](https://img.shields.io/badge/publisher-diegogarcia.ca-blue)](https://pub.dev/publishers/diegogarcia.ca)


🛠️ A lightweight, zero-runtime-dependency Dependency Injection (DI) container for Dart.  
🌌 Inspired by .NET Core and powered by the Force.  
**This is the Way.**

## ✨ Features

- Constructor-based dependency injection
- Support for `singleton`, `transient`, and `scoped lifetimes
- Zero dependencies — pure Dart
- No code generation, no mirrors
- Inspired by C#/.NET Core DI patterns
- Lightweight, test-friendly, and easy to integrate

## ⚙️ Dependencies

ForceInject is designed to have **no runtime dependencies**.

We use the Dart team's official [`meta`](https://pub.dev/packages/meta) package only for static annotations like `@protected` and `@visibleForTesting`.

This ensures:
- ✅ No runtime or platform bloat
- ✅ Full IDE and analyzer support
- ✅ Maximum compatibility with Flutter, backend, and CLI

## 🚀 Getting Started

### 1. Register your services

```dart
final services = ServiceCollection();

services.addSingleton<ILogger, ConsoleLogger>();
services.addTransient<UserService, UserService>();

ServiceProvider.registerConstructor<ConsoleLogger>(() => ConsoleLogger(), []);
ServiceProvider.registerConstructor<UserService>(
  (ILogger logger) => UserService(logger),
  [ILogger],
);
```

### 2. Build the provider

```dart
final provider = services.buildServiceProvider();
```

### 3. Resolve services

```dart
final userService = provider.get<UserService>();
userService.sayHello(); // [LOG]: Hello from UserService!
```

### Need a per-screen or per-request services? Create a `ServiceScope`:

```dart
final scope = provider.createScope();
final viewModel = scope.get<MyViewModel>();
scope.dispose(); // clean up when done
```

## ⚙️ Lifetimes

| Type        | Description                                |
|-------------|--------------------------------------------|
| `singleton` | One shared instance across the application |
| `transient` | A new instance is created every time       |
| `scoped`    | One instance per ServiceScope — ideal for screen/request lifetimes |


## 📦 Why ForceInject?

Dart is an elegant language, but backend structure is still evolving.  
**ForceInject** gives you the power of .NET’s DI model, but in pure Dart — making your code modular, testable, and maintainable.

No magic. No mirrors. Just clean, focused architecture.  
💬 *"When your services are confused, inject them you must."* – Yodart


## 🧪 Examples

This package includes two complete examples you can explore:

- 🧱 [`minimal_dart_di`](https://github.com/diegomgarcia/force_inject/tree/main/example/minimal_dart_di)  
  A simple Dart CLI app using ForceInject with singleton and transient services.

- 📱 [`minimal_flutter_di`](https://github.com/diegomgarcia/force_inject/tree/main/example/minimal_flutter_di)  
  A clean Flutter app using scoped DI and a `ValueNotifier`-based ViewModel.

To run the Flutter example:
```bash
cd example/minimal_flutter_di
flutter create .
flutter pub get
flutter run
```
**Read the README.md inside the minimal_flutter_di project for more details.**

## Support me ([@diegomgarcia](https://github.com/diegomgarcia)) with Patreon

[![Patreon](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/dmgarcia)

Or make a donation buying me a coffee:

[![Buy Me A Coffee](https://user-images.githubusercontent.com/835641/60540201-fcd7fa00-9ce4-11e9-87ec-1e98568e9f58.png)](https://www.buymeacoffee.com/dmgarcia)

You can also show support by showing on your repository that you use this lib on it with a direct link to it.

## 📜 License

MIT – Free to use, modify, or extend.  
**May the DI be with you. ⚔️**
