# ZenLife Localize

Dedicated localization repository for ZenLife.

This repo stores ARB translation source files only, so localization can be managed independently from the main Flutter app repository.

## Structure

```text
lib/l10n/arb/
  app_en.arb
  app_vi.arb
  app_hi.arb
  app_fr.arb
  app_de.arb
  app_ja.arb
  app_ko.arb
  app_zh_Hans.arb
  app_en_XA.arb
docs/
  workflow.md
RULES.md
```

## How this integrates with the app

In the main app repo, i18n scripts are configured to resolve ARB source in this order:

1. `ZENLIFE_ARB_DIR` (if set)
2. `localize/ZenLife_Localize/lib/l10n/arb`
3. `lib/l10n/arb` (fallback)

That means app tooling can consume translations directly from this repo when both repos live in the same workspace.

## Daily workflow

1. Update keys in `lib/l10n/arb/app_en.arb`.
2. Keep key set aligned across all locale files.
3. Translate values per locale.
4. From app repo root, run:
   - `dart run tool/i18n/sync_keys.dart`
   - `dart run tool/i18n/sync_from_arb.dart`
   - `dart run tool/i18n/validate_locales.dart --strict-orphan`
5. Commit and push changes in this repo.

Read detailed guide: `docs/workflow.md`.
Read translation constraints: `RULES.md`.
