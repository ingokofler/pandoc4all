# Examples

> **_NOTE:_**  The name of the image needs to be adapted and is currently
> `pandoc4all` in all of the examples.

## Thesis support

The image contains all necessary packages to run the PhD thesis template
provided on [GitHub](https://github.com/tompollard/phd_thesis_markdown).

The only thing that needs to be adapted is to remove the [line that includes the
`eps` logo file from the title page](https://github.com/tompollard/phd_thesis_markdown/blob/master/style/template.tex#L205).

### How to run - Windows Powershell

```powershell
# change to a directory of your choice
cd c:\your\path\here

# get the current thesis
git clone https://github.com/tompollard/phd_thesis_markdown.git

# remove logo from title page in file style/template.tex

# run an interactive shell in the container
docker run -it -v C:\your\path\here\phd_thesis_markdown:/data `
           --entrypoint=/bin/sh `
           --rm `
           pandoc4all

# run the make pdf target in the container
$ make pdf
```

### How to run - Linux

```shell
# change to a directory of your choice
cd /your/path/here

# get the current thesis
git clone https://github.com/tompollard/phd_thesis_markdown.git

# remove logo from title page in file style/template.tex

# run an interactive shell in the container
docker run -it -v /your/path/here/phd_thesis_markdown:/data \
           --entrypoint=/bin/sh \
           --rm \
           pandoc4all

# run the make pdf target in the container
$ make pdf
```

## PlantUML Integration

PlantUML diagrams can be integrated directly within Markdown files.
Pandoc will invoke a dedicated PlantUML filter to render the PlantUML code
to an image which is finally included in the PDF.

More details can be found in the offical documentation of the filter ([Link](https://github.com/timofurrer/pandoc-plantuml-filter)).

> **_NOTE:_** Using the integration requires the extra paramters `--filter pandoc-plantuml` on the command line.

### How to run - Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           plantuml-integration.md `
           -o plantuml-integration.pdf `
           --filter pandoc-plantuml
```

### How to run - Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           plantuml-integration.md \
           -o plantuml-integration.pdf \
           --filter pandoc-plantuml
```

## reveal.js

pandoc can also be used to create presentations based on [reveal.js](https://revealjs.com/) based on Markdown syntax. It allows for creating self-contained
presentations in a single HTML file with the intrinsic simplicity of Markdown.

As an example see the presentation on [Use Case Diagrams](use-case-diagrams.md) and the resulting [HTML presentation](use-case-diagrams.html).

Further examples can be found at <https://github.com/jgm/pandoc/wiki/Using-pandoc-to-produce-reveal.js-slides>.

### How to run - Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           use-case-diagrams.md `
           -t revealjs `
           --section-divs  -V theme=sky -V transition=slide `
           -s --self-contained `
           -o use-case-diagrams.html `
           --filter pandoc-plantuml
```

### How to run - Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           use-case-diagrams.md \
           -t revealjs \
           --section-divs  -V theme=sky -V transition=slide \
           -s --self-contained \
           -o use-case-diagrams.html \
```

## Included Eisvogel Template

The image comes with the [Eisvogel Pandoc Latex](https://github.com/Wandmalfarbe/pandoc-latex-template) template for rendering.
See the [Examples](https://github.com/Wandmalfarbe/pandoc-latex-template/tree/master/examples) on what can be achieved with this template. Of course
this template can be combined with the Plant UML support.
Note that the stylesheet can be parametrized based on the available
[Custom Template Variables](https://github.com/Wandmalfarbe/pandoc-latex-template#custom-template-variables).

This template is greate for creating assignment sheets including code samples
and/or UML diagrams as demonstrated in this [real-world example](assignment-using-eisvogel.pdf).

The most recent template is located in the image at `/opt/eisvogel/eisvogel.tex`.
One can inspect the file `/opt/eisvogel/version` to check for the included
version.

### How to run - Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           assignment-using-eisvogel.md `
           -o assignment-using-eisvogel.pdf `
           -V header-center="PLF" `
           --listings `
           --template eisvogel.tex `
           --filter pandoc-plantuml
```

### How to run - Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           assignment-using-eisvogel.md \
           -o assignment-using-eisvogel.pdf \
           -V header-center="PLF" \
           --listings \
           --template eisvogel.tex \
           --filter pandoc-plantuml
```
