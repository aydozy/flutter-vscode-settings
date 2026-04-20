# Flutter & Dart — VS Code Setup

A clean, productivity-focused VS Code configuration for Flutter and Dart development.
Drop these files into your project and get formatting, auto-imports, const fixes, and more — all on save.

> 📖 For a full walkthrough of each setting, check out the companion article:
> [A Clean & Productive VS Code Setup for Flutter & Dart Developers](https://medium.com/@ozyurek.aydanil/a-clean-productive-vs-code-setup-for-flutter-dart-developers-6fba37f050bc)

---

## What's included

| File | Purpose |
|---|---|
| `.vscode/settings.json` | Editor formatting, save actions, Dart/Flutter quality-of-life settings |
| `analysis_options.yaml` | Lint rules that power auto-const fixes on save |

---

## Quick start

1. Copy `.vscode/settings.json` into your project's `.vscode/` folder.
2. Copy `analysis_options.yaml` into your project root.
3. Make sure `flutter_lints` is in your `pubspec.yaml`:

```yaml
dev_dependencies:
  flutter_lints: ^4.0.0
```

4. Run `flutter pub get`, then open any Dart file and hit **Cmd+S** (or Ctrl+S).

---

## What happens on save

- Code is formatted using `dart format`
- Imports are sorted and unused ones are removed
- Missing imports are added automatically
- `const` keywords are added wherever possible
- Trailing whitespace is trimmed

---

## settings.json — highlights

### Formatting
```jsonc
"editor.formatOnSave": true,
"editor.formatOnType": true,
"editor.formatOnPaste": true
```
Keeps code clean without any manual effort.

### Save actions
```jsonc
"editor.codeActionsOnSave": {
  "source.organizeImports": "always",
  "source.addMissingImports": "always",
  "source.fixAll": "always"
}
```
`source.fixAll: "always"` is the key setting — it applies all auto-fixable lint warnings on save, including adding `const`. This only works if the corresponding lint rules are active in `analysis_options.yaml`.

### File cleanliness
```jsonc
"files.trimTrailingWhitespace": true,
"files.insertFinalNewline": true,
"files.trimFinalNewlines": true
```
No more trailing spaces or inconsistent file endings in your diffs.

### Hot reload on save
```jsonc
"dart.hotReloadOnSave": "all"
```
Triggers Flutter hot reload automatically whenever you save a file.

### Editor readability
```jsonc
"editor.bracketPairColorization.enabled": true,
"editor.guides.bracketPairs": true,
"editor.stickyScroll.enabled": true
```
Makes deeply nested widget trees much easier to navigate.

---

## analysis_options.yaml — const rules

These four rules are what make auto-const work on save:

| Rule | What it does |
|---|---|
| `prefer_const_constructors` | Adds `const` to constructors that can be constant |
| `prefer_const_literals_to_create_immutables` | Makes `[]` → `const []` inside immutable widgets |
| `prefer_const_declarations` | Changes `final x = 5` → `const x = 5` where possible |
| `prefer_const_constructors_in_immutables` | Enforces `const` constructors on `StatelessWidget` subclasses |

Without these rules active, `source.fixAll` has nothing to fix — so both files are needed together.

---

## Requirements

- [Dart-Code extension](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code)
- [Flutter extension](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter)
- Flutter SDK
- `flutter_lints` in `dev_dependencies`
