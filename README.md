Prism-JS for DITA-OT
=========================

[![license](https://img.shields.io/github/license/jason-fox/fox.jason.prismjs.svg)](http://www.apache.org/licenses/LICENSE-2.0)
[![DITA-OT 3.2](https://img.shields.io/badge/DITA--OT-3.2-blue.svg)](http://www.dita-ot.org/3.2/)
<br/>
[![Documentation Status](https://readthedocs.org/projects/prismjsdita-ot/badge/?version=latest)](https://prismjsdita-ot.readthedocs.io/en/latest/?badge=latest)


This is a syntax highlighting DITA-OT Plug-in which integrates the flexible [Prism-JS](https://github.com/PrismJS/prism) highlighting library into the DITA Open Toolkit engine. This enables the generation of documents including code snippets which are automatically colorized according to language syntax. The plug-in extends both static HTML and PDF transtypes.

Table of Contents
=================

- [Background](#background)
  * [What is Prism-JS?](#what-is-prism-js)
- [Install](#install)
  * [Installing DITA-OT](#installing-dita-ot)
  * [Installing the Plug-in](#installing-the-plug-in)
- [Usage](#usage)
  * [Invocation from the command line](#invocation-from-the-command-line)
      - [Result](#result)
  * [Customizing the output](#customizing-the-output)
    + [Extending to other languages](#extending-to-other-languages)
    + [Altering the static HTML look and feel](#altering-the-static-html-look-and-feel)
    + [Altering the PDF look and feel](#altering-the-pdf-look-and-feel)
- [License](#license)

Background
==========

What is Prism-JS?
----------------

Prism is a lightweight, robust, elegant syntax highlighting library. It's a spin-off project from [Dabblet](http://dabblet.com/).

- Highlights embedded languages (e.g. CSS inside HTML, JavaScript inside HTML)
- Highlights inline code (`<codeph>`) as well, not just code blocks (`<codeblock>`)
- Highlights nested languages (CSS in HTML, JavaScript in HTML)
- It doesn’t force you to use any Prism-specific markup

You can learn more on http://prismjs.com/.

Why another syntax highlighter?: http://lea.verou.me/2012/07/introducing-prism-an-awesome-new-syntax-highlighter/#more-1841


Install
=======

The DITA-OT Prism-JS syntax highlighter has been tested against [DITA-OT 3.x](http://www.dita-ot.org/download). It is recommended that you upgrade to the latest version.

Installing DITA-OT
------------------

The DITA-OT Prism-JS syntax highlighter is a plug-in for the DITA Open Toolkit.

-  Full installation instructions for downloading DITA-OT can be found [here](https://www.dita-ot.org/3.2/topics/installing-client.html).

    1.  Download the `dita-ot-3.2.zip` package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download)
    2.  Extract the contents of the package to the directory where you want to install DITA-OT.
    3.  **Optional**: Add the absolute path for the `bin` directory to the _PATH_ system variable.
This defines the necessary environment variable to run the `dita` command from the command line.

```bash
curl -LO https://github.com/dita-ot/dita-ot/releases/download/3.2/dita-ot-3.2.zip
unzip -q dita-ot-3.2.zip
rm dita-ot-3.2.zip
```

Installing the Plug-in
----------------------

-  Run the plug-in installation command:

```bash
dita -install https://github.com/jason-fox/fox.jason.prismjs/archive/master.zip
```

The `dita` command line tool requires no additional configuration.


Usage
=====

To highlight the syntax within codeblocks, add an `outputclass` attribute to any `<codeph>` or `<codeblock>` elements in your `*.dita` files. Alternatively add an `outputclass` attribute to the `<body>` element, and all `<codeph>` or `<codeblock>` will inherit from it.

With the default Prism-JS [library](https://prismjs.com/download.html#themes=prism&languages=markup+css+clike+javascript)
the following languages can be highlighted

- `outputclass="language-markup"` - HTML, XML etc.
- `outputclass="language-css"` - Cascading Style Sheet highlighting
- `outputclass="language-clike"` - C-language family highlighting
- `outputclass="language-javascript"` - JavaScript highlighting

e.g.:


```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE topic PUBLIC "-//OASIS//DTD DITA Topic//EN" "topic.dtd">
<topic id="examples">
  <title>Examples</title>
  <body  outputclass="language-markup">

  <p>The Prism source, highlighted with Prism:</p>
  <codeblock outputclass="language-javascript">
    <coderef href="../src/prism.js"/>
  </codeblock>

  <p>This page’s CSS code, highlighted with Prism:</p>
  <codeblock outputclass="language-css">
    <coderef href="../src/style.css"/>
  </codeblock>

  <p>This page’s HTML, highlighted with Prism:</p>
  <codeblock outputclass="language-html">
    <coderef href="../src/index.html"/>
  </codeblock>

  <p>This page’s logo (SVG), highlighted with Prism:</p>
  <codeblock outputclass="language-markup">
    <coderef href="../src/logo.svg"/>
  </codeblock>
  </body>
</topic>
```

A test document including HTML, CSS and JavaScript code snippets can be found within the plug-in at: `PATH_TO_DITA_OT/plugins/fox.jason.prismjs/sample`

Invocation from the command line
--------------------------------

The Plug-in extends the existing PDF and HTML transforms

- to create a PDF with highlighted code snippets run:

```console
PATH-TO-DITA-OT/bin/dita -f pdf -i document.ditamap  -o out
```

#### Result

![](https://jason-fox.github.io/fox.jason.prismjs/prism-pdf.png)

- to create static HTML with highlighted code snippets run:

```console
PATH-TO-DITA-OT/bin/dita -f html5 -i document.ditamap  -o out
```

#### Result

![](https://jason-fox.github.io/fox.jason.prismjs/prism-html.png)

Customizing the output
----------------------

Prism-JS is easily extended to other languages since it purely relies on regular expressions. A large number of additional languages are supported - just look at the list on
https://github.com/PrismJS/prism/tree/master/components


### Extending to other languages

To extend code highlight to other languages, just pick
the languages of your choice from the Prism-JS [download page](https://prismjs.com/download.html#themes=prism&languages=markup+css+clike+javascript) and replace
the existing `resource/prism.js` file

### Altering the static HTML look and feel

Amend the `resource/style.css` file to alter the look-and-feel of the rendered HTML

### Altering the PDF look and feel

The `cfg/fo/attrs/prismjs-attr.xsl` provides the colors for the PDF output. The names of the attributes match the CSS file.


License
=======

[Apache 2.0](LICENSE) © 2018 Jason Fox

The Program includes the following additional software components which were obtained under license:

* prism.js - https://github.com/PrismJS/prism/ - **MIT license**
* xmltask.jar - http://www.oopsconsultancy.com/software/xmltask/ - **Apache 1.1 license**