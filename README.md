# telegram-ios-build

Build-only sandbox for compiling the official open-source
[Telegram-iOS](https://github.com/TelegramMessenger/Telegram-iOS) source with a fake-signed,
non-distributable IPA. No source is mirrored here; the workflow checks out upstream at
`release-13.2` on `workflow_dispatch`.

## Important

This is **not** an app distribution. The upstream target name, bundle id and fake provisioning
profiles remain Telegram's because that is what the upstream CI build expects. Per the upstream
README, do **not** ship an app using Telegram's name/logo, obtain your own `api_id`, and publish
your own source if you distribute a derivative.

The workflow overwrites `api_id`/`api_hash` in the generated config with repository secrets
`TELEGRAM_API_ID`/`TELEGRAM_API_HASH` when present, otherwise with random build-only values. It
never uses upstream's public `api_id` `8`. If secrets are added to this repository, remember that
the uploaded IPA embeds them.

Upstream's fake provisioning profiles expired on 2026-10-30. The workflow patches the vendored
`rules_apple` `plisttool.py` to skip the profile-expiration check. This only affects this private
build sandbox and does not alter the checked-in upstream source in any repository.
