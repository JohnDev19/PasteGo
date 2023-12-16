<div align="center">
  <img height="100" src="(https://github.com/JohnDev19/PasteGo/blob/7de1b3ac4244a9cb52b38cfc32ee6de74a033693/IMG_20231015_103745.jpg)">
</div>

# What is PasteGo?

[PasteGo](https://johndev19.github.io/PasteGo/) is a simple and secure paste service that stores your data entirely in the link, without any database or back-end code. Easily share your text, code, or images with others, and they can access it without needing an account. It is an open-source tool that allows you to store and share any text, code, or image with a unique link. It's simple, secure, and doesn't require an account.

However, what makes NoPaste special is that it works with **no database**, and **no back-end code**. Instead, the data is compressed and **stored entirely in the link** that you share, nowhere else!

> Of course, all of your old links will continue to work if you just replace `pastego.ml` with `pastego.sh`!

### Because of this design:

 <ul>
                <li>Your data <span>cannot be deleted</span> from PasteGo</li>
                <li>Your data <span>cannot be censored</span></li>
                <li>The server hosting PasteGo (or any clone of it) <span>cannot read or access</span> your data</li>
                <li>Your data will be accessible <span>forever</span> (as long as you have the link)</li>
                </li>
                <li>Google <span>will not index</span> your data, even if your link is public</li>

## How it works

When you click on "Generate Link", PasteGo compresses the whole text using the
[LZMA algorithm](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Markov_chain_algorithm), encodes it in
[Base64](https://en.wikipedia.org/wiki/Base64), and puts it in the optional URL fragment, after the first `#` symbol: `pastego.sh/#<your data goes here>`

When you open a link, PasteGo reads, decodes, and decompresses whatever is after the `#`, and displays the result in the editor.

This process is done entirely **in your browser**, and the web server hosting PasteGo [never has access to the fragment](https://en.wikipedia.org/wiki/Fragment_identifier)

For example, [this is the CSS code used by PasteGo][example]

## Other features

### Embedded PasteGo snippets

You can include PasteGo code snippets into your own website by clicking the _Embed_ button and using the generated HTML code.

Here is an example of generated code and how it looks (click on the screenshot to see the interactive version)

```html
<iframe
    width="100%"
    height="243"
    frameborder="0"
    src="https://johndev19.github.io/PasteGo/?l=py#XQAAAQAbAQAAAAAAAAA0m0pnuFI8c+qagMoNTEcTIfyUWbZjtjmBYcmJSzoNwS5iVMWHzvowv3IPM0vOG5cjrtDRTSVP/0biTIrrahfmbkuMQBBeSiSGpaJOqYJiKmUDYn2Gp1RtWE6gm8fLHMB4eyZ3+rEbUQwWyMcmWqvZ7m96RUeFyZdYbE85JGvhghqF8cyPB0ZjV0OQWsDxn5O5ysMrIcL+pKPk89EtLjAHhA1LZL9F3hzAtTx7I+GlyrxhhXGxAN//CvtaAA=="
></iframe>
```

Feel free to edit the `height` and `width` attributes, so they suit your needs

### Offline usage

When you visit PasteGo for the first time, its code is saved in your browser cache. After that, every PasteGo link you open
will load really quick, even if your internet connection is slow.

What if you have no internet connection at all? No problem, PasteGo will still work perfectly!

### Editor features

-   Syntax highlighting (use the language selector)
-   Enable / disable line wrapping (use the button next to the language selector)
-   Delete line (`Ctrl+D`)
-   Multiple cursors (`Ctrl+Click`)
-   Usual keyboard shortuts (`Ctrl+A`, `Ctrl+Z`, `Ctrl+Y`...)

## Maximum sizes for links

PasteGo is great for sharing code snippets on various platforms.

These are the maximum link lengths on some apps and browsers.

| App     | Max length |
| ------- | ---------- |
| Reddit  | 10,000     |
| Twitter | 4,088      |
| Slack   | 4,000      |
| QR Code | 2,610      |
| Bitly   | 2,048      |

| Browser         | Max length                | Notes                                   |
| --------------- | ------------------------- | --------------------------------------- |
| Google Chrome   | (win) 32,779 (mac) 10,000 | Will not display, but larger links work |
| Firefox         | >64,000                   |                                         |
| Microsoft IE 11 | 4,043                     | Will not show more than 2,083           |
| Microsoft Edge  | 2,083                     | Anything over 2083 will fail            |
| Android         | 8,192                     |                                         |
| Safari          | Lots                      |                                         |

## Generate PasteGo links

PasteGo links can be created easily from your system's command line:

```bash
# Linux
echo -n 'Hello World' | lzma | base64 -w0 | xargs -0 printf "https://johndev19.github.io/PasteGo/#%s\n"

# Mac
echo -n 'Hello World' | lzma | base64 | xargs -0 printf "https://johndev19.github.io/PasteGo/#%s\n"

# Windows / WSL / Linux
echo -n 'Hello World' | xz --format=lzma | base64 -w0 | printf "https://johndev19.github.io/PasteGo/#%s\n" "$(cat -)"
```
