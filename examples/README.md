# Examples

## PlantUML Integration

PlantUML diagrams can be integrated directly within Markdown files.
Pandoc will invoke a dedicated PlantUML filter to render the PlantUML code
to an image which is finally included in the PDF.

More details can be found in the offical documentation of the filter ([Link](https://github.com/timofurrer/pandoc-plantuml-filter)).

> **_NOTE:_** Using the integration requires the extra paramters `--filter pandoc-plantuml` on the command line.

## How to run the examples

Invocation shown based on the example `plantuml-integration.md`.

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


## Included Eisvogel Template

The image comes with the [Eisvogel Pandoc Latex](https://github.com/Wandmalfarbe/pandoc-latex-template) template for rendering.

See the [Examples](https://github.com/Wandmalfarbe/pandoc-latex-template/tree/master/examples) on what can be achieved with this template. Of course
this template can be combined with the Plant UML support.

The most recent template is located in the image at `/opt/eisvogel/eisvogel.tex`.
One can inspect the file `/opt/eisvogel/version` to check for the included
version.

How to run the examples

Invocation shown based on the example `assignment-using-eisvogel.md`.

Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           assignment-using-eisvogel.md `
           -o assignment-using-eisvogel.pdf `
           --filter pandoc-plantuml
```

Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           assignment-using-eisvogel.md \
           -o assignment-using-eisvogel.pdf \
           --filter pandoc-plantuml
```

docker run -it -v $(pwd):/data \
           pandoc4all \
           assignment-using-eisvogel.md \
           -o assignment-using-eisvogel.pdf \
           -V header-center="PLF" \
           --template eisvogel.tex \
           --filter pandoc-plantuml
