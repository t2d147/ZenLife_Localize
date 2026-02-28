# Localization Workflow

This workflow is for contributors who edit ARB files in `ZenLife_Localize`.

## 1. Add or update source key

- Edit `lib/l10n/arb/app_en.arb` first.
- Add the value and, when needed, metadata block `@<key>`.

Example:

```json
{
  "home.welcome": "Welcome back, {name}",
  "@home.welcome": {
    "description": "Greeting on home screen",
    "placeholders": {
      "name": {
        "type": "String"
      }
    }
  }
}
```

## 2. Sync keys to all locale files

From app repository root:

```bash
dart run tool/i18n/sync_keys.dart
```

This fills missing keys in other locale files using English values as placeholders.

## 3. Translate locale values

- Translate only user-facing strings.
- Keep placeholders unchanged (`{name}`, `{count}`, etc.).
- Do not remove metadata blocks for keys with placeholders/plurals.

## 4. Build runtime JSON from ARB

From app repository root:

```bash
dart run tool/i18n/sync_from_arb.dart
```

## 5. Validate

From app repository root:

```bash
dart run tool/i18n/validate_locales.dart --strict-orphan
```

## 6. Commit

In this repo:

```bash
git add .
git commit -m "i18n: update <scope>"
git push
```

## PR checklist

- `app_en.arb` contains new/changed keys.
- All locale files include the same key set.
- Placeholders are preserved across locales.
- JSON syntax is valid.
- Validation command passes in app repo.
