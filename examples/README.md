# Examples

## PlantUML Integration

PlantUML diagrams can be integrated directly within Markdown files.
Pandoc will invoke a dedicated PlantUML filter to render the PlantUML code
to an image which is finally included in the PDF.

More details can be found in the offical documentation of the filter ([Link](https://github.com/timofurrer/pandoc-plantuml-filter)).

How to run the examples

Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           plantuml-integration.md `
           -o plantuml-integration.pdf `
           --filter pandoc-plantuml
```

Linux

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

Invocation shown based on the example `plantuml-integration.md`.

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

Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           use-case-diagrams.md \
           -t revealjs \
           --section-divs  -V theme=sky -V transition=slide \
           -s --self-contained \
           -o use-case-diagrams.html \
           --filter pandoc-plantuml
```
