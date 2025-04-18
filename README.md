# telegram-format

[![NPM Version](https://img.shields.io/npm/v/telegram-format.svg)](https://www.npmjs.com/package/telegram-format)
[![node](https://img.shields.io/node/v/telegram-format.svg)](https://www.npmjs.com/package/telegram-format)
[![JSR Version](https://jsr.io/badges/@edjopato/telegram-format)](https://jsr.io/@edjopato/telegram-format)
[![JSR Score](https://jsr.io/badges/@edjopato/telegram-format/score)](https://jsr.io/@edjopato/telegram-format/score)

> Format Telegram message texts with Markdown or HTML

This library abstracts the
[formatting options](https://core.telegram.org/bots/api#formatting-options) for
you.

## Install

Node.js:

```bash
npm install @flla/telegram-format
```

Deno:

```bash
deno add @edjopato/telegram-format
```

## Usage

```ts
import { html as format } from "telegram-format";
import { markdownv2 as format } from "telegram-format";

format.bold("hey");
//=> "*hey*"

format.italic("you");
//=> "_you_"

format.bold(format.italic("they"));
//=> "*_they_*"

format.url("me", "https://edjopato.de");
//=> "[me](https://edjopato.de)"

// Legacy but still works
import { markdown as format } from "telegram-format";
```

When using `format` as an alias its easy to switch between Markdown and HTML
fast.

### Escaping Input

When you have something that might be unescaped you need to use `format.escape`
before formatting it.

```ts
const username = "master_yoda";
format.italic(format.escape(username));
```

`format.monospace` and `format.monospaceBlock` will escape on their own as they
only need to escape specific characters. You do not need to escape the input in
these cases.

`MarkdownV2` and `HTML` are fairly similar in escaping inputs but `Markdown` is
not. `Markdown` is still supported by this library and by Telegram for legacy
reasons, but it behaves a bit differently. `Markdown` still escapes inputs and
does not need `format.escape` before. Also nested formatting is not supported by
telegram itself. Consider switching to `MarkdownV2` or `HTML` for simplicity
reasons.
