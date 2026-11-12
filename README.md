# AyuGram Access

An accessible build of [AyuGram Desktop](https://github.com/AyuGram/AyuGramDesktop) (which itself is a
fork of Telegram Desktop). The priority here is screen reader support: NVDA on Windows first, then the
same surfaces on other platforms. Everything else follows upstream.

## What is different

- Screen reader semantics are added to surfaces that upstream paints without any: menus, reactions,
  settings rows, shared media lists, attachment previews.
- Changes stay additive and are kept in our own forks of the libraries (`lib_ui`, `lib_base`, `lib_tl`
  and the rest), so pulling upstream changes stays cheap.
- **Automatic updates are disabled.** Builds are updated manually, on purpose: an updater must never
  replace files we patched.

## Builds

Release builds are published in this repository's releases. The client is a normal AyuGram build,
so its features and settings work as usual; accessibility work only adds semantics and keyboard paths.

## Reporting an accessibility problem

A report without a speech log cannot be reproduced. Please include:

1. What you did (keyboard steps: `Shift+F10`, arrows, `Enter`, `Tab`).
2. What NVDA said (`NVDA menu -> Tools -> Speech Viewer`), quoted word for word.
3. What you expected to hear instead.

An `Accessibility Insights` tree fragment helps for lists and grids, but the speech log is the part
that matters.

## Branches

- `dev` - the integration branch and the only long-lived one. Verified changes land here, and releases
  are tagged here.
- `fix/<topic>` - one short-lived branch per fix. It is merged into `dev` once the change is verified
  with a screen reader, then deleted.

The library forks (`lib_ui`, `lib_base`, `lib_tl`, and the rest) each keep a `dev` branch with our
changes and an `upstream` remote pointing at the original repository.

## Thanks

AyuGram Desktop by Radolyn and contributors; Telegram Desktop by the tdesktop team.
