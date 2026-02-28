# Localization Rules

## Scope

These rules apply to all ARB files in `lib/l10n/arb/`.

## Key naming

- Use dot-separated namespaces: `feature.section.item`.
- Use lowercase and snake_case segments only.
- Keep key names stable after release.
- Do not reuse an old key for a new meaning.

Good:

- `profile.item.language`
- `notification.mock.goal.title`

Avoid:

- `ProfileLanguage`
- `profile.languageTitleNew`

## Translation behavior

- Keep product names unchanged: `ZenLife`.
- Translate meaning, not word-by-word.
- Keep tone consistent per locale.
- Avoid adding extra punctuation not present in source unless required by language grammar.

## Placeholders and ICU

- Preserve placeholders exactly: `{name}`, `{count}`, `{date}`.
- Preserve ICU syntax for plural/select messages.
- When key has placeholder/plural logic, keep corresponding metadata block `@<key>`.

## File consistency

- All locale files must have the same key set as `app_en.arb`.
- Keep files as valid JSON objects.
- Keep indentation consistent (2 spaces).
- Keep metadata keys (`@...`) aligned with base keys.

## Pseudo locale

- Keep `app_en_XA.arb` key set aligned with English.
- Do not delete or rename pseudo-locale keys.

## Review and release

- Run i18n scripts from app repository before release:
  - `dart run tool/i18n/sync_keys.dart`
  - `dart run tool/i18n/sync_from_arb.dart`
  - `dart run tool/i18n/validate_locales.dart --strict-orphan`
