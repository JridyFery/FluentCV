FluentCV
========

[![Latest release][img-release]][latest-release]
[![Build status (MASTER)][img-master]][travis-url-master]
[![Build status (DEV)][img-dev]][travis-url-dev]
[![Join the chat at https://gitter.im/hacksalot/HackMyResume][badge]][gh]

*Create polished résumés and CVs in multiple formats from your command line or
shell. Author in clean Markdown and JSON, export to Word, HTML, PDF, LaTeX,
plain text, and other arbitrary formats. Fight the power, save trees. Compatible
with [FRESH][fresca] and [JRS][6] resumes.*

![](assets/hmr_build.png)

FluentCV is a dev-friendly, local-only Swiss Army knife for resumes and CVs. It
is the corporate-friendly fork of [HackMyResume][hmr]&mdash;same tool, different
name. Use it to:

1. **Generate** HTML, Markdown, LaTeX, MS Word, PDF, plain text, JSON, XML,
YAML, print, smoke signal, carrier pigeon, and other arbitrary-format resumes
and CVs, from a single source of truth&mdash;without violating DRY.
2. **Analyze** your resume for keyword density, gaps/overlaps, and other
metrics.
3. **Convert** resumes between [FRESH][fresca] and [JSON Resume][6] formats.
4. **Validate** resumes against either format.

FluentCV is built with Node.js and runs on recent versions of OS X, Linux,
or Windows. View the [FAQ](FAQ.md).

![](assets/hmr_analyze.png)

## Features

- OS X, Linux, and Windows.
- Choose from dozens of FRESH or JSON Resume themes.
- Private, local-only resume authoring and analysis.
- Analyze your resume for keywords, gaps, and other metrics.
- Store your resume data as a durable, versionable JSON or YAML document.
- Generate polished resumes in multiple formats without violating [DRY][dry].
- Output to HTML, Markdown, LaTeX, PDF, MS Word, JSON, YAML, plain text, or XML.
- Validate resumes against the FRESH or JSON Resume schema.
- Support for multiple input and output resumes.
- Convert between FRESH and JSON Resume resumes.
- Use from your command line or [desktop][7].
- Free and open-source through the MIT license.
- Updated daily / weekly. Contributions are [welcome](CONTRIBUTING.md).

## Install

Install the latest stable version of FluentCV with NPM:

```bash
[sudo] npm install fluentcv -g
```

## Installing PDF Support (optional)

FluentCV tries not to impose a specific PDF engine requirement on
the user, but will instead work with whatever PDF engines you have installed.

Currently, HackMyResume's PDF generation requires one of [Phantom.js][2],
[wkhtmltopdf][3], or [WeasyPrint][11] to be installed on your system and the
corresponding binary to be accessible on your PATH. This is an optional
requirement for users who care about PDF formats. If you don't care about PDF
formats, skip this step.

## Installing Themes

FluentCV supports both [FRESH][fresh-themes] and [JSON Resume][jrst]-style
résumé themes.

- FRESH themes currently come preinstalled with FluentCV.
- JSON Resume themes can be installed from NPM, GitHub, or manually.

To install a JSON Resume theme, just `cd` to the folder where you want to store
your themes and run one of:

```bash
# Install with NPM
npm install jsonresume-theme-[theme-name]

# Install with GitHub
git clone https://github.com/[user-or-org]/[repo-name]
```

Then when you're ready to generate your resume, just reference the location of
the theme folder as you installed it:

```bash
fluentcv BUILD resume.json TO out/resume.all -t node_modules/jsonresume-theme-classy
```

Note: You can use install themes anywhere on your file system. You don't need a
package.json or other NPM/Node infrastructure.

## Getting Started

To use FluentCV you'll need to create a valid resume in either
[FRESH][fresca] or [JSON Resume][6] format. Then you can start using the command
line tool. There are five basic commands you should be aware of:

- **build** generates resumes in HTML, Word, Markdown, PDF, and other formats.
Use it when you need to submit, upload, print, or email resumes in specific
formats.

    ```bash
    # fluentcv BUILD <INPUTS...> TO <OUTPUTS...> [-t THEME]
    fluentcv BUILD resume.json TO out/resume.all
    fluentcv BUILD r1.json r2.json TO out/rez.html out/rez.md foo/rez.all
    ```

- **new** creates a new resume in FRESH or JSON Resume format.

    ```bash
    # fluentcv NEW <OUTPUTS...> [-f <FORMAT>]
    fluentcv NEW resume.json
    fluentcv NEW resume.json -f fresh
    fluentcv NEW r1.json r2.json -f jrs
    ```

- **analyze** inspects your resume for keywords, duration, and other metrics.

    ```bash
    # fluentcv ANALYZE <INPUTS...>
    fluentcv ANALYZE resume.json
    fluentcv ANALYZE r1.json r2.json
    ```

- **convert** converts your source resume between FRESH and JSON Resume
formats. Use it to convert between the two formats to take advantage of tools
and services.

    ```bash
    # fluentcv CONVERT <INPUTS...> TO <OUTPUTS...>
    fluentcv CONVERT resume.json TO resume-jrs.json
    fluentcv CONVERT 1.json 2.json 3.json TO out/1.json out/2.json out/3.json
    ```

- **validate** validates the specified resume against either the FRESH or JSON
Resume schema. Use it to make sure your resume data is sufficient and complete.

    ```bash
    # fluentcv VALIDATE <INPUTS...>
    fluentcv VALIDATE resume.json
    fluentcv VALIDATE r1.json r2.json r3.json
    ```

- **peek** echoes your resume or any field, property, or object path on your
resume to standard output.

    ```bash
    # fluentcv PEEK <INPUTS...> [OBJECT-PATH]
    fluentcv PEEK rez.json # Echo the whole resume
    fluentcv PEEK rez.json info.brief # Echo the "info.brief" field
    fluentcv PEEK rez.json employment.history[1] # Echo the 1st job
    fluentcv PEEK rez.json rez2.json info.brief # Compare value
    ```    

## Supported Output Formats

FluentCV supports these output formats:

Output Format | Ext | Notes
------------- | --- | -----
HTML | .html | A standard HTML 5 + CSS resume format that can be viewed in a browser, deployed to a website, etc.
Markdown | .md | A structured Markdown document that can be used as-is or used to generate HTML.
LaTeX | .tex | A structured LaTeX document (or collection of documents) that can be processed with pdflatex, xelatex, and similar tools.
MS Word | .doc | A Microsoft Word office document (XML-driven; WordProcessingML).
Adobe Acrobat (PDF) | .pdf | A binary PDF document driven by an HTML theme (through wkhtmltopdf).
plain text | .txt | A formatted plain text document appropriate for emails or copy-paste.
JSON | .json | A JSON representation of the resume.
YAML | .yml | A YAML representation of the resume.
RTF | .rtf | Forthcoming.
Textile | .textile | Forthcoming.
image | .png, .bmp | Forthcoming.

## Use

Assuming you've got a JSON-formatted resume handy, generating resumes in
different formats and combinations is easy. Just run:

```bash
fluentcv BUILD <INPUTS> <OUTPUTS> [-t theme].
```

Where `<INPUTS>` is one or more .json resume files, separated by spaces;
`<OUTPUTS>` is one or more destination resumes, and `<THEME>` is the desired
theme (default to Modern). For example:

```bash
# Generate all resume formats (HTML, PDF, DOC, TXT, YML, etc.)
fluentcv BUILD resume.json -o out/resume.all -t modern

# Generate a specific resume format
fluentcv BUILD resume.json TO out/resume.html
fluentcv BUILD resume.json TO out/resume.pdf
fluentcv BUILD resume.json TO out/resume.md
fluentcv BUILD resume.json TO out/resume.doc
fluentcv BUILD resume.json TO out/resume.json
fluentcv BUILD resume.json TO out/resume.txt
fluentcv BUILD resume.json TO out/resume.yml

# Specify 2 inputs and 3 outputs
fluentcv BUILD in1.json in2.json TO out.html out.doc out.pdf
```

You should see something to the effect of:

```
*** FluentCV v1.4.2 ***
Reading JSON resume: foo/resume.json
Applying MODERN Theme (7 formats)
Generating HTML resume: out/resume.html
Generating TXT resume: out/resume.txt
Generating DOC resume: out/resume.doc
Generating PDF resume: out/resume.pdf
Generating JSON resume: out/resume.json
Generating MARKDOWN resume: out/resume.md
Generating YAML resume: out/resume.yml
```

## Advanced

### Applying a theme

FluentCV can work with any FRESH or JSON Resume theme (the latter must be
installed first). To specify a theme when generating your resume, use the `-t`
or `--theme` parameter:

```bash
fluentcv BUILD resume.json TO out/rez.all -t [theme]
```

The `[theme]` parameter can be the name of a predefined theme OR the path to any
FRESH or JSON Resume theme folder:

```bash
fluentcv BUILD resume.json TO out/rez.all -t modern
fluentcv BUILD resume.json TO OUT.rez.all -t ../some-folder/my-custom-theme/
fluentcv BUILD resume.json TO OUT.rez.all -t node_modules/jsonresume-theme-classy
```

FRESH themes are currently pre-installed with FluentCV. JSON Resume themes
can be installed prior to use:

```bash
# Install a JSON Resume theme into a local node_modules subfolder:
npm install jsonresume-theme-[name]
# Use it with FluentCV
fluentcv build resume.json -t node_modules/jsonresume-theme-[name]
```

As of v1.6.0, available predefined FRESH themes are `positive`, `modern`,
`compact`, `minimist`, and `hello-world`. For a list of JSON Resume themes,
check the [NPM Registry](https://www.npmjs.com/search?q=jsonresume-theme).

### Merging resumes

You can **merge multiple resumes together** by specifying them in order from
most generic to most specific:

```bash
# Merge specific.json onto base.json and generate all formats
fluentcv BUILD base.json specific.json TO resume.all
```

This can be useful for overriding a base (generic) resume with information from
a specific (targeted) resume. For example, you might override your generic
catch-all "software developer" resume with specific details from your targeted
"game developer" resume, or combine two partial resumes into a "complete"
resume. Merging follows conventional [extend()][9]-style behavior and there's
no arbitrary limit to how many resumes you can merge:

```bash
fluentcv BUILD in1.json in2.json in3.json in4.json TO out.html out.doc
Reading JSON resume: in1.json
Reading JSON resume: in2.json
Reading JSON resume: in3.json
Reading JSON resume: in4.json
Merging in4.json onto in3.json onto in2.json onto in1.json
Generating HTML resume: out.html
Generating WORD resume: out.doc
```

### Multiple targets

You can specify **multiple output targets** and FluentCV will build them:

```bash
# Generate out1.doc, out1.pdf, and foo.txt from me.json.
fluentcv BUILD me.json TO out1.doc out1.pdf foo.txt
```

### Using .all

The special `.all` extension tells FluentCV to generate all supported output
formats for the given resume. For example, this...

```bash
# Generate all resume formats (HTML, PDF, DOC, TXT, etc.)
fluentcv BUILD me.json TO out/resume.all
```

..tells FluentCV to read `me.json` and generate `out/resume.md`,
`out/resume.doc`, `out/resume.html`, `out/resume.txt`, `out/resume.pdf`, and
`out/resume.json`.

### Building PDFs

*Users who don't care about PDFs can turn off PDF generation across all themes
and formats with the `--pdf none` switch.*

FluentCV takes a unique approach to PDF generation. Instead of enforcing
a specific PDF engine on users, FluentCV will attempt to work with whatever
PDF engine you have installed through the engine's command-line interface (CLI).
Currently that means any of...

- [wkhtmltopdf][3]
- [Phantom.js][2]
- [WeasyPrint][11]

..with support for other engines planned in the future. But for now, **one or
more of these engines must be installed and accessible on your PATH in order
to generate PDF resumes with FluentCV**. That means you should be able to
invoke either of these tools directly from your shell or terminal without error:

```bash
wkhtmltopdf input.html output.pdf
phantomjs script.js input.html output.pdf
weasyprint input.html output.pdf
```

Assuming you've installed one or both of these engines on your system, you can
tell FluentCV which flavor of PDF generation to use via the `--pdf` option
(`-p` for short):

```bash
fluentcv BUILD resume.json TO out.all --pdf phantom
fluentcv BUILD resume.json TO out.all --pdf wkhtmltopdf
fluentcv BUILD resume.json TO out.all --pdf weasyprint
fluentcv BUILD resume.json TO out.all --pdf none
```

### Analyzing

FluentCV can analyze your resume for keywords, employment gaps, and other
metrics. Run:

```bash
fluentcv ANALYZE <my-resume>.json
```

Depending on the FluentCV version, you should see output similar to:


```
*** FluentCV v1.7.1 ***
Reading resume: resume.json
Analyzing FRESH resume: resume.json

SECTIONS (10):

        employment:    12
         education:     2
           service:     1
            skills:     8
           writing:     1
       recognition:     0
            social:     4
         interests:     2
        references:     1
         languages:     2

COVERAGE (61.1%):

        Total Days:  6034
          Employed:  3688
              Gaps:     8  [31, 1065, 273, 153, 671, 61, 61, 31]
          Overlaps:     1  [243]

KEYWORDS (61):

           Node.js:     6 mentions
        JavaScript:     9 mentions
        SQL Server:     3 mentions
     Visual Studio:     6 mentions
           Web API:     1 mentions
   N-tier / 3-tier:     1 mentions
            HTML 5:     1 mentions
        JavaScript:     6 mentions
               CSS:     2 mentions
Sass / LESS / SCSS:     1 mentions
              LAMP:     3 mentions
              WISC:     1 mentions
              HTTP:    21 mentions
              JSON:     1 mentions
               XML:     2 mentions
              REST:     1 mentions
        WebSockets:     2 mentions
       Backbone.js:     3 mentions
        Angular.js:     1 mentions
           Node.js:     4 mentions
               NPM:     1 mentions
             Bower:     1 mentions
             Grunt:     2 mentions
              Gulp:     1 mentions
            jQuery:     2 mentions
         Bootstrap:     3 mentions
     Underscore.js:     1 mentions
         PhantomJS:     1 mentions
      CoffeeScript:     1 mentions
            Python:    11 mentions
              Perl:     4 mentions
               PHP:     7 mentions
             MySQL:    12 mentions
        PostgreSQL:     4 mentions
             NoSQL:     2 mentions
            Apache:     2 mentions
               AWS:     2 mentions
               EC2:     2 mentions
               RDS:     3 mentions
                S3:     1 mentions
             Azure:     1 mentions
         Rackspace:     1 mentions
               C++:    23 mentions
            C++ 11:     1 mentions
             Boost:     1 mentions
             Xcode:     2 mentions
               gcc:     1 mentions
             OO&AD:     1 mentions
              .NET:    20 mentions
           Unity 5:     2 mentions
              Mono:     3 mentions
       MonoDevelop:     1 mentions
           Xamarin:     1 mentions
             TOTAL:   180 mentions
```

### Validating

FluentCV can also validate your resumes against either the [FRESH /
FRESCA][fresca] or [JSON Resume][6] formats. To validate one or more existing
resumes, use the `validate` command:

```bash
# Validate myresume.json against either the FRESH or JSON Resume schema.
fluentcv VALIDATE resumeA.json resumeB.json
```

FluentCV will validate each specified resume in turn:

```bash
*** FluentCV v1.7.1 ***
Validating JSON resume: resumeA.json (INVALID)
Validating JSON resume: resumeB.json (VALID)
```

### Converting

FluentCV can convert between the [FRESH][fresca] and [JSON Resume][6]
formats. Just run:

```bash
fluentcv CONVERT <INPUTS> <OUTPUTS>
```

where <INPUTS> is one or more resumes in FRESH or JSON Resume format, and
<OUTPUTS> is a corresponding list of output file names. FluentCV will autodetect
the format (FRESH or JRS) of each input resume and convert it to the other
format (JRS or FRESH).

### File-based Options

You can pass options into FluentCV via an external options or ".fluentrc"
file with the `--options` or `-o` switch:

```bash
fluentcv BUILD resume.json -o path/to/options.json
```

The options file can contain any documented FluentCV option, including
`theme`, `silent`, `debug`, `pdf`, `css`, and other settings.

```json
{
  "theme": "compact",

  "sectionTitles": {
    "employment": "Work"
  },

  "wkhtmltopdf": {
    "margin-top": "20mm"
  }
}
```

If an option is specified on both the command line and in an external options
file, the command-line option wins.

```bash
# path/to/options.json specifes the POSITIVE theme
# -t parameter specifies the COMPACT theme
# The -t parameter wins.
fluentcv BUILD resume.json -o path/to/options.json -t compact
> Reading resume: resume.json
> Applying COMPACT theme (7 formats)
```

### Prettifying

FluentCV applies [js-beautify][10]-style HTML prettification by default to
HTML-formatted resumes. To disable prettification, the `--no-prettify` or `-n`
flag can be used:

```bash
fluentcv BUILD resume.json out.all --no-prettify
```

### Silent Mode

Use `-s` or `--silent` to run in silent mode:

```bash
fluentcv BUILD resume.json -o someFile.all -s
fluentcv BUILD resume.json -o someFile.all --silent
```

### Debug Mode

Use `-d` or `--debug` to force FluentCV to emit a call stack when errors occur.
In the future, this option will emit detailed error logging.

```bash
fluentcv build resume.json -d
fluentcv analyze resume.json --debug
```

### Disable Encoding

Use the `--no-escape` option to disable encoding in Handlebars themes. Note:
this option has no effect for non-Handlebars themes.

```bash
fluentcv build resume.json --no-escape
```

### Private Resume Fields

Have a gig, education stint, membership, or other relevant history that you'd
like to hide from *most* (e.g. public) resumes but sometimes show on others? Tag it with
`"private": true` to omit it from outbound generated resumes by default.


```json
"employment": {
  "history": [
    {
      "employer": "Acme Real Estate"
    },
    {
      "employer": "Area 51 Alien Research Laboratory",
      "private": true
    },
    {
      "employer": "H&R Block"
    }
  ]
}
```

Then, when you want a copy of your resume that includes the private gig / stint
/ etc., tell FluentCV that it's OK to emit private fields. The way you do
that is with the `--private` switch.

```bash
fluentcv build resume.json private-resume.all --private
```


### Custom theme helpers

You can attach your own custom Handlebars helpers to a FRESH theme with the
`helpers` key of your theme's `theme.json` file.

```js
{
  "title": "my-cool-theme",

  // ...

  "helpers": [
    "../path/to/helpers/*.js",
    "some-other-helper.js"
  ]
}
```

HackMyResume will attempt to load each path or glob and register any specified
files with [Handlebars.registerHelper][hrh], making them available to your
theme.


## Contributing

FluentCV is a community-driven free and open source project under the MIT
License. Contributions are encouraged and we respond to all PRs and issues in
time. See [CONTRIBUTING.md][contribute] for details.

## License

MIT. Go crazy. See [LICENSE.md][1] for details.

[1]: LICENSE.md
[2]: http://phantomjs.org/
[3]: http://wkhtmltopdf.org/
[4]: https://nodejs.org/
[5]: https://www.npmjs.com/
[6]: http://jsonresume.org
[7]: http://fluentcv.com
[8]: https://youtu.be/N9wsjroVlu8
[9]: https://api.jquery.com/jquery.extend/
[10]: https://github.com/beautify-web/js-beautify
[11]: http://weasyprint.org/
[fresh]: https://github.com/fluentdesk/FRESH
[fresca]: https://github.com/fresh-standard/fresh-resume-schema
[dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[img-release]: https://img.shields.io/github/release/fluentdesk/FluentCV.svg?label=version
[img-master]: https://img.shields.io/travis/fluentdesk/FluentCV/master.svg
[img-dev]: https://img.shields.io/travis/fluentdesk/FluentCV/dev.svg?label=dev
[travis-url-master]: https://travis-ci.org/fluentdesk/FluentCV?branch=master
[travis-url-dev]: https://travis-ci.org/fluentdesk/FluentCV?branch=dev
[latest-release]: https://github.com/fluentdesk/FluentCV/releases/latest
[contribute]: CONTRIBUTING.md
[fresh-themes]: https://github.com/fluentdesk/fresh-themes
[jrst]: https://www.npmjs.com/search?q=jsonresume-theme
[gh]: https://gitter.im/hacksalot/HackMyResume?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge
[badge]: https://badges.gitter.im/hacksalot/HackMyResume.svg
[hrh]: http://handlebarsjs.com/reference.html#base-registerHelper
[hmr]: https://github.com/hacksalot/hackmyresume
