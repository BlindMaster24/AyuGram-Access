# AyuGram Access

An accessible build of [AyuGram Desktop](https://github.com/AyuGram/AyuGramDesktop), which is itself a
fork of [Telegram Desktop](https://github.com/telegramdesktop/tdesktop). The priority here is screen
reader support: [NVDA](https://www.nvaccess.org/) on Windows first, then the same surfaces on other
platforms. Everything else follows upstream.

Background: the upstream request is
[telegramdesktop/tdesktop#476 "tdesktop should be screen-reader friendly"](https://github.com/telegramdesktop/tdesktop/issues/476),
open since 2015.

## What is different

- Screen reader semantics are added to surfaces that upstream paints without any: menus, reactions,
  settings rows, shared media lists, attachment previews.
- Changes stay additive and live in our own forks of the libraries
  ([lib_ui](https://github.com/BlindMaster24/lib_ui),
  [lib_base](https://github.com/BlindMaster24/lib_base),
  [lib_tl](https://github.com/BlindMaster24/lib_tl) and the rest), so pulling upstream stays cheap.
- **Automatic updates are disabled on purpose.** An updater must never replace files we patched, so
  builds are updated manually through [Releases](../../releases).

## Builds

Release builds are published in [Releases](../../releases) of this repository. The client is a normal
AyuGram build: its features and settings work as usual, accessibility work only adds semantics and
keyboard paths.

Build instructions for the fork are the same as upstream:
[AyuGram Desktop docs](https://github.com/AyuGram/AyuGramDesktop/tree/dev/docs), and the whole
pipeline is wrapped by `Telegram/build/prepare/win.bat` plus `configure.bat`.

## Reporting an accessibility problem

A report without a speech log cannot be reproduced. Please include:

1. What you did (keyboard steps: `Shift+F10`, arrows, `Enter`, `Tab`).
2. What NVDA said - `NVDA menu -> Tools -> Speech Viewer`, quoted word for word.
3. What you expected to hear instead.

The [Accessibility Insights](https://accessibilityinsights.io/) tree helps for lists and grids, but the
speech log is the part that matters. Open an
[issue](../../issues) with that log attached.

## Branches

- `dev` - the integration branch and the only long-lived one. Verified changes land here, and releases
  are tagged here.
- `fix/<topic>` - one short-lived branch per fix. It is merged into `dev` once the change is verified
  with a screen reader, then deleted.

The library forks each keep a `dev` branch with our changes and an `upstream` remote pointing at the
original repository, so their changes can be pulled with
`git fetch upstream && git rebase upstream/<branch>`.

## Thanks

- [AyuGram Desktop](https://github.com/AyuGram/AyuGramDesktop) by
  [Radolyn](https://github.com/Radolyn) and [contributors](https://github.com/AyuGram/AyuGramDesktop/graphs/contributors)
- [AyuGram for Android](https://github.com/AyuGram/AyuGram4A) - the same idea on Android, where
  TalkBack support comes from the platform
- [Telegram Desktop](https://github.com/telegramdesktop/tdesktop) and the
  [desktop-app](https://github.com/orgs/desktop-app/repositories) libraries it is built from
- [Qt](https://www.qt.io/) - `QAccessible` is the whole foundation of this work
- [NVDA](https://www.nvaccess.org/) and [NV Access](https://www.nvaccess.org/about-us/) - the screen
  reader this build is tested with
- [Accessibility Insights](https://accessibilityinsights.io/) - the UIA tree inspection tool used
  during development
