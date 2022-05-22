# 🏳️‍🌈 force-color-emoji

> Add the color variation selector to emoji that need it!

## Overview

Sometimes, you might notice monochrome emoji, for example ✌︎ instead of ✌️.

This is likely because this particular emoji needs an explicit
[Unicode variation selector](https://www.codejam.info/2021/11/emoji-variation-selector.html)
to be displayed properly as an emoji instead of a monochrome glyph.

It seems that some emoji pickers don't always include the variation
selector, and different systems have different defaults as for picking
the monochrome or color variant when no selector is explicitly specified.

This program leverages [ripgrep](https://github.com/BurntSushi/ripgrep)
and the [`unicode-emoji-json`](https://github.com/muan/unicode-emoji-json)
package to identify emoji that need to include the variation selector to
be properly displayed, and optionally add the variation selector in
place.

## Dependencies

[ripgrep](https://github.com/BurntSushi/ripgrep) must be installed
globally as `rg`.

```sh
apt install ripgrep
pacman -S ripgrep
brew install ripgrep
```

## Usage

```
force-color-emoji [<path>...] [--fix-all]
force-color-emoji --fix
```

To list files that contain emoji missing the variation selector:

```sh
force-color-emoji
```

Uses the current directory by default. Specify one or more paths if you
prefer:

```sh
force-color-emoji ~/blog
```

Fix all the identified emoji:

```
force-color-emoji --fix-all
```

Fix a subset of emoji:

```
force-color-emoji | grep ... | force-color-emoji --fix
```

## Example

```
~/blog $ force-color-emoji
posts.md:🏕
2021/09/zoom-h2n-pro-tips-and-tricks.md:™
2021/09/totp-2fa-support-any-password-manager.md:🐿
2021/10/tent-sleeping-bag-packed-wet.md:🏕
2021/11/emoji-variation-selector.md:☹
2021/11/emoji-variation-selector.md:✍
2021/11/homebrew-multi-user.md:✌
2021/05/macos-screen-recording-with-system-audio.md:🎚
2021/05/macos-screen-recording-with-system-audio.md:🎛

~/blog $ force-color-emoji | grep -v '™' | grep -v 2021/11/emoji-variation-selector.md
posts.md:🏕
2021/09/totp-2fa-support-any-password-manager.md:🐿
2021/10/tent-sleeping-bag-packed-wet.md:🏕
2021/11/homebrew-multi-user.md:✌
2021/05/macos-screen-recording-with-system-audio.md:🎚
2021/05/macos-screen-recording-with-system-audio.md:🎛

~/blog $ force-color-emoji | grep -v '™' | grep -v 2021/11/emoji-variation-selector.md | force-color-emoji --fix
Wrote posts.md
Wrote 2021/09/totp-2fa-support-any-password-manager.md
Wrote 2021/10/tent-sleeping-bag-packed-wet.md
Wrote 2021/11/homebrew-multi-user.md
Wrote 2021/05/macos-screen-recording-with-system-audio.md
```
